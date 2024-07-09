# 모나드BFT (Monad BFT)

파이프라인된 두단계 핫스터프 합의 (Pipelined two-phase HotStuff Consensus)

모나드BFT는 부분 동기 조건에서 비잔틴 행위자가 존재하는 상황에서 트랜잭션 순서에 대한 합의를 달성하기 위한 고성능 합의 메커니즘입니다. 이것은 [HotStuff](https://arxiv.org/pdf/1803.05069.pdf)에서 파생된 것으로, [Jolteon](https://arxiv.org/pdf/2106.10362.pdf) / [DiemBFT](https://developers.diem.com/papers/diem-consensus-state-machine-replication-in-the-diem-blockchain/2021-08-17.pdf) / [Fast-HotStuff](https://arxiv.org/abs/2010.11454)에서 제안된 개선 사항을 포함하고 있습니다. 이는 리더 타임아웃 이벤트에서 쿼드러틱 통신 복잡성을 활용하여 세 라운드에서 두 라운드로 줄였습니다.

모나드BFT는 낙관적 응답성과 함께 파이프라인 처리되는 두 단계의 BFT 알고리즘으로, 일반적인 경우에 선형 통신 오버헤드(즉, 노드수에 비례하는 크기)가 있으며 타임아웃의 경우에는 쿼드러틱 통신 오버헤드(노드수의 제곱에 비례하는 크기)가 있습니다. 대부분의 BFT 알고리즘에서와 같이 통신은 여러 단계로 진행됩니다. 각 단계에서 리더는 유권자에게 서명된 메시지를 보내고, 유권자는 다음 리더에게 서명된 응답을 보냅니다. 파이프라인 처리는 블록 `k`에 대한 쿼럼 증명(QC) 또는 타임아웃 증명(TC)을 블록 `k+1`의 제안서에 실을 수 있게 합니다.

## 요약

| 항목                      | 내용                   |
|--------------------------|------------------------|
| 시빌 저항 메커니즘        | 지분 증명(Proof-of-Stake) |
| 블록 시간                 | 1초                    |
| 최종성                    | 단일 슬롯              |
| 위임 허용 여부            | 예                     |

## 멤풀

[공유 멤풀](shared_mempool.md)을 참조하십시오.

## 합의 프로토콜

모나드BFT는 라운드로 진행되는 파이프라인 합의 메커니즘입니다. 아래 설명은 프로토콜에 대한 대략적이면서 직관적인 이해를 제공합니다.

관례적으로, 비잔틴 노드의 최대 수를 `f`라고 하고, `n = 3f + 1` 노드가 있다고 가정합시다. 즉, `2f + 1` (2/3)의 노드는 비잔틴 노드가 아닙니다. 아래 논의에서는 모든 노드가 동일한 지분 가중치를 가진 것으로 간주합니다. 실제로 모든 임계값은 노드 수가 아닌 지분 가중치로 표현될 수 있습니다.

- 각 라운드에서 리더는 이전 라운드에 대한 QC 또는 TC와 함께 새로운 블록을 보냅니다.
- 각 검증자는 프로토콜 준수를 위해 해당 블록을 검토하고, 동의하면 다음 라운드의 리더에게 서명된 YES 투표를 보냅니다. 다음 리더는 `2f + 1` 검증자의 YES 투표를 집계하여 QC를 생성합니다. 이 경우 통신은 선형입니다: 리더는 블록을 검증자에게 보내고, 검증자는 투표를 다음 리더에게 직접 보냅니다.
  - 검증자가 미리 지정된 시간 내에 유효한 블록을 받지 못하면, 모든 피어에게 서명된 타임아웃 메시지를 멀티캐스트합니다. 이 타임아웃 메시지에는 검증자가 관찰한 가장 높은 QC도 포함됩니다. 검증자 중 하나가 `2f + 1` 타임아웃 메시지를 수집하면 이를 TC로 조립하여 다음 리더에게 직접 보냅니다.
- 각 검증자는 라운드 `k`에서 제안된 블록을 라운드 `k+1`에 대한 QC를 수신하면 확정합니다.
  - Alice는 라운드 `k`의 리더로서 새로운 블록을 모두에게 보냅니다 (QC 또는 TC와 함께).
  - `2f + 1` 검증자가 그 블록에 YES 투표를 하면, `k+1` 라운드의 블록에는 `k` 라운드에 대한 QC가 포함됩니다. 이 시점에서 `k` 라운드의 QC를 보는 것만으로는 `k` 라운드의 블록이 확정되었다는 것을 Valerie 검증자가 알 수 없습니다.
  - `2f + 1` 검증자가 `k+1` 블록에 YES 투표를 하면 Charlie는 `k+1`에 대한 QC와 `k+2` 라운드에 대한 블록 제안을 발표합니다. Valerie가 이 블록을 수신하면, `k` 라운드의 블록이 확정되었음을 알게 됩니다.
  - Bob이 악의적으로 행동하여 유효하지 않은 블록 제안을 보내거나 `2f + 1` 미만의 검증자에게 보냈다면 최소한 `f + 1` 검증자가 타임아웃하게 되고, 이는 다른 비잔틴이 아닌 검증자들이 타임아웃하도록 유도하여 검증자 중 하나가 `k+1` 라운드에 대한 TC를 생성하게 됩니다. 그런 다음 Charlie는 그의 제안에서 `k+1`에 대한 TC를 게시합니다.
  - 우리는 이 커밋 절차를 2-체인 커밋 규칙이라고 합니다. 검증자가 두 개의 인접한 인증된 블록 `B`와 `B'`를 보면 `B`와 모든 조상 블록을 커밋할 수 있습니다.

참고 문헌:

- Maofan Yin, Dahlia Malkhi, Michael K. Reiter, Guy Golan Gueta, Ittai Abraham. [HotStuff: BFT Consensus in the Lens of Blockchain](https://arxiv.org/abs/1803.05069), 2018.
- Mohammad M. Jalalzai, Jianyu Niu, Chen Feng, Fangyu Gai. [Fast-HotStuff: A Fast and Resilient HotStuff Protocol](https://arxiv.org/abs/2010.11454), 2020.
- Rati Gelashvili, Lefteris Kokoris-Kogias, Alberto Sonnino, Alexander Spiegelman, Zhuolun Xiang. [Jolteon and ditto: Network-adaptive efficient consensus with asynchronous fallback](https://arxiv.org/pdf/2106.10362.pdf). arXiv preprint arXiv:2106.10362, 2021.
- The Diem Team. [DiemBFT v4: State machine replication in the diem blockchain](https://developers.diem.com/papers/diem-consensus-state-machine-replication-in-the-diem-blockchain/2021-08-17.pdf). 2021.

## BLS 멀티서명

증명서(QC 및 TC)는 secp256k1 곡선에서 ECDSA 서명의 벡터로 구현될 수 있습니다. 이러한 증명서는 명시적이며 구성하고 검증하기 쉽습니다. 그러나 서명자의 수에 따라 증명서의 크기가 선형으로 증가합니다. 이는 투표 메시지를 제외한 거의 모든 합의 메시지에 증명서가 포함되기 때문에 확장에 한계를 초래합니다.

BLS12-381 곡선에서의 페어링 기반 BLS 서명은 확장 문제를 해결하는 데 도움이 됩니다. 서명은 점진적으로 하나의 서명으로 집계될 수 있습니다. 유효한 집계 서명을 검증하면 공개 키와 관련된 지분이 모두 메시지에 서명했음을 증명할 수 있습니다.

BLS 서명은 ECDSA 서명보다 훨씬 느립니다. 따라서 성능상의 이유로 모나드BFT는 혼합 서명 방식을 채택하여 BLS 서명을 집계 가능한 메시지 유형(투표 및 타임아웃)에만 사용합니다. 메시지의 무결성과 진정성은 여전히 ECDSA 서명에 의해 제공됩니다.
