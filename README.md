Hash Teste Back-end

Antes de começar, leia os nossos key values para entender um pouco sobre o que nós priorizamos no desenvolvimento e faça o seu melhor, pois iremos avaliar o teste como se fosse seu melhor esforço ;)

O teste consiste em escrever 2 microserviços que possibilitam retornar uma lista de produtos com desconto personalizado para cada usuário.

Envie o resultado do seu desafio para dev@hash.com.br (ele pode ser open source!). Em até uma semana marcaremos uma conversa com você após analisarmos seu desafio.

Restrições

Os serviços desse teste devem ser escritos usando linguagens distintas
Os serviços desse teste devem se comunicar via gRPC
Utilize docker para provisionar os serviços
Para facilitar, os serviços podem usar um banco de dados compartilhado
Avaliação

Conversaremos sobre a estrutura do código, escolha do banco, e outras decisões que foram tomadas
Discutiremos como esse sistema evoluiria ao longo do tempo
Considere que as regras de descontos irão mudar com o tempo
Considere que mais pessoas irão trabalhar junto com você nesse projeto
Serviço 1: Desconto invidual de produto

Este serviço recebe um id de produto e um id de usuário e retorna um desconto.
Produto exemplo:

{
    id: string
    price_in_cents: int
    title: string
    description: string
    discount: {
        pct: float
        value_in_cents: int
    }
}
Usuário exemplo:

{
    id: string
    first_name: string
    last_name: string
    date_of_birth: Date
}
As regras de descontos da aplicação são:
Se for aniversário do usuário, o produto terá 5% de desconto
Se for black friday (nesse exemplo ela pode ser fixada dia 25/11) o produto terá 10% de desconto
O desconto não pode passar de 10%
Serviço 2: Listagem de produtos

Expõe uma rota HTTP tal que GET /product retorne um json com uma lista de produtos.

Essa rota deve receber opcionalmente via header X-USER-ID um id de usuário.

Para obter o desconto personalizado este serviço deve utilizar o serviço 1.

Caso o serviço 1 retorne um erro, a lista de produtos ainda precisa ser retornada, porém com esse produto que deu erro sem desconto.

Se o serviço de desconto (1) cair, o serviço de lista (2) tem que continuar funcionando e retornando a lista normalmente, só não vai aplicar os descontos.

Executando

Para rodar o sistema, use:
docker-compose build
docker-compose up

Parando tudo

Para parar o sistema, use:

sudo docker-compose down

Usando

O serviço de produtos estará rodando no endereço 
http://localhost:8086/product

Já o serviço de usuários poderá ser usado no endereço
http://localhost:8080/swagger-ui.html