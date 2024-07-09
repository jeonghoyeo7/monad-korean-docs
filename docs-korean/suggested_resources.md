# 추천 리소스

모나드는 모든 지원되는 연산코드 및 사전 컴파일과 함께 EVM 바이트코드와 완전히 호환됩니다. 이는 [상하이 포크](https://www.evm.codes/?fork=shanghai)를 기준으로 합니다. 모나드는 또한 표준 이더리움 JSON-RPC 인터페이스를 유지합니다.

따라서 이더리움 메인넷을 위한 대부분의 개발 리소스가 모나드 개발에도 적용됩니다.

이 페이지는 이더리움을 위한 분산 앱을 구축하는 데 필요한 **최소한의** 리소스를 제안합니다. 자식 페이지에서는 추가 세부 정보나 옵션을 제공합니다.

[솔리디티(Solidity)](https://docs.soliditylang.org/)가 이더리움 스마트 계약의 가장 인기 있는 언어이기 때문에, 이 페이지의 리소스는 주로 Solidity에 중점을 둡니다. 대안으로 [바이퍼(Vyper)](https://using-monad/developing-on-monad/suggested-resources/other-languages/vyper-resources) 또는 [Huff](https://using-monad/developing-on-monad/suggested-resources/other-languages/huff-resources) 리소스를 참조하세요. 스마트 계약은 구성 가능하기 때문에, 처음에 다른 언어로 작성된 계약도 여전히 다른 언어로 작성된 계약을 호출할 수 있습니다.

## IDE

- [Remix](https://remix.ethereum.org/#lang=en&optimize=false&runs=200&evmVersion=null)는 대화형 Solidity IDE입니다. 추가 도구 설치 없이 Solidity 스마트 계약을 코딩하고 컴파일하는 가장 쉽고 빠른 방법입니다.
- [VSCode](https://code.visualstudio.com/) + [솔리디티 확장](https://marketplace.visualstudio.com/items?itemName=NomicFoundation.hardhat-solidity)

## 기본 솔리디티

- [CryptoZombies](https://cryptozombies.io/en/course)는 EVM에서 dApp을 구축하는 것에 대한 종합적인 소개를 제공합니다. 코딩을 전혀 해본 적이 없는 사람부터 다른 분야의 숙련된 개발자까지 블록체인 개발을 탐색하려는 사람들에게 리소스와 수업을 제공합니다.
- [Solidity by Example](https://solidity-by-example.org/)는 간단한 예제를 통해 점진적으로 개념을 소개합니다. 다른 언어에 대한 기본 경험이 있는 개발자에게 적합합니다.

## 중급 솔리디티

- [Solidity Language](https://docs.soliditylang.org/en/v0.8.21/introduction-to-smart-contracts.html) 공식 문서는 EVM 환경을 중심으로 한 스마트 계약 및 블록체인 기본 사항에 대한 종합적인 설명을 제공합니다. 이 문서에는 Solidity 언어 문서 외에도 EVM에서 코드를 컴파일하고 배포하는 기본 사항 및 EVM에서 스마트 계약을 배포할 때 관련된 기본 구성 요소가 포함되어 있습니다.
- [Solidity Patterns](https://github.com/fravoll/solidity-patterns) 저장소는 코드 템플릿 라이브러리와 그 사용법에 대한 설명을 제공합니다.
- [Uniswap V2](https://github.com/Uniswap/v2-core) 계약은 실제 사용 중인 Solidity dApp에 대한 훌륭한 개요를 제공하는 전문적이면서도 이해하기 쉬운 스마트 계약입니다. 계약에 대한 안내된 워크스루는 [여기](https://ethereum.org/en/developers/tutorials/uniswap-v2-annotated-code/)에서 찾을 수 있습니다.
- [Cookbook.dev](https://www.cookbook.dev/search?q=cookbook&categories=Contracts&sort=popular&filter=&page=1)는 라이브 편집, 원클릭 배포 및 코드 질문에 도움을 주는 AI 채팅 통합 기능이 있는 상호작용 예제 템플릿 계약 세트를 제공합니다.
- [OpenZeppelin](https://www.openzeppelin.com/contracts)은 ERC20, ERC712 및 ERC1155와 같은 일반적인 이더리움 토큰 배포를 위한 사용자 정의 가능한 템플릿 계약 라이브러리를 제공합니다. 단, 가스 최적화는 되어 있지 않습니다.

## 고급 솔리디티

- [Solmate 저장소](https://github.com/transmissions11/solmate) 및 [Solady 저장소](https://github.com/Vectorized/solady/tree/main)는 Solidity 또는 Yul을 활용하여 가스 최적화된 계약을 제공합니다.
- [Yul](https://docs.soliditylang.org/en/latest/yul.html)은 일반적으로 EVM용 인라인 어셈블리로 생각할 수 있는 중간 언어입니다. 순수 어셈블리는 아니지만 제어 흐름 구조를 제공하고 스택의 내부 작업을 추상화하면서도 개발자에게 원시 메모리 백엔드를 노출합니다. Yul은 고성능 가스 최적화된 EVM 코드를 작성하기 위해 EVM의 원시 메모리 백엔드에 접근해야 하는 개발자를 대상으로 합니다.
- [Huff](https://docs.huff.sh/get-started/overview/)는 EVM 어셈블리로 설명될 수 있습니다. Yul과 달리 제어 흐름 구조를 제공하지 않으며 프로그램 스택의 내부 작업을 추상화하지 않습니다. 성능에 매우 민감한 애플리케이션만 Huff를 사용하지만, EVM이 가장 낮은 수준에서 명령을 해석하는 방법을 배우는 데 훌륭한 교육 도구입니다.

## 로컬 노드

개발자는 블록체인과의 상호작용을 테스트하기 위해 수정된 매개변수로 1노드 이더리움 네트워크를 실행할 수 있기를 원합니다:

- [Anvil](https://github.com/foundry-rs/foundry/tree/master/crates/anvil)은 Foundry 툴킷에 패키지된 로컬 이더리움 노드입니다.
- [Hardhat Network](https://hardhat.org/hardhat-network/docs/overview)는 Hardhat 툴킷에 패키지된 로컬 이더리움 노드입니다.

설치는 각각의 툴킷을 설치하는 과정의 일부로 가장 쉽게 수행됩니다. 

## 툴킷

개발자는 종종 외부 종속성을 관리하고(즉, 패키지 관리), 단위 및 통합 테스트를 조직하고, 배포 절차(로컬 노드, 테스트넷 및 메인넷에 대해)를 정의하고, 가스 비용을 기록하는 등 더 광범위한 프레임워크의 컨텍스트에서 프로젝트를 빌드하는 것을 유용하게 생각합니다.

다음은 Solidity 개발을 위한 가장 인기 있는 두 가지 툴킷입니다:

- [Foundry](https://book.getfoundry.sh/)는 개발 및 테스트를 위한 Solidity 프레임워크입니다. Foundry는 종속성을 관리하고, 프로젝트를 컴파일하며, 테스트를 실행하고, 배포하며, 커맨드 라인 및 Solidity 스크립트를 통해 체인과 상호작용할 수 있게 합니다. Foundry 사용자는 일반적으로 Solidity 언어로 스마트 계약 및 테스트를 작성합니다.
- [Hardhat](https://hardhat.org/docs)은 JavaScript 테스트 프레임워크와 짝을 이루는 Solidity 개발 프레임워크입니다. Foundry와 유사한 기능을 제공하며, Foundry 이전에 EVM 개발자들에게 가장 많이 사용된 도구 체인이었습니다.

## 이더리움 RPC API와의 상호작용

dapp의 프론트엔드는 일반적으로 JavaScript 또는 Python을 사용하여 RPC 노드에 읽기 또는 쓰기 쿼리를 제출합니다. 이 코드는 일반적으로 "클라이언트 측"이라고 하며, 웹 개발자가 블록체인을 백엔드 서버에 비유할 수 있습니다.

몇몇 라이브러리는 RPC 노드에 쿼리 또는 트랜잭션을 제출하기 위한 표준 방법을 제공합니다:

- Python:
  - [web3.py](https://web3py.readthedocs.io/en/stable/)
- Javascript:
  - [web3.js](https://web3js.readthedocs.io/)
  - [ethers.js](https://docs.ethers.org/)

이를 위해 [Web3.js](https://web3js.readthedocs.io/en/v1.10.0/getting-started.html)와 [Web3.py](https://web3py.readthedocs.io/en/stable/quickstart.html)는 각각 Java Script 및 Python 라이브러리로서 웹 개발자가 블록체인과의 상호작용을 보다 직관적으로 할 수 있도록 발전했습니다.

프론트엔트를 만드는 간단한 예시는 [create-eth-app](https://github.com/PaulRBerg/create-eth-app)에서 확인할 수 있습니다.

## 테스트넷

모나드 테스트넷은 향후 몇 달 내에 개발자에게 제공될 예정입니다. 그러나 바이트코드 및 RPC가 EVM과 호환되기 때문에 모나드에 배포하려는 개발자는 [이더리움의 테스트넷](https://ethereum.org/en/developers/docs/networks/)을 임시로 사용할 수 있습니다.

## 추가 세부 정보

하위 페이지는 추가 리소스를 제공합니다:

- [EVM 동작](evm_behavior.md)
- [추가 Solidity 리소스](further_solidity_resources.md)
- [온체인 디버깅](debuggin_on_chain.md)
- [기타 언어](other_languages.md)
  - [Vyper](vyper_resources.md)
  - [Huff](huff_resources.md)
