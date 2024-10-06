## Português Brasil

# BetCandidate

Este projeto é uma aplicação de apostas on-chain, focada nas eleições presidenciais dos Estados Unidos. Utiliza a biblioteca Web3 para integrar carteiras digitais como MetaMask para transações de apostas. Este README explica detalhadamente o funcionamento do código e a interação com contratos inteligentes em Solidity.

## Objetivo do Projeto

O projeto permite que usuários façam apostas em um dos candidatos das eleições americanas, utilizando a criptomoeda POL. Após a conclusão da eleição, os vencedores podem reivindicar seus prêmios de forma descentralizada.

## Tecnologias Utilizadas

- **Next.js**: Framework para React, utilizado na criação da interface da aplicação.
- **Web3.js**: Biblioteca para comunicação com a blockchain Ethereum.
- **Solidity**: Linguagem para desenvolvimento de contratos inteligentes.

## Estrutura do Código

### 1. Arquivo `pages/index.js` (Página de Login)

#### Objetivo

A página inicial da aplicação serve como ponto de autenticação do usuário com a carteira MetaMask. O usuário deve estar autenticado para acessar as funcionalidades de apostas.

#### Componentes Importados

- `Head`: Componente do Next.js para manipulação de `<head>`.
- `useRouter`: Utilizado para navegação entre páginas.
- `useState`: Gerenciamento do estado local do componente.
- `doLogin`: Função do Web3Service para autenticar a carteira MetaMask.

#### Explicação do Código

- `useRouter()`: Captura o método `push` para navegação entre as rotas.
- `btnLoginClick()`: Função que conecta a carteira do usuário. Define a mensagem de feedback ao usuário e, caso a autenticação seja bem-sucedida, redireciona para a página de apostas (`/bet`).

#### Interface do Usuário

- Uma imagem relacionada às eleições e um botão para conectar a carteira MetaMask.
- Mensagens de feedback são exibidas na interface conforme a interação do usuário.

### 2. Arquivo `pages/bet.js` (Página de Apostas)

#### Objetivo

Permitir que os usuários façam apostas em um dos candidatos ou reivindiquem o prêmio após o final da eleição.

#### Componentes Importados

- `useEffect`: Para executar ações ao carregar a página.
- `getDispute`, `placeBet`, `claimPrize`: Funções do Web3Service para obter dados, fazer apostas e reivindicar prêmios.

#### Lógica Principal

- `useEffect()`: Ao carregar a página, verifica se há uma carteira conectada. Caso contrário, redireciona para a página de login.
- `processBet(candidate)`: Realiza uma aposta no candidato selecionado. Solicita a quantia a ser apostada e chama a função `placeBet()`.
- `btnClaimClick()`: Solicita o prêmio caso o usuário tenha apostado no vencedor.

#### Interface do Usuário

- Exibição dos candidatos e botões para apostar ou reivindicar o prêmio.
- Mostra a quantidade total de apostas feitas em cada candidato.

### 3. Arquivo `services/Web3Service.js` (Serviço de Web3)

#### Objetivo

Fornecer funções de interação com a blockchain, como autenticação e manipulação de apostas.

#### Funções

- `doLogin()`: Conecta o usuário à carteira MetaMask e armazena o endereço da carteira no `localStorage`.
- `getContract()`: Cria uma instância do contrato inteligente.
- `getDispute()`: Obtém os detalhes da disputa atual.
- `placeBet(candidate, amountInEth)`: Realiza uma aposta no candidato especificado.
- `finishDispute(winner)`: Finaliza a disputa e determina o vencedor.
- `claimPrize()`: Reivindica o prêmio para o usuário.

### 4. Arquivo `contracts/BetCandidate.sol` (Contrato Inteligente)

#### Objetivo

Gerenciar apostas e prêmios em uma disputa entre candidatos.

#### Estruturas

- `Bet`: Estrutura que armazena informações sobre cada aposta.
- `Dispute`: Estrutura que armazena informações sobre a disputa, como candidatos e totais apostados.

#### Funções

- `bet(uint candidate)`: Permite que um usuário aposte em um dos candidatos, desde que a disputa esteja aberta.
- `finish(uint winner)`: Fecha a disputa e define o vencedor. Calcula a comissão do proprietário do contrato e o valor do prêmio.
- `claim()`: Permite que um vencedor reivindique seu prêmio, calculando a proporção de sua aposta em relação ao total apostado.

## Como Executar o Projeto

### Pré-requisitos

- Node.js e npm instalados.
- Carteira MetaMask instalada no navegador.
- Rede Ethereum configurada no MetaMask (pode ser uma rede de testes).

### Passos para Executar

1. Clone este repositório:
   ```sh
   git clone <URL_DO_REPOSITÓRIO>
   cd <NOME_DO_DIRETÓRIO>
   ```

### ===========================================================================================================================

## English

# BetCandidate

This project is an on-chain betting application focused on the U.S. presidential elections. It uses the Web3 library to integrate digital wallets like MetaMask for bet transactions. This README explains the functionality of the code and the interaction with smart contracts written in Solidity.

## Project Objective

The project allows users to bet on one of the candidates in the U.S. elections, using the POL cryptocurrency. After the election concludes, winners can claim their prizes in a decentralized manner.

## Technologies Used

- **Next.js**: A framework for React, used for creating the application's interface.
- **Web3.js**: A library for communicating with the Ethereum blockchain.
- **Solidity**: A language for developing smart contracts.

## Code Structure

### 1. File `pages/index.js` (Login Page)

#### Objective

The application's homepage serves as the authentication point for the user using the MetaMask wallet. The user must be authenticated to access the betting features.

#### Imported Components

- `Head`: A Next.js component for `<head>` manipulation.
- `useRouter`: Used for navigation between pages.
- `useState`: Manages local state of the component.
- `doLogin`: Function from `Web3Service` to authenticate the MetaMask wallet.

#### Code Explanation

- `useRouter()`: Captures the `push` method for route navigation.
- `btnLoginClick()`: Function that connects the user's wallet. It sets feedback messages for the user, and upon successful authentication, redirects to the betting page (`/bet`).

#### User Interface

- An election-related image and a button to connect the MetaMask wallet.
- Feedback messages are displayed as the user interacts with the interface.

### 2. File `pages/bet.js` (Betting Page)

#### Objective

Allows users to bet on one of the candidates or claim their prize after the election concludes.

#### Imported Components

- `useEffect`: To perform actions when the page loads.
- `getDispute`, `placeBet`, `claimPrize`: Functions from `Web3Service` to get dispute data, place bets, and claim prizes.

#### Main Logic

- `useEffect()`: On page load, checks if a wallet is connected. If not, redirects to the login page.
- `processBet(candidate)`: Places a bet on the selected candidate. Requests the amount to be bet and calls the `placeBet()` function.
- `btnClaimClick()`: Requests the prize if the user has bet on the winner.

#### User Interface

- Displays the candidates and buttons to place bets or claim prizes.
- Shows the total amount bet on each candidate.

### 3. File `services/Web3Service.js` (Web3 Service)

#### Objective

Provides functions for interacting with the blockchain, such as authentication and managing bets.

#### Functions

- `doLogin()`: Connects the user to the MetaMask wallet and stores the wallet address in `localStorage`.
- `getContract()`: Creates an instance of the smart contract.
- `getDispute()`: Gets details of the current dispute.
- `placeBet(candidate, amountInEth)`: Places a bet on the specified candidate.
- `finishDispute(winner)`: Finishes the dispute and determines the winner.
- `claimPrize()`: Allows the user to claim their prize.

### 4. File `contracts/BetCandidate.sol` (Smart Contract)

#### Objective

Manages bets and prizes in a dispute between candidates.

#### Structures

- `Bet`: Structure that stores information about each bet.
- `Dispute`: Structure that stores information about the dispute, such as candidates and total bets.

#### Functions

- `bet(uint candidate)`: Allows a user to bet on one of the candidates while the dispute is open.
- `finish(uint winner)`: Closes the dispute and sets the winner. Calculates the commission for the contract owner and the prize value.
- `claim()`: Allows a winner to claim their prize, calculating the proportion of their bet relative to the total amount bet.

## How to Run the Project

### Prerequisites

- Node.js and npm installed.
- MetaMask wallet installed in the browser.
- Ethereum network configured in MetaMask (it can be a test network).

### Steps to Run

1. Clone this repository:
   ```sh
   git clone <REPOSITORY_URL>
   cd <DIRECTORY_NAME>
   ```
