# BOOTCAMP-DIO-AI102

## Tradutor de Artigos com Azure OpenAI Foundry
Este projeto é um tradutor de artigos de blog que utiliza o modelo de linguagem do Azure OpenAI. Desenvolvido durante o bootcamp da DIO e Microsoft (Microsoft Certification Challenge AI-102), ele demonstra a extração de texto de uma URL, a tradução via API de chat completions e a manipulação dos resultados.

*O Bootcamp mostra o desafio utilizando o OpenAI Studio, porém não consegui ter acesso ao Studio no Azure, tendo como opção, a utilização do Foundry.

## Tecnologias Utilizadas
Python: Linguagem de programação.
requests: Biblioteca para fazer chamadas à API.
BeautifulSoup4: Biblioteca para extração de texto de HTML.
python-dotenv: Para gerenciar variáveis de ambiente de forma segura.
Azure OpenAI Foundry: Serviço de IA da Microsoft.

# A depuração revelou três problemas principais, que exigiram uma abordagem mais robusta para serem resolvidos.
1.	Incompatibilidade de Parâmetros da API (Erro 400) A versão da API (2025-01-01-preview) utilizada no Foundry não suportava os parâmetros max_tokens e top_p que eram aceitos em versões anteriores. A solução foi ajustar o payload da requisição, substituindo max_tokens por max_completion_tokens e removendo o parâmetro top_p.
2.	Limitação de Tamanho de Entrada O modelo não conseguia processar um artigo inteiro em uma única chamada de API, o que resultava em uma resposta vazia. A solução foi implementar a técnica de "chunking", que divide o texto do artigo em pequenos blocos de 800 caracteres antes de enviá-los para a API. Cada bloco é traduzido individualmente.
3.	Código Não Robusto O código inicial não tinha um tratamento de erro adequado. Quando uma tradução falhava (por limite de tokens ou outro motivo), ele simplesmente parava ou retornava uma string vazia. A solução foi refatorar a função de tradução para tratar erros de forma mais robusta, exibindo as mensagens detalhadas da API para ajudar na depuração.
Ao final, o código se tornou mais complexo, mas muito mais resiliente e confiável, capaz de traduzir textos longos e lidar com as peculiaridades do ambiente do Azure OpenAI Foundry.

# Utilizei um arquivo config.env com as informações do endpoint que precisamos utilizar no código:
Conteúdo:

AZURE_OPENAI_KEY=”Sua KEY do ENDPOINT”

AZURE_ENDPOINT=”URL do seu Ponto de Extremidade”

AZURE_DEPLOYMENT=”Versão da sua implantação/deployment” ex: o4-mini

AZURE_API_VERSION=”Versão da API” 2025-01-01-preview

## Implementação

https://github.com/mrbisao/BOOTCAMP-DIO-AI102/blob/main/Desafio-Tradutor/Desafio_Tradutor.ipynb
