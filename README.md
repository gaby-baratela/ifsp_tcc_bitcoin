# Previsão de Preço de Fechamento do Bitcoin
### TCC - 1S/2024

## Aluna:
- Gabrielly Baratela de Carvalho (CP3016331)

# Sumário:
1. [Motivação](#ancora1)
2. [Definição do Problema e Infraestrutura](#ancora2)
3. [Coleta de dados](#ancora3)
4. [Análise exploratória](#ancora4)
5. [Modelagem](#ancora5)
6. [Discussão de Resultados e Melhorias](#ancora6)

### 1. Motivação<a id="ancora1"></a>

As criptomoedas são moedas digitais que vêm a cada dia mais consolidando sua posição no mercado, tendo atualmente **mais de 843 bilhões de dólares investidos** (4,5 trilhões de reais), e mais de 20 mil diferentes opções de criptomoedas no mercado mundial. Elas podem vir a substituir, mesmo que parcialmente, o que consideramos como "dinheiro" atualmente, servindo como reserva de valor - preservando o patrimônio e o poder de compra do indivíduo; meio de troca - facilitando as transações comerciais e com redução de taxas; unidade de conta - parâmetro para precificação de produtos. 

O surgimento e a ascensão das moedas digitais se deu devido ao desejo de privacidade dos dados transacionais e a descentralização de informações, através do **blockchain**. No Blockchain múltiplos servidores armazenam registros particionados das transações, garantindo maior segurança e privacidade dos dados.

A **Bitcoin** é a principal criptomoeda, e vem sendo cada dia mais reconhecida mundialmente, aparecendo em manchetes de vários jornais, por já vir sendo utilizada como forma de pagamento por algumas empresas e até para salários de jogadores de futebol. Seu crescimento maior aconteceu principalmente após 2017, 9 anos após seu lançamento, e fatos relevantes serão estudados na análise exploratória, para entendimento de eventos que podem ter impactado a série.

Dada a importância desse mercado na economia atual, a motivação do estudo é entender como se comporta o preço do Bitcoin ao longo do tempo e se é possível realizar sua predição, para que haja maior confiança na aquisição das moedas e diminuição do risco de prejuízo.

### 2. Definição do problema e Infraestrutura<a id="ancora2"></a>

- **Objetivo:** Previsão do preço de fechamento ajustado do bitcoin nos próximos 5 dias
- **Periodicidade**: Diária

##### **Setup de infraestrutura:**

- Workflow de arquitetura [(Ilustração)](https://github.com/gaby-baratela/ifsp_s2_bitcoin/blob/cbe47e342c3c7ab67e5d9629c3a7add43ae20f2e/Imagens/Infraestrutura.png)
- Configurações de ambiente:
    - Permissões/roles: no ambiente learner lab não é possível configurar permissões e usuários, portanto foi utilizada a credencial padrão de aluno.
    - Sagemaker [(Foto da configuração)](https://github.com/gaby-baratela/ifsp_s2_bitcoin/blob/97ce612542b03ce645676d8bfe89add27e1de2aa/Imagens/Configura%C3%A7%C3%B5es%20Sagemaker.png): O sagemaker foi configurado com a máquina ml.t3.medium, que contém 2 CPUs , 0 GPU e 4 GB de memória RAM. A plataforma escolhida foi Amazon Linux 2 - JupyterLab 3, devido à compatibilidade com bibliotecas e scripts, ele foi conectado ao github e não foi definida nenhuma configuração personalizada de rede. No sagemaker, a opção de Kernel é `conda_tensorflow2_p38`
    - S3 [(Foto da estrutura)](https://github.com/gaby-baratela/ifsp_s2_bitcoin/blob/97ce612542b03ce645676d8bfe89add27e1de2aa/Imagens/Estrutura%20S3.png): No S3 foi criado o bucket `projetointerdisciplinars2`, público, sem criptografia e com as configurações padrão da nuvem. Ele foi dividido entre as pastas `data/`, para armazenamento de dados, e `models/`, para armazenamento dos modelos treinados.  
    - Local: Todos os recursos estão sendo utilizados do Norte da virginia

### 3. Coleta de dados<a id="ancora3"></a>

**[Link do notebook](https://github.com/gaby-baratela/ifsp_s2_bitcoin/blob/cbe47e342c3c7ab67e5d9629c3a7add43ae20f2e/1_Coleta_de_dados.ipynb)**

Para entender como o bitcoin se comporta ao longo do tempo e realizar a predição de preços, é necessário, pelo menos, de sua série histórica diária. Além disso, alguns fatores podem influenciar no preço da criptomoeda e explicar sua variação, portanto serão estudados como potenciais covariáveis para o modelo.

Os dados foram coletados de diversas fontes via API, incluindo Yahoo Finance, NASDAQ Data, Google (pytrends). O período selecionado para análise foi dos últimos 5 anos, pois mesmo que as fontes forneçam ainda mais histórico caso haja necessidade, como a granularidade é diária, o período é suficiente para obtenção de muito insumo.


### 4. Análise Exploratória<a id="ancora4"></a>

Para conhecer melhor os dados, foi criado um notebook com análise exploratória 
**[neste link](https://github.com/gaby-baratela/ifsp_s2_bitcoin/blob/cbe47e342c3c7ab67e5d9629c3a7add43ae20f2e/2_Conhecendo_os_dados.ipynb)**.

Além disso, foi realizada uma análise extra sobre os dados de pesquisas sobre o assunto Bitcoin no google, que está **[neste notebook](https://github.com/gaby-baratela/ifsp_s2_bitcoin/blob/cbe47e342c3c7ab67e5d9629c3a7add43ae20f2e/3_Exploratoria_extra_pytrends_interesse_x_tempo_bitcoin.ipynb).**

### 5. Modelagem<a id="ancora5"></a>

A modelagem foi realizada [por esse notebook](https://github.com/gaby-baratela/ifsp_s2_bitcoin/blob/cbe47e342c3c7ab67e5d9629c3a7add43ae20f2e/4_Modelagem_bitcoin.ipynb). 

Os modelos foram: ARIMA, LR, MLP, XGB e RF. Apesar de modelos de machine learning serem usualmente mais robustos e completos, o modelo ARIMA se saiu melhor. A acurácia do período analisada é boa, porém quando se olha a longo prazo o modelo se comporta de forma flat, o que é esperado dado seu ajuste para período curto.

### 6. Discussão de Resultados e Melhorias<a id="ancora6"></a>

Como melhorias deste trabalho, pretendo desenvolver a modelagem em um horizonte maior, ajustando o modelo para tal; modelagem de redes neurais recorrentes, para que seja possível modelar a dependência temporal; uso de outras covariáveis que impactam no preço de fechamento ajustado da Bitcoin, a maior criptomoeda do mundo.
