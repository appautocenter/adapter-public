## 📃 Sobre

Este repositório contém informações sobre uma integração do Autocenter App com bancos de dados utilizando views para acessar e manipular apenas os dados de interesse. Esta integração foi desenvolvida para facilitar a interação entre o Autocenter App e os sistemas de banco de dados, permitindo um acesso mais eficiente e seguro às informações relevantes.


## ⚛️ Tecnologia

Este projeto foi desenvolvido com as seguintes tecnologias:

- Node.js: Um ambiente de execução JavaScript que permite executar código JavaScript do lado do servidor.
- TypeScript: Um superconjunto de JavaScript que adiciona tipagem estática opcional ao JavaScript.

## 🎲 BD's Suportados

- SQL Server
- DBF

Obs: Caso o seu sistema de banco de dados não esteja entre os suportados entre em contato para homologação do novo banco de dados (prazo de 5 dias).

## 🚀Funcionamento

"O Autocenter App é uma aplicação Node.js (v18+) projetada para ser instalada na máquina local do cliente, onde os dados estarão disponíveis. No caso de disponibilização das views na web, o serviço pode operar na nuvem, proporcionando flexibilidade e acessibilidade aos usuários."

Obs: Caso ja exista o node instalado na maquina para o funcionamento de outra aplicação entrar em contato para avaliar compatibilidade.

## 🔐 Configuração do Arquivo `.env`

O Autocenter utiliza um arquivo `.env` para armazenar informações sensíveis, como conexões com o BD, e outros dados confidenciais. Abaixo estão os campos necessários no arquivo `.env` e como configurá-los:

```dotenv
# PORTA RESERVADA PARA A APLICAÇÃO (PADRÃO 3000)
PORT_APP=

# TOKEN FORNECIDO PELA AUTOCENTER
TOKEN=

# INFORMAÇÕES DE CONEXÃO COM O BANCO DE DADOS
## 'sqlserver' | 'mysql' | 'postgresql';
BD=
USER=
PASSWORD=
SERVER=
DATABASE=
PORT_DB=
SSL= ##padrão false

# ATIVAR COMBUSTIVEL TRUE OU FALSE (PADRÃO É FALSE) - PARA POSTOS
FUEL=

# ATIVAR PRODUTOS TRUE OU FALSE (PADRÃO É FALSE)
PRODUCTS=

# ATIVAR ORDEM DE SERVIÇO TRUE OU FALSE (PADRÃO É FALSE)
ORDER_SERVICE=
```

Certifique-se de fornecer todos os dados para a conexão com o bd para o correto funcionamento da integração.

## 📊 Views do Banco de Dados

Nesta seção, descrevemos as views específicas que foram criadas no banco de dados para fornecer os dados necessários para a integração com o Autocenter App. As views são utilizadas para encapsular consultas complexas e fornecer uma interface simplificada para acessar os dados de interesse.

"É importante ressaltar que os nomes dos campos das views e das próprias views devem ser respeitados para garantir o correto funcionamento da integração com o Autocenter App."

### View: VW_AUTOCENTER_ORDEMDESERVICO

A view `VW_AUTOCENTER_ORDEMDESERVICO` é responsável por fornecer informações detalhadas sobre as ordens de serviço (OS) registradas no sistema. Ela inclui os seguintes campos:

- **ID:** Identificador único da ordem de serviço.
- **ID_OS:** Identificador que vincula os itens da ordem de serviço.
- **USERNAME:** Nome do usuário associado à ordem de serviço.
- **USERDOCUMENT:** Documento do usuário associado à ordem de serviço (necessário para vinculação com o aplicativo).
- **USERPHONE:** Número de telefone do usuário associado à ordem de serviço.
- **USERCELPHONE:** Número de celular do usuário associado à ordem de serviço.
- **PLATE:** Placa do veículo associado à ordem de serviço.
- **KM:** Quilometragem registrada no momento da ordem de serviço.
- **DATE:** Data de início da ordem de serviço.
- **FINISHDATE:** Data de finalização da ordem de serviço.
- **TOTAL:** Valor total da ordem de serviço.

Esta view é construída a partir das tabelas varias tabelas de acordo com o seu sistema.


### View: VW_AUTOCENTER_ITENSORDEMDESERVICO

A view `VW_AUTOCENTER_ITENSORDEMDESERVICO` é responsável por fornecer informações detalhadas sobre os itens relacionados às ordens de serviço registradas no sistema.

Ela inclui os seguintes campos:

- **ID:** Identificador único do item.
- **ID_PRODUTO:** Identificador do produto associado ao item.
- **ID_OS:** Identificador da ordem de serviço à qual o item está vinculado.
- **NAME:** Nome do produto.
- **DESCRIPTION:** Descrição do produto.
- **QUANTITY:** Quantidade do item.
- **TOTAL:** Valor total do item.
- **NCM:** Número comum do Mercosul associado ao produto.

Esta view é construída a partir das tabelas varias tabelas de acordo com o seu sistema.


### View: VW_AUTOCENTER_PRODUTOS

A view `VW_AUTOCENTER_PRODUTOS` é responsável por fornecer informações detalhadas sobre os produtos disponíveis no sistema. Esta view é construída a partir das seguintes tabelas:

1. **PRODUTOS (p):** Esta tabela contém informações sobre os produtos cadastrados no sistema, como nome, NCM, aplicação e outras características.
2. **ESTOQUE (e):** Esta tabela contém informações sobre o estoque de cada produto, incluindo a quantidade atual disponível.
3. **GRUPOPRODUTOS (g):** Esta tabela contém informações sobre os grupos de produtos, fornecendo uma descrição adicional para os produtos.

Ela inclui os seguintes campos:

- **ID:** Identificador único do produto.
- **NAME:** Nome do produto.
- **NCM:** Número comum do Mercosul associado ao produto.
- **APLICACAO:** Possíveis veículos onde o produto pode ser aplicado.
- **DESCRIPTION:** Descrição detalhada do produto, incluindo código do fabricante, grupo e outras informações relevantes.
- **AMOUNT:** Quantidade atual em estoque do produto.

Esta view é construída a partir das tabelas varias tabelas de acordo com o seu sistema. Devem ser excluidos da view produtos fora do interesse do setor automotivo.


### View: VW_AUTOCENTER_COMBUSTIVEL

A view `VW_AUTOCENTER_COMBUSTIVEL` é responsável por fornecer informações detalhadas sobre os produtos de combustível disponíveis no sistema e é EXCLUSIVO PARA POSTOS DE COMBUSTIVEL. Esta view é construída a partir das seguintes tabelas de exemplo:

1. **BICOS (B):** Esta tabela contém informações sobre os bicos de combustível associados aos tanques e o preço de venda.
2. **TANQUES (T):** Esta tabela contém informações sobre os tanques de combustível.
3. **PRODUTOS (P):** Esta tabela contém informações sobre os produtos cadastrados no sistema, incluindo os produtos de combustível.

Ela inclui os seguintes campos:

- **ID:** Identificador único do produto de combustível.
- **NAME:** Nome do produto de combustível.
- **PRICE:** Preço do combustível por litro.
- **NCM:** Número comum do Mercosul associado ao produto.
- **ACTIVED:** Indica se o produto de combustível está ativo ou não.

Obs: Em caso de repetição de combustiveis será conservado apenas o menor valor repassado.


## Considerações Finais

Nesta seção, gostaríamos de ressaltar alguns pontos importantes relacionados à integração com o Autocenter App e ao uso das views no banco de dados.

- **Respeito aos Nomes dos Campos e Views:** É crucial garantir que os nomes dos campos das views e das próprias views sejam respeitados conforme definido na documentação. Isso é essencial para garantir o correto funcionamento da integração com o Autocenter App e para evitar problemas de compatibilidade.

- **Segurança dos Dados:** Ao lidar com dados sensíveis, como informações de clientes ou transações comerciais, garantimos práticas de segurança adequadas, como criptografia e controle de acesso, para proteger a confidencialidade e a integridade dos dados.

- **Feedback e Aprimoramento:** Estamos sempre abertos a feedback e sugestões de aprimoramento para tornar a integração com o Autocenter App ainda mais eficiente e fácil de usar. Se você tiver alguma dúvida, problema ou sugestão, não hesite em entrar em contato conosco.

Obrigado por escolher nossa solução de integração com o Autocenter App. Esperamos que esta ferramenta seja útil para otimizar suas operações e melhorar sua experiência com o sistema.

