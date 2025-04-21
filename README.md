# aptos-smart_contract

## Description
This project implements a simple voting system on the Aptos blockchain using Move. It allows users to create polls with multiple options and cast votes securely. The contract ensures that each voter can only vote once per poll and that voting is only allowed while the poll is active.

## Features
- Create a voting poll with multiple options.
- Cast votes for a specific option in a poll.
- Prevent duplicate voting by the same user.
- Ensure voting is only allowed while the poll is active.

## Prerequisites
- Aptos CLI installed on your system.
- An Aptos account with testnet tokens.
- Move language tools for development.

## Setup
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd aptos-proj
   ```

2. Compile the Move modules:
   ```bash
   aptos move compile
   ```

3. Publish the module to the Aptos blockchain:
   ```bash
   aptos move publish --profile testnet
   ```

## Usage
1. **Create a Poll**  
   Use the `create_poll` function to create a new voting poll. Provide the options as a vector of strings.

2. **Cast a Vote**  
   Use the `vote` function to cast a vote for a specific option in a poll. Provide the poll creator's address and the index of the option you want to vote for.

3. **Example Commands**  
   - Create a poll:
     ```bash
     aptos move run --function-id 0xc65df22fe8951577e17c07bd2f87193accf91f501055287e9bdbcaecccf35d17::SimpleVoting::create_poll --args <options>
     ```
   - Vote in a poll:
     ```bash
     aptos move run --function-id 0xc65df22fe8951577e17c07bd2f87193accf91f501055287e9bdbcaecccf35d17::SimpleVoting::vote --args <poll_creator_address> <option_index>
     ```

## Contract Details
### Module Address
`0xc65df22fe8951577e17c07bd2f87193accf91f501055287e9bdbcaecccf35d17`

### Functions
- **create_poll**  
  Creates a new voting poll with the specified options.  
  **Parameters:**  
  - `creator`: The signer of the transaction.  
  - `options`: A vector of options (as byte arrays) for the poll.

- **vote**  
  Casts a vote for a specific option in the poll.  
  **Parameters:**  
  - `voter`: The signer of the transaction.  
  - `poll_creator`: The address of the poll creator.  
  - `option_index`: The index of the option to vote for.

### Error Codes
- `E_ALREADY_VOTED (1)`: The voter has already voted in this poll.
- `E_VOTING_CLOSED (2)`: The poll is no longer active.

### Structures
- **VotingPoll**  
  Stores the details of a voting poll.  
  **Fields:**  
  - `creator`: The address of the poll creator.  
  - `options`: A vector of options for the poll.  
  - `votes`: A vector of vote counts for each option.  
  - `voters`: A vector of addresses of users who have voted.  
  - `is_active`: A boolean indicating if the poll is active.

## License
This project is licensed under the MIT License.