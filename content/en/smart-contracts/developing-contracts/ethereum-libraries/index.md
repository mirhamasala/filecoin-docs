---
title: "Solidity libraries"
lead: "A _Solidity library_ is a Solidity contract that provides reusable, standardized building blocks that developers can use to quickly build custom smart contracts. With Filecoin Virtual Machine (FVM), Solidity developers can use existing libraries listed on this page in their FVM smart contracts."
description: "Learn how to use existing Solidity libraries with FVM projects."
draft: false
images: []
type: docs
menu:
  smart-contracts:
    parent: "smart-contracts-developing-contracts"
    identifier: "integrating-existing-ethereum-libraries-e0b2c827da6ced7e92bfaf452add675c"
weight: 430
toc: true
---

## OpenZeppelin

[OpenZeppelin](https://www.openzeppelin.com/contracts) provides a library of battle-tested smart contract templates, including widely used [implementations of ERC token standards](https://docs.openzeppelin.com/contracts/2.x/tokens#standards). For a guided example that implements an ERC20 token on the Filecoin network, see [Example using an ERC20 contract](#example-using-an-erc20-contract).

Learn more about OpenZepplin with the following resources:

- [OpenZeppelin Contracts website](https://www.openzeppelin.com/contracts)
- [Documentation](https://docs.openzeppelin.com/contracts/4.x/)
- [GitHub](https://github.com/OpenZeppelin/openzeppelin-contracts)

### Using OpenZeppelin with FVM

The _general_ procedure for using OpenZeppelin with FVM is as follows:

1. Install OpenZeppelin. For example, using `npm`:

   ```bash
   npm install @openzeppelin/contracts
   ```

1. Import the specific library you want to use.
1. In your smart contract, inherit the library.

Thanks to the FVM, your contract can be integrated and deployed on the Filecoin network with OpenZepplin inheritance. For a guided example that implements an ERC20 token on the Filecoin network, see [Example using an ERC20 contract](#example-using-an-erc20-contract).

### Example using an ERC20 contract

In the following tutorial, you'll write and deploy a smart contract that implements the [ERC20](https://docs.openzeppelin.com/contracts/4.x/erc20) on the Hyperspace testnet using Remix and MetaMask:

#### Prerequisites

Before starting the procedure, ensure that you have:

- [Remix](https://remix.ethereum.org).
- [MetaMask](https://metamask.io/).
- [MetaMask connected to the Hyperspace testnet]({{< relref "/basics/assets/metamask-setup" >}}).
- Test tokens (tFIL) [from the faucet]({{< relref "/networks/hyperspace/get-test-tokens">}}).

#### Procedure

In this procedure, you will create, deploy, mint and send an [ERC20](https://docs.openzeppelin.com/contracts/4.x/erc20) token on Hyperspace using Remix and MetaMask. 

1. Navigate to [remix.ethereum.org](https://remix.ethereum.org/).

1. Next to **Workspaces**, click the **+** icon to create a new workspace.

1. In the dropdown:
   - Set **Choose a template** to **ERC 20**.
   - Under **Features**, select **Mintable**.
   - In **Workspace name**, enter a name or keep the default.
   - Leave all other settings on default.

1. Click **OK**. 

   {{< alert >}}
   **Checkpoint**

   A new workspace and an ERC20 token called `MyToken.sol` have been created. You can view the workspace and its contents in the Remix menu.
   {{< /alert >}}

1. In the **contracts** directory in the menu, click `MyToken.sol`.

1. The `MyToken.sol` code should look similar to the following:

   ```solidity
   // SPDX-License-Identifier: MIT
   pragma solidity ^0.8.9;

   import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
   import "@openzeppelin/contracts/access/Ownable.sol";

   contract MyToken is ERC20, Ownable {
      constructor() ERC20("MyToken", "MTK") {}

      function mint(address to, uint256 amount) public onlyOwner {
         _mint(to, amount);
      }
   }
   ```

1. At the top of the workspace, click the green play symbol to compile the contract. Once the contract compiles, an `artifacts` folder is generated in the workspace directory.

1. Open the the **Deploy & run transactions** tab on the left.

1. In the tab **Environment** dropdown, select **Injected Provider - MetaMask**. <!--ISSUE I see a "Injected Provider - Brave" option but not Metamask !-->

1. In the MetaMask popup window, select **Confirmed connection**.

   ![Select contract in Remix.](deploy-select-contract.png)

1. Click **Deploy**.

1. In MetaMask, confirm the transaction. 

   {{< alert >}}
   **Checkpoint**

   After the transaction is confirmed on-chain, your token contract is deployed to the Hyperspace network. Now, you can mint tokens.
   {{< /alert >}}

1. In Remix, open the **Deployed Contracts** dropdown. 

1. In the `mint` method, set:
   -  `to` to your wallet address.
   -  `amount` to `100000000000000000000` (1 `FIL`).

   ![Click Deploy in Remix.](deploy-remix-deploy.png)

1. Click **Transact**.

1. In MetaMask, confirm the transaction. 

Once the network processes the transaction, the token is minted and sent to your network address. Congratulations, you've completed the tutorial!

## DappSys

The DappSys library provides safe, simple, and flexible Ethereum contract building blocks for common Ethereum and Solidity use cases.

- [Documentation](https://dappsys.readthedocs.io/en/latest/)
- [GitHub](https://github.com/dapphub/dappsys)

## 0x protocol

 The 0x protocol library provides a set of secure smart contracts that facilitate peer-to-peer exchange of Ethereum-based assets.

- [Documentation](https://docs.0x.org/introduction/introduction-to-0x)
- [GitHub](https://github.com/0xProject)
