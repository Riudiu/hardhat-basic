# Sample Hardhat Project

This project demonstrates a basic Hardhat use case. It comes with a sample contract, a test for that contract, and a script that deploys that contract.

Try running some of the following tasks:

```shell
npx hardhat help
npx hardhat test
REPORT_GAS=true npx hardhat test
npx hardhat node
npx hardhat run scripts/deploy.ts
```

<br>

## Hardhat?

- 테스트 용 노드 실행부터 테스트 코드 실행
- 스마트 컨트랙트 배포등 편리한 개발 환경 제공
- 개발환경 비교

![image](https://github.com/Riudiu/hardhat-basic/assets/86466976/c834e9d7-8831-4db4-ab5e-191d3794a5ee)

<br>

## Hardhat install

**설치 순서**

1. node.js 설치
2. 프로젝트를 만들고 싶은 폴더(Part1-1)에서 `npx hardhat init` 명령어를 통해 hardhat을 설치
3. 옵션설정은 Create a Typescriptproject → y → y
4. 아래의 hardhat - solidity extension을 설치
   ![image](https://github.com/Riudiu/hardhat-basic/assets/86466976/5420665d-6d99-4d9c-924b-359c3758a8d8)
5. (옵션) `npm install --save @openzeppelin/contracts` 를 통해 openzeppelin/contracts module을 추가

<br>

### hardhat 폴더/파일 구조 간단한 설명

![image](https://github.com/Riudiu/hardhat-basic/assets/86466976/15476116-af1b-4762-a621-192d53ca8460)

- contracts: 컨트랙트 코드 작성
- scripts: 스크립트 파일 작성(컨트랙트 배포할 때 사용)
- test: 테스트 코드 작성
- hardhat.config.js: 배포할 네트워크와 솔리디티 버전은 설정

<br>

## ERC20

ERC20: A standard interface for tokens.

### ERC? EIP?

EIP: **Ethereum Improvement Proposals**

ERC: **Ethereum Improvement Proposals를 코드로 만든것**

즉 EIP는 아이디어, ERC는 아이디어를 코드로 만든것!

<br>

```shell
# 컴파일
npx hardhat compile

# 테스트 코드 실행
npx hardhat test

# hardhat 로컬 배포
npx hardhat node                                        # local node 실행
npx hardhat run --network localhost scripts/deploy.ts   # localhost network에 배포

# hardhat 테스트 넷 배포 (메인넷에 배포하고 테스트하기에는 높은 비용 때문에 테스트넷 사용)
npx hardhat run --network <your-network> scripts/deploy.ts
npx hardhat run --network sepolia scripts/deploy.ts         # 이더리움 Seporlia testnet을 이용 예시
```

<br>

## Hardhat 관련 팁

### 1. Hardhat Network Helpers

실제 네트워크를 포크해서 사용할 수도 있습니다. local 혹은 HRE에서 실행하고 테스트해볼 수 있습니다.  
테스트 하다보면 이미 배포되어있는 컨트랙트와 상호작용하고 싶을때가 있을 수 있습니다. 이때 즐겨 사용합니다.

https://hardhat.org/hardhat-network/docs/guides/forking-other-networks

가상의 채굴을 통해 시간에 따른 변화도 테스트 해볼 수 있습니다.  
https://hardhat.org/hardhat-network-helpers/docs/overview

### 2. ethers - typechain

typescript로 사용할 경우, compile하면 typechain이 생겨납니다. 이를 통해 내가 실행하고자하는 컨트랙트의  
interface를 그때그때 확인할 수 있어 편합니다. 실수도 당연히 줄고요. 그리고 에러 찾기도 편합니다!

그래서 뭐다? hardhat을 쓸려면 무무무무무무무조건 타입스크립트로 프로젝트 만드세요

### 3. hardhat - ethers plugin

`ethers.getContractAt` 이나 `ethers.getContractFactory`  
를 사용해서 긴 코드를 사용하지 않고도 아주 쉽게 컨트랙트의 인스턴스를 생성 할 수 있습니다.

### 4. hardhat-gas-reporter

gas 측정하는데 사용합니다. 그때그때 현재 네트워크에서 발생하는 가스도 측정이 가능합니다.

### 5. hardhat/console.sol

contract 특성상 함수가 실행되고 어디서 에러가 났는지 revert 를 설정하지 않으면 전혀 알 수 없습니다.
contract 코드 상에 콘솔을 찍을 수 있어 에러를 찾는데 매우 용이합니다.  
https://hardhat.org/tutorial/debugging-with-hardhat-network
