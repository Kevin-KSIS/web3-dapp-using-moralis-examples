# Code dApp bằng Morailis

Status: In progress
Tags: Blockchain, dapps
Guideline: [https://docs.moralis.io/guides/deploy-and-track-erc20-events#deploy-smart-contract](https://docs.moralis.io/guides/deploy-and-track-erc20-events#deploy-smart-contract)  

## Async/Await

- **Async / Await** là một tính năng của JavaScript giúp chúng ta làm việc với các hàm bất đồng bộ theo cách thú vị hơn và dễ hiểu hơn. Nó được xây dựng trên Promises và tương thích với tất cả các Promise dựa trên API. Trong đó:
- **Async** - khai báo một hàm bất đồng bộ (async function someName(){...}).
    - Tự động biến đổi một hàm thông thường thành một Promise.
    - Khi gọi tới hàm async nó sẽ xử lý mọi thứ và được trả về kết quả trong hàm của nó.
    - Async cho phép sử dụng Await.
- **Await** - tạm dừng việc thực hiện các hàm async. (Var result = await someAsyncCall ().
    - Khi được đặt trước một Promise, nó sẽ đợi cho đến khi Promise kết thúc và trả về kết quả.
    - Await chỉ làm việc với Promises, nó không hoạt động với callbacks.
    - Await chỉ có thể được sử dụng bên trong các function async.

## Setup Cloud Functions Moralis in IDE

- Replacing keys

```bash
npm install -g moralis-admin-cli
mkdir cloud
moralis-admin-cli watch-cloud-folder --moralisApiKey XXXX --moralisApiSecret YYYY --moralisSubdomain XXX.usemoralis.com --autoSave 1 --moralisCloudfolder `pwd`
```

## Setup Ganache

- [https://www.trufflesuite.com/ganache](https://www.trufflesuite.com/ganache)
- Import secret key to metamask
- Add Network to Metamask
    - **Network Name**: Ganache
    - **New RPC URL**: http://localhost:7545
    - **Chain Id**: 1337
    - **Token:** ETH

## Deploy Smart Contract

- IDE - [https://remix.ethereum.org/](https://remix.ethereum.org/)
- Create a new contract ETH - [https://docs.moralis.io/guides/deploy-and-track-erc20-events#deploy-smart-contract](https://docs.moralis.io/guides/deploy-and-track-erc20-events#deploy-smart-contract)
- Create ERC20.sol
    
    ```bash
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.0;
    import "github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/presets/ERC20PresetMinterPauser.sol";
    ```
    
- Deploy new symbol contract
    - Mode: Injected web3
    - Contract: ERC20PresetMinterPauser
    - Contract: name MORALIS, symbol MOR
- Mint:
    - 1000 wei = 1000 * 10^18 = 1000 0000 0000 0000 0000 00
    - account: address of minter (owner). Create a balance for this user
- Add contract address to Metamask

## Connecting Moralis to Your Local Ganache Instance

- Open local port
- Downloading: [https://github.com/fatedier/frp/releases](https://github.com/fatedier/frp/releases)
- Create alias binary: `ln -s $HOME/tools/frp_0.38.0_darwin_amd64/frpc.ini $HOME/.local/bin/frpc`
- Create frpc.ini following the guideline on Moralis server
    
    ```bash
    [common]
      server_addr = XXXX.usemoralis.com
      server_port = 7000
      token = YYYY
    [ganache]
      type = http
      local_port = 7545
      custom_domains = XXXX.usemoralis.com
    ```
    
- Run: `frpc -c frpc.ini`
- F5 page admin
- [https://docs.moralis.io/guides/deploy-and-track-erc20-events#connecting-moralis-to-your-local-ganache-instance](https://docs.moralis.io/guides/deploy-and-track-erc20-events#connecting-moralis-to-your-local-ganache-instance)

## Syncing and Watching Contract Events From Moralis

- [https://docs.moralis.io/guides/deploy-and-track-erc20-events#syncing-and-watching-contract-events-from-moralis](https://docs.moralis.io/guides/deploy-and-track-erc20-events#syncing-and-watching-contract-events-from-moralis)
- **"description" -** Enter "Sync MOR Transfer Events". It's a small description for us to keep track of all the plugins we add to our instance.
- **"topic" -** We use "***Transfer(address,address,uint256)",*** but you can also use the sha3 topic "**0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef**".
- abi: abi of Transfer function, get it in Remix → compiler
- address: of contract
- **"tableName" -** "***MORTransferEvent**",* it's the name of the table that will be created in our database with all the events.

---

## References

1. [https://docs.moralis.io/](https://docs.moralis.io/)  

2. [https://hackernoon.com/getting-started-as-an-ethereum-web-developer-9a2a4ab47baf](https://hackernoon.com/getting-started-as-an-ethereum-web-developer-9a2a4ab47baf)  

3. [https://github.com/ChainSafe/web3.js](https://github.com/ChainSafe/web3.js)  

4. [https://courses.blockgeeks.com/course/blockgeeks-basic-solidity-course/](https://courses.blockgeeks.com/course/blockgeeks-basic-solidity-course/)  

5. Moralis Youtube - [https://www.youtube.com/channel/UCgWS9Q3P5AxCWyQLT2kQhBw](https://www.youtube.com/channel/UCgWS9Q3P5AxCWyQLT2kQhBw)  
