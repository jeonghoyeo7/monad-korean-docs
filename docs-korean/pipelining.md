# 파이프라이닝 (Pipelining)

*파이프라이닝*은 작업을 일련의 더 작은 작업으로 나누어 병렬로 처리할 수 있게 하는 기술입니다.

파이프라이닝은 컴퓨터 프로세서에서 일련의 명령을 동일한 클록 속도로 순차적으로 실행하는 처리량을 증가시키기 위해 사용되는 한가지 기술입니다. 명령 수준 병렬성(ILP, instruction-level parallelism)에 대한 자세한 내용은 [여기](https://en.wikipedia.org/wiki/Instruction_pipelining)에서 찾을 수 있습니다.

간단한 파이프라이닝 예시:

![빨래하는 날의 파이프라이닝. 위: 평범한 방식; 아래: 파이프라인 방식.  출처: Prof. [Lois Hawkes, FSU](https://www.cs.fsu.edu/~hawkes/cda3101lects/chap6/index.html?$$$F6.1.html$$$)](pipelining_example.png)

세탁물 네 번 세탁 시, 단순한 전략은 첫 번째 세탁물을 세탁하고, 건조하고, 접고, 저장한 후 두 번째 세탁을 시작하는 것이겠지? 하지만 스마트한 방법은 아닐것입니다. 
파이프라이닝 전략은 첫 번째 세탁물이 건조기에 들어갈 때 두 번째 세탁을 시작하는 것입니다. 파이프라이닝은 여러 자원을 동시에 활용하여 작업을 더 효율적으로 수행합니다.
