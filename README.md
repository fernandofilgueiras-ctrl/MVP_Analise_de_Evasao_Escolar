# MVP_Analise_de_Evasao_Escolar
MVP para análise de evasão escolar - Especialização em Ciência de Dados e IA - PUC-Rio
Predição de evasão e sucesso acadêmico no ensino superior

MVP da disciplina Análise de Dados e Boas Práticas

Discente Fernando de Barros Filgueiras

Sobre o projeto

Este repositório reúne a análise exploratória e o pré-processamento de uma base de dados sobre evasão e sucesso acadêmico de estudantes de graduação. O notebook funciona como relatório do trabalho e contém o código, os resultados, as interpretações, as decisões tomadas e as limitações.

O trabalho termina na preparação dos dados. Nenhum modelo de aprendizado de máquina é treinado. O uso preditivo futuro para o qual os dados são preparados é uma classificação multiclasse da situação final do estudante, com as categorias Dropout, Enrolled e Graduate.

Perguntas investigadas
Hipótese	Enunciado resumido
H1	O desempenho nos dois primeiros semestres reúne os atributos mais associados à situação final
H2	Regularidade das mensalidades, condição de devedor e bolsa de estudos associam-se à permanência
H3	Idade de ingresso mais avançada, vias de acesso não convencionais e regime noturno associam-se a maior evasão
H4	A classe Enrolled é a mais difícil de separar das demais

As respostas a cada hipótese, com a evidência correspondente e o que permanece incerto, estão na seção 6 do notebook. A hipótese H4 não é testada diretamente, pois dependeria do treinamento de um modelo.

Dados
Item	Descrição
Base	Predict Students' Dropout and Academic Success
Fonte	UCI Machine Learning Repository, https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success
DOI do conjunto	https://doi.org/10.24432/C5MC89
Versão	Arquivo data.csv doado ao repositório em 12 de dezembro de 2021
Dimensões	4424 linhas e 37 colunas (36 atributos e a variável alvo Target)
Unidade de observação	Um estudante em uma matrícula de graduação
Recortes	Nenhum. A base é utilizada integralmente
Licença	Creative Commons Atribuição 4.0 Internacional (CC BY 4.0)

Os dados são anonimizados e não contêm identificadores pessoais. O dicionário completo das variáveis está na seção 1.5 do notebook.

Estrutura do repositório
.
├── evasao_academica_preprocessamento.ipynb   Notebook com o relatório completo
└── README.md                                  Este arquivo
Como executar
Abra o notebook no Google Colab pelo botão no topo desta página ou pelo link https://colab.research.google.com/drive/1_aSW9358RguPwXCGo85cuuzHF1hIwCd8
No menu, escolha Ambiente de execução e depois Executar tudo.
Quando solicitado, autorize a montagem do Google Drive.

A célula de carga procura a pasta Análise de Dados II no Drive montado. Quando a pasta não é encontrada, o notebook baixa automaticamente o arquivo data.csv da pasta compartilhada do projeto, sem necessidade de credenciais do autor nem de intervenção manual. Ao final da execução, o Colab oferece o download do arquivo dados_processados.zip.

Dependências

O notebook utiliza apenas bibliotecas já disponíveis no ambiente padrão do Google Colab.

Biblioteca	Uso
pandas	Manipulação tabular
NumPy	Operações numéricas
scikit-learn	Partição dos dados, padronização e informação mútua
Matplotlib e seaborn	Visualização
gdown	Download da pasta compartilhada do Google Drive

As versões efetivamente utilizadas são impressas na seção 2 do notebook a cada execução. A semente aleatória é fixada em 42 para garantir a reprodução da partição e da informação mútua.

Organização do notebook
Seção	Conteúdo
1. Definição do problema	Problema, unidade de observação, hipóteses, objetivo analítico, fonte e dicionário de variáveis
2. Configuração do ambiente e carga dos dados	Bibliotecas, versões, carga e padronização dos nomes das colunas
3. Análise exploratória de dados	Dimensões, tipos, ausências, duplicidades, inconsistências, valores extremos, distribuições e relações com a situação final
4. Pré-processamento de dados	Decisões D1 a D4, partição em treinamento e teste, codificação, padronização e verificações antes e depois
5. Finalização e download da base processada	Gravação das visões processadas
6. Considerações finais	Respostas às hipóteses, limitações e próximos passos
7. Referências	Fontes de dados e bibliotecas
8. Declaração de uso de IA	Registro do uso de ferramentas de IA
9. Checklist de entrega	Localização de cada requisito no notebook
Decisões de pré-processamento
Decisão	Problema observado	Escolha
D1	A nota zero tem dois significados, desempenho nulo ou ausência de avaliação	Manter o zero e criar indicadores de ausência de avaliação
D2	Proporção elevada de valores discrepantes pelo critério do intervalo interquartil	Manter os valores, pois a remoção eliminaria 45,7% das linhas e 73,8% dos evadidos
D3	Atributos nominais com muitas categorias raras	Agrupar as categorias com menos de 1% do treinamento antes da codificação one-hot
D4	Escalas muito distintas entre os atributos numéricos	Gerar uma visão sem escala e uma visão padronizada por z-score

A partição em treinamento (80%) e teste (20%) é estratificada pela variável alvo e antecede todas as transformações que aprendem parâmetros dos dados, de modo a evitar vazamento de informação.

Saídas geradas

A execução produz o arquivo dados_processados.zip com os seguintes conteúdos.

Arquivo	Descrição
onehot_train.csv e onehot_test.csv	Visão base, com atributos derivados e codificação one-hot dos nominais
standardized_train.csv e standardized_test.csv	Visão base com padronização dos atributos numéricos
dataset_preprocessado_completo.csv	Base completa com os atributos derivados, antes da partição
dicionario_de_dados.csv	Correspondência entre os nomes originais e os nomes padronizados
codificacao_alvo.csv	Correspondência entre as classes do alvo e seus códigos
Principais resultados

A base tem 49,9% de concluintes, 32,1% de evadidos e 17,9% de estudantes ainda matriculados. Os atributos de desempenho no primeiro ano são os mais associados à situação final. A evasão é de 86,6% entre os estudantes com mensalidades em atraso, contra 24,7% entre os que estão em dia, e cresce de 21,0% entre os que ingressam com 17 a 19 anos para 57,6% na faixa de 25 a 29 anos. As associações são descritivas e não devem ser lidas como relações causais.

A análise também identificou uma lacuna de registro. Os 180 registros sem nenhuma inscrição em unidades curriculares pertencem todos a um único curso, o que explica a presença de concluintes com nota zero.

Limitações

Os dados provêm de uma única instituição portuguesa e de um período encerrado em 2018/2019. A análise é univariada e descritiva, sem testes de hipótese nem controle de fatores sobrepostos. A base chegou pré-processada pelos autores, sem registro dos casos removidos.

Referências

Realinho, V., Machado, J., Baptista, L., e Martins, M. V. (2022). Predicting student dropout and academic success. Data, 7(11), 146. https://doi.org/10.3390/data7110146

Realinho, V., Vieira Martins, M., Machado, J., e Baptista, L. (2021). Predict Students' Dropout and Academic Success [conjunto de dados]. UCI Machine Learning Repository. https://doi.org/10.24432/C5MC89
