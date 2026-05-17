# Guia Completo: Registro e Autorização de App no Trello com Python

## Descrição do Projeto

Este projeto foi desenvolvido como parte de um desafio da DIO, com o objetivo de entender como registrar, autorizar e utilizar um aplicativo no Trello por meio da API, usando Python.

A proposta é simular uma integração real entre uma aplicação Python e o Trello, permitindo que o sistema acesse boards, listas e cards de forma automatizada.

## Objetivo

O objetivo principal deste desafio é aprender o processo de autenticação e autorização no Trello, utilizando:

- API Key;
- Token de acesso;
- Biblioteca `py-trello`;
- Arquivo `.env` para proteger credenciais;
- Python para integração com a API do Trello.

## Tecnologias Utilizadas

- Python
- Trello API
- py-trello
- python-dotenv
- Google ADK
- Git e GitHub

## Etapas Realizadas

### 1. Criação do Power-Up no Trello

Primeiro, acessei o portal de Power-Ups do Trello:

```text
https://trello.com/power-ups/admin/
```

Nesse portal, criei um novo Power-Up para poder gerar as credenciais necessárias para acessar a API do Trello.

### 2. Obtenção da API Key

Após criar o Power-Up, acessei a área de gerenciamento do aplicativo e copiei a API Key gerada pelo Trello.

Essa chave é necessária para identificar a aplicação nas requisições feitas para a API.

### 3. Geração do Token de Acesso

Com a API Key em mãos, utilizei a URL de autorização do Trello para gerar um Token de acesso:

```text
https://trello.com/1/authorize?expiration=never&name=AppDio&scope=read,write&response_type=token&key=SUA_API_KEY_AQUI
```

Depois de acessar o link, autorizei o aplicativo e copiei o token gerado.

### 4. Configuração do Arquivo `.env`

Para manter as credenciais protegidas, criei um arquivo `.env` com as seguintes variáveis:

```env
TRELLO_API_KEY=sua_api_key
TRELLO_API_SECRET=seu_api_secret
TRELLO_TOKEN=seu_token
TRELLO_BOARD_ID=id_do_board
```

O arquivo `.env` não deve ser enviado para o GitHub, pois contém dados sensíveis como chave da API e token de acesso.

### 5. Configuração do `.gitignore`

Para evitar o envio de informações sensíveis para o GitHub, adicionei o arquivo `.env` ao `.gitignore`.

Exemplo:

```text
.env
```

Dessa forma, as credenciais ficam protegidas localmente no computador.

### 6. Instalação das Dependências

As principais bibliotecas utilizadas no projeto foram:

```bash
pip install py-trello python-dotenv
```

A biblioteca `py-trello` permite a comunicação com a API do Trello, enquanto a `python-dotenv` permite carregar as variáveis salvas no arquivo `.env`.

### 7. Integração com Python

No código Python, utilizei a biblioteca `py-trello` para conectar com minha conta do Trello, acessar o board e manipular listas e cards.

Exemplo básico de conexão:

```python
from trello import TrelloClient
from dotenv import load_dotenv
import os

load_dotenv()

client = TrelloClient(
    api_key=os.getenv("TRELLO_API_KEY"),
    api_secret=os.getenv("TRELLO_API_SECRET"),
    token=os.getenv("TRELLO_TOKEN")
)
```

### 8. Uso do Board ID

Para acessar um quadro específico do Trello, utilizei o ID do board salvo no arquivo `.env`.

Exemplo:

```python
BOARD_ID = os.getenv("TRELLO_BOARD_ID")
meu_board = client.get_board(BOARD_ID)
```

Isso evita depender apenas do nome do quadro, deixando a integração mais segura e organizada.

## Funcionalidades Desenvolvidas

Durante o desenvolvimento, foram trabalhadas funções para:

- Criar tarefas no Trello;
- Listar tarefas existentes;
- Consultar listas do board;
- Mudar o status de uma tarefa entre listas;
- Utilizar variáveis de ambiente para proteger credenciais.

## Exemplo de Criação de Card

Um exemplo simples de criação de card no Trello:

```python
listas = meu_board.list_lists()

lista_tarefas = [l for l in listas if l.name.upper() == "A FAZER" or l.name.upper() == "TO DO"][0]

lista_tarefas.add_card(
    name="Estudar API",
    desc="Revisar conceitos de GET, POST e JSON"
)
```

Esse exemplo cria um card em uma lista chamada `A Fazer` ou `To Do`.

## Cuidados com Segurança

Durante o projeto, alguns cuidados importantes foram considerados:

- Não expor API Key ou Token no GitHub;
- Utilizar arquivo `.env` para armazenar credenciais;
- Adicionar `.env` ao `.gitignore`;
- Nunca compartilhar prints contendo tokens ou chaves de API;
- Usar variáveis de ambiente no código.

## Dificuldades Encontradas

Durante o desenvolvimento, encontrei algumas dificuldades comuns em integrações com APIs, como:

- Entender a diferença entre API Key e Token;
- Descobrir o ID correto do board;
- Trabalhar com listas e cards no Trello;
- Corrigir erros de data inválida ao criar cards;
- Entender melhor o uso de variáveis de ambiente.

Essas dificuldades ajudaram no aprendizado, principalmente sobre integração entre sistemas e segurança de credenciais.

## Aprendizados

Com este desafio, aprendi melhor como funciona a autenticação com a API do Trello, como usar variáveis de ambiente em Python e como estruturar uma integração simples entre uma aplicação Python e uma ferramenta externa.

Também entendi a importância de organizar bem o README, pois ele ajuda outras pessoas a compreenderem o objetivo, as tecnologias e o funcionamento do projeto.

## Conclusão

Este desafio foi importante para praticar conceitos de API, autenticação, automação e integração com ferramentas externas.

A integração com o Trello mostrou como é possível usar Python para automatizar tarefas do dia a dia, como criar cards, listar tarefas e organizar informações em um board.

## Autor

Carlos Eduardo

Projeto desenvolvido como parte do desafio da DIO.
