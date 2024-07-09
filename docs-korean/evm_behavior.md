# EVM 동작

## EVM 동작 명세

- [EVM에 대한 노트](https://github.com/CoinCulture/evm-tools/blob/master/analysis/guide.md): EVM에 대한 간단한 기술 명세와 몇 가지 동작 예시를 포함합니다.
- [EVM: Solidity에서 바이트코드, 메모리 및 스토리지로](https://www.youtube.com/watch?v=RxL_1AfV7N4): Peter Robinson과 David Hyland-Wood의 90분 강연.
- [EVM 일러스트](https://takenobu-hs.github.io/downloads/ethereum_evm_illustrated.pdf): 정신 모델을 확인하기 위한 훌륭한 다이어그램 세트.
- [EVM 딥 다이브: Shadowy Super-Coder로 가는 길](https://noxx.substack.com/p/evm-deep-dives-the-path-to-shadowy)

## Opcode 참조

- [evm.codes](https://www.evm.codes/): 연산 코드 참조(가스 비용 포함) 및 바이트코드 실행을 단계별로 확인할 수 있는 인터랙티브 샌드박스.

## 솔리디티 스토리지 레이아웃

EVM은 스마트 계약이 32바이트 단어("스토리지 슬롯")에 데이터를 저장할 수 있도록 허용하지만, 목록이나 매핑과 같은 복잡한 데이터 구조를 처리하는 방법은 상위 언어의 구현 세부 사항으로 남아 있습니다. Solidity는 변수들을 스토리지 슬롯에 할당하는 특정한 방법을 가지고 있으며, 아래에서 설명합니다:

- [스토리지 레이아웃에 대한 공식 문서](https://docs.soliditylang.org/en/latest/internals/layout_in_storage.html)
- [솔리디티에서의 스토리지 패턴](https://programtheblockchain.com/posts/2018/03/09/understanding-ethereum-smart-contract-storage/)
