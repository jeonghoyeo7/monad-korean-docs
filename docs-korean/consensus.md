# 합의 (Consensus)

모나드의 합의를 이해하기 위해서는 몇 가지 핵심 영역을 이해해야 합니다:

- [MonadBFT](monad_bft.md): 부분 동기 조건에서 임의의 페이로드에 대한 합의를 달성하면서 비잔틴 결함 허용성(Byzantine fault tolerance, BFT)을 유지하기 위한 모나드의 합의 메커니즘.
- [공유 메모리 풀](shared_mempool.md): 거래를 해시로 참조하고, 거래가 미리 메모리 풀을 통해 전파되도록 보장함으로써 합의 페이로드에 대한 중요한 최적화를 정의.
- [비동기 실행](asynchronous_execution.md): 실행과 합의 프로세스를 별도로 갖는 방법으로서 합의 과정에 대한 중요한 최적화.
- [운송 비용 및 예비 잔액](carriage_cost_reserve_balance.md): 합의가 지연된 실행 뷰를 통해 이루어지기 때문에 스팸을 방지하기 위해 거래 가격에 대한 행동 변화를 정의.
