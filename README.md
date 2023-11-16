# Avalanche Subnets

This project provides an implementation of the ERC20 token standard and a Vault contract for interacting with ERC20 tokens.

## Description

This project implements the ERC20 token standard and a Vault contract in Solidity. The ERC20 Contract manages token supply, balances, allowances, and details, and handles Transfer and Approval events. The Vault Contract allows users to deposit ERC20 tokens and receive shares, which can be redeemed by burning. It manages share supply and balances, and includes functions for depositing and withdrawing tokens.

## Getting Started

### Creating EVM Subnet with Ava Labs

1. Install the Avalanche CLI tool: To get started, you will need to install the Avalanche Command Line Interface (CLI) tool. This tool is used to interact with the Avalanche network from your terminal. You can find installation instructions for the Avalanche CLI in the official documentation.
2. Create a new subnet: Once you have the Avalanche CLI installed, you can create a new subnet by running the command avalanche subnet create mySubnet in your terminal. This will create a new subnet with the name "mySubnet" on your local machine.
3.Select the EVM Subnet option and configure: When creating a new subnet, you will be prompted to select a subnet type. Choose the SubnetEVM option to create an EVM Subnet on your local machine and follow the steps in the image below:
```
avalanche subnet create mySubnet
Attempted to check if a new version is available, but couldn't find the currently running version information
Make sure to follow official instructions, or automatic updates won't be available for you
✔ Subnet-EVM
creating subnet mySubnet
Enter your subnet's ChainId. It can be any positive integer.
ChainId: 12345567
Select a symbol for your subnet's native token
Token symbol: MYSUBNET
✔ Use latest version
✔ Low disk use    / Low Throughput    1.5 mil gas/s (C-Chain's setting)
✔ Airdrop 1 million tokens to the default address (do not use in production)
✔ No
```
4. Deploy the subnet: After selecting the EVM Subnet option, you can deploy the subnet by running the command avalanche subnet deploy mySubnet and selecting to deploy your subnet on your local network. This will deploy your new EVM Subnet on your local machine.
5. View subnet details: Once your EVM Subnet is deployed, the console will display all the details about the subnet you just created. You can use this information to interact with the subnet and start building your smart-contract protocol.
### Executing program
To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g.,ERC20.sol). Copy and paste the following code into the file:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract ERC20 {
    uint public totalSupply;
    mapping(address => uint) public balanceOf;
    mapping(address => mapping(address => uint)) public allowance;
    string public name = "Solidity by Example";
    string public symbol = "SOLBYEX";
    uint8 public decimals = 18;

	event Transfer(address indexed from, address indexed to, uint value);
    event Approval(address indexed owner, address indexed spender, uint value);

    function transfer(address recipient, uint amount) external returns (bool) {
        balanceOf[msg.sender] -= amount;
        balanceOf[recipient] += amount;
        emit Transfer(msg.sender, recipient, amount);
        return true;
    }

    function approve(address spender, uint amount) external returns (bool) {
        allowance[msg.sender][spender] = amount;
        emit Approval(msg.sender, spender, amount);
        return true;
    }

    function transferFrom(
        address sender,
        address recipient,
        uint amount
    ) external returns (bool) {
        allowance[sender][msg.sender] -= amount;
        balanceOf[sender] -= amount;
        balanceOf[recipient] += amount;
        emit Transfer(sender, recipient, amount);
        return true;
    }

    function mint(uint amount) external {
        balanceOf[msg.sender] += amount;
        totalSupply += amount;
        emit Transfer(address(0), msg.sender, amount);
    }

    function burn(uint amount) external {
        balanceOf[msg.sender] -= amount;
        totalSupply -= amount;
        emit Transfer(msg.sender, address(0), amount);
    }
}

interface IERC20 {
    function totalSupply() external view returns (uint);

    function balanceOf(address account) external view returns (uint);

    function transfer(address recipient, uint amount) external returns (bool);

    function allowance(address owner, address spender) external view returns (uint);

    function approve(address spender, uint amount) external returns (bool);

    function transferFrom(
        address sender,
        address recipient,
        uint amount
    ) external returns (bool);

    event Transfer(address indexed from, address indexed to, uint value);
    event Approval(address indexed owner, address indexed spender, uint value);
}
```

## Authors
Marl Shane G. Esteron
