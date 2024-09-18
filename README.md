# VotingSystem Smart Contract

## Overview

The `VotingSystem` contract is a decentralized voting system built on Ethereum using Solidity. It uses a token-based system where users vote for candidates by transferring tokens to their chosen candidate. The owner of the contract can mint and burn tokens, manage the list of candidates, and control the voting periods. This contract uses the ERC-20 standard-like mechanism for minting and transferring tokens but is customized for a voting scenario.

## Features

1. **Token Management**: 
   - The contract allows the owner to mint and burn tokens.
   - Each user has a balance of tokens they can use to vote.

2. **Voting Process**:
   - The owner can start and end the voting period.
   - Users can vote for a candidate by sending tokens to their preferred candidate.
   - Voting is only allowed within a specified time frame.

3. **Candidates**:
   - The owner can add candidates before voting begins.
   - Users can only vote for valid candidates.

4. **Event-driven**: 
   - The contract emits events for key activities such as minting tokens, burning tokens, casting votes, and adding candidates.

## Contract Details

### Variables

- `name`: The name of the token used for voting (VotingToken).
- `totalSupply`: The total number of tokens in circulation.
- `owner`: The address of the contract owner.
- `votingStartTime` & `votingEndTime`: The time period during which voting is active.
- `votingEnded`: Boolean flag to determine whether the voting has ended.
- `balances`: A mapping that holds the token balance for each address.
- `candidateVotes`: A mapping that holds the total votes for each candidate.
- `candidates`: An array that holds the list of candidate addresses.

### Events

- `TokensMinted`: Emitted when the owner mints new tokens.
- `TokensBurned`: Emitted when the owner burns tokens.
- `Voted`: Emitted when a user casts a vote for a candidate.
- `CandidateAdded`: Emitted when a new candidate is added to the list.
- `VotingStarted`: Emitted when the voting period begins.
- `VotingEnded`: Emitted when the voting period ends.

## Functions

### Constructor

```solidity
constructor(uint _initialSupply)
```

Initializes the contract with the owner as the contract deployer and sets an initial supply of tokens.

### Modifiers

- `onlyOwner`: Ensures that only the owner can call specific functions.
- `onlyDuringVoting`: Ensures that a function can only be executed during the voting period.
- `onlyAfterVoting`: Ensures that a function can only be executed after the voting has ended.

### Token Management

- `mintTokens(address _address, uint _value)`: Mints new tokens to a specified address.
- `burnTokens(address _address, uint _value)`: Burns tokens from a specified address.

### Voting

- `addCandidate(address _candidate)`: Adds a new candidate.
- `startVoting(uint _duration)`: Starts the voting process for a specified duration.
- `endVoting()`: Ends the voting process.
- `vote(address _candidate, uint _amount)`: Allows a user to vote by transferring a specified amount of tokens to a candidate.

### Getters

- `getCandidates()`: Returns the list of candidates.
- `getVotes(address _candidate)`: Returns the number of votes a candidate has received.
- `isCandidate(address _candidate)`: Internal function to check if an address is a valid candidate.

## Example Usage

1. **Deploy the Contract**:
   - Deploy the `VotingSystem` contract by specifying an initial token supply.

2. **Mint Tokens**:
   - The contract owner can mint tokens to themselves or other users by calling the `mintTokens` function.

3. **Add Candidates**:
   - The owner can add candidates by calling the `addCandidate` function.

4. **Start Voting**:
   - The owner can start the voting period by calling the `startVoting` function and specifying the duration of the voting period.

5. **Cast Votes**:
   - Users with tokens can vote by calling the `vote` function and specifying the candidate's address and the number of tokens to vote with.

6. **End Voting**:
   - Once the voting period is over, the owner can call the `endVoting` function.

7. **Check Results**:
   - Anyone can check the votes for each candidate using the `getVotes` function.

## Requirements

- **Solidity Version**: `^0.8.9`
- **Ethereum Environment**: Requires an Ethereum network to deploy and interact with the contract (e.g., Ganache, Rinkeby, or Mainnet).

## How to Deploy

1. Open a Solidity development environment (e.g., Remix, Hardhat).
2. Copy the contract code into the editor.
3. Deploy the contract by providing the initial supply of tokens as a constructor argument.

Example:

```solidity
constructor(1000) // Initial supply of 1000 tokens
```

4. After deployment, use the available functions to interact with the contract.

## License

This project is licensed under the MIT License.
