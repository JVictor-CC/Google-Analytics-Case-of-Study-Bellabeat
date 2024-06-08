# Google-Analytics-Case-of-Study-Bellabeat

## Acesso ao Estudo de Caso

Meu estudo de caso esta dísponivel publicamente no site da Kaggle. Clique abaixo para acessar e interagir com o notebook.

<a href="https://www.kaggle.com/code/joovictordesouza/google-analytics-case-of-study" target="_blank">
  <img src="https://img.shields.io/badge/Kaggle-035a7d?style=for-the-badge&logo=kaggle&logoColor=white">
</a>

## Relatório

### Resumo da Tarefa de Negócios

O objetivo é analisar dados relacionados ao uso de dispositivos inteligentes, buscando insights sobre como os consumidores utilizam esses produtos. Com essas informações, pretende-se orientar as partes interessadas, incluindo a co-fundadora e CEO da Bellabeat, Urška Sršen, e o co-fundador e membro-chave da equipe executiva, Sandro Mur, na tomada de decisões estratégicas. Esta análise visa identificar tendências de mercado e selecionar um produto da Bellabeat para uma análise mais detalhada, visando aprimorar a estratégia de marketing da empresa.

### Descrição da Fonte de Dados

Os dados utilizados nesta análise foram obtidos a partir da plataforma FitBit e foram indicados pela CEO Urška Sršen como fonte de informação sobre o condicionamento físico dos usuários. Este conjunto de dados foi gerado por respondentes a uma pesquisa distribuída via Amazon Mechanical Turk entre 12/03/2016 e 12/05/2016. Trinta usuários elegíveis do Fitbit consentiram com o envio de dados pessoais do rastreador, incluindo informações sobre atividade diária, calorias diárias, intensidade diária, passos diários, sono diário e peso de usuários da FitBit.

Os dados foram coletados diversos dispositivos inteligentes FitBit, refletindo uma variedade de comportamentos e preferências individuais dos usuários. Devido a essas diferenças nos dispositivos e nos hábitos dos usuários, pode haver variações nos dados de uma mesma coluna.

Os dados estão disponíveis sob a licença CC0: Public Domain, permitindo seu uso sem restrições para qualquer finalidade. Todos os dados foram anonimizados, garantindo a privacidade dos participantes, que são identificados apenas por IDs numéricos, assegurando que nenhuma informação pessoal identificável fosse divulgada. Dessa forma, o acesso ao conjunto de dados é concedido de forma aberta e transparente.

O conjunto de dados possui 18 arquivos, porém para essa análise serão utilizados os datasets `dailyActivity_merged.csv` e o `sleepDay_merged.csv`.

### Limpeza e Manipulação de Dados

Durante o processo de limpeza e manipulação de dados, a linguagem R foi escolhida como a principal ferramenta devido à sua eficácia na manipulação de conjuntos de dados, sua flexibilidade e sua ampla gama de pacotes dedicados à análise de dados.

Os packages utilizados foram o `janitor` e os que estão presentes no package `tidyverse`, sendo alguns deles:

1. **dplyr**: Este pacote foi utilizado para realizar operações de limpeza, filtragem e transformação nos dados. Com funções como `filter()` e `mutate()`, foi possível remover observações inválidas, criar novas variáveis e realizar operações de agregação conforme necessário.
2. **readr**: Para importar e ler os dados em R, o pacote readr foi utilizado devido à sua eficiência e facilidade de uso. A função `read_csv()` foi empregada para carregar os dados do arquivo de origem para um formato adequado para manipulação.
3. **ggplot2**: Este pacote foi utilizado para a visualização dos dados, permitindo a criação de gráficos para análise e apresentação de resultados. Funções como `ggplot()` e `geom_...()` ajudaram a visualizar padrões e tendências nos dados.
4. **janitor**: O pacote janitor foi empregado para a limpeza dos dados, oferecendo funções como `clean_names()` para padronizar nomes de colunas.

Antes de serem analisados, os dados foram submetidos a uma lista de verificação de limpeza, que inclui:

- Verificação de Dados Ausentes ou Nulos.
- Formatação de dados em um padrão consistente.
- Verificação dos tipos de dados para garantir precisão.
- Verificação de duplicatas.
- verificação de padrao de códigos (como IDs).
- verificação de valores fora do padrão.

A limpeza foi realizada seguindo os passos acima. Após a limpeza, foram adicionadas informações sobre os dias da semana ao conjunto de dados, associando-as corretamente às respectivas datas. Isso foi feito com o objetivo de analisar o comportamento dos usuários ao longo da semana.

### Resumo da Análise e Descobertas

Inicialmente foram feitos resumos estatísticos de ambos os dataframes utilizando a função `summary()`, assim é possível observar o mínimo, o máximo e a média de dados como: total de passos (`total_steps`), calorias (`calories`), distância total (`total_distance`) e tempos de cada tipo de atividade. O mesmo para dados relacionados ao sono.

após isso, foram criadas categorias para os usuários de acordo com as atividades, seguindo as métricas definidas pela Organização Mundial da Saúde (OMS). Com essas informações é possivel rotular os dados da seguinte maneira:

- ( Atividade Moderada/Semana > 300 min OU Atividade Vigorosa/Semana > 150 min ) = Muito Ativo
- ( 150 min >= Atividade Moderada/Semana >= 300 min OU 75 min >= Atividade Vigorosa/Semana >= 150 min ) = Ativo
- Restante = Pouco Ativo ou Sedentário

Assim foi permitido tirar a conclusão que a maior parte das pessoas nesta pesquisa (21 dos 33) são usuários mais ativos, sendo 9 ativos e 13 muito ativos.

Em seguida os usuários foram categorizados com relação ao sono. Para isso, foram retiradas informações do artigo **"Recommended Amount of Sleep for a Healthy Adult: A Joint Consensus Statement of the American Academy of Sleep Medicine and Sleep Research Society"**. As informações coletadas permitiram categorizar em:

- Tempo de Sono >= 7 Horas = Sono Adequado
- Tempo de Sono < 7 Horas = Sono Inadequado

Com a média de sono dos usuários foi possível obter uma conclusão equilibrada. Das pessoas que utilizam os dispositivos para monitorar sono (24), 13 possuem o sono inadequado, sendo maioria, e 11 possuem sono adequado.

Para entender melhor como os usuários utilizam os dispositivos, foi verificado o uso dos mesmos durante os dias da semana no mês da pesquisa.

Primeiro foi obtida a informação de que a maioria dos usuários realiza mais tempo de atividades físicas (leves, moderadas e vigorosas), em média, aos sábados e a minoria às segundas e quintas.
Outra informação útil é o tempo médio de atividades físicas registradas por dias da semana. É possível verificar que, contribuindo com a informação anterior, o dia da semana que possui uma média de horas mais alta durante a semana são os sábados e o dia que possui menos horas, em média, é a quinta-feira.

Para entender como os usuários utilizam os dispositivos durante o dia, foi utilizado o dataframe `hourly_steps`, calculando a média de passos dos usuários por hora. Com o gráfico é visto que os horários do dia em que a média de passos dos usuários é mais alta, ou seja, em que os usuários são mais ativos, são das 8 da manhã às 19 da noite. Com altas de 12 às 14 e das 17 às 19, onde há o máximo às 18 horas.

No próximo passo, foi analisado o uso de dispositivos para atividades diárias e o uso de dispositivos para monitoramento do sono. As categorias definidas para ambos foram:

- Não usado (Not used) = 0 Registros de Sono
- Pouco usado (Lightly used) = de 1 a 10 dias de uso
- Regularmente usado (Regurlarly used) = de 11 a 20 dias de uso
- Usado com frequência (Frequently used) = de 21 a 31 dias de uso

Assim, ficou nítido que grande parte dor usuários (75.76%) usam seu dispositivo com frequência para atividades diárias, 21.21% usam dispositivos de forma regular e apenas 3.03% fazem pouco uso para esse intuito.

Já no uso para monitoramento de sono, tem-se novamente um resultado mais equilibrado, onde maioria (36.36%) utiliza o dispositivo com frequência, 9.09% utilizam de forma regular, 27.27% utilizam com pouca frequência e 27.27% não utilizam.

Após isso, foi examinado o tempo médio diário do dispositivo, somando os tempos de atividades disponiveis, que em horas devem ser menores que 24. Ao calcular a média de horas diária de uso por usuário, entendeu-se que a média de uso diário do dispositivo pelos usuários, se concentra ente 15 e 24 horas de uso. Sendo que quase metade dos usuários, nos dias que utilizam o dispositivo, utilizam aproximadamente de 22 a 24 horas. 

por fim foram verificadas as correlações entre os dados, com auxilio da lib `corrplot()` para criar matrizes de correlação. observando a matriz de correlação das atividades, nota-se que (como já esperado) a quantidade de calorias possui corelações positivas com as distancias percorridas, quantidade de passos e tempos de cada atividade. Assim como as distancias possuem fortes correlações com tempo. Já para os dados relacionados ao sono, é interessante notar que o tempo de sono possui uma correlação negativa com o tempo sedentário, ou seja, quanto maior o tempo sedentário, menor o tempo de sono. Não se pode afirmar que uma coisa causa a outra, mas existe uma correlação entre as duas variáveis.

### Principais Recomendações de Conteúdo de Qualidade com Base em sua Análise

Como a Bellabeat é uma fabricante de produtos de alta **tecnologia voltados à saúde** para mulheres. É possível utilizar dos insights desta análise para gerar recomendações personalizadas.

#### **Recomendações**

Gameficação parcial do aplicativo, para estimular a melhoria da saúde, a partir de metas para atividades físicas seguindo a OMS. O foco é melhorar a experiência para os usuários que já são ativos e tentar estimular os usuários sedentarios e pouco ativos, que são 1/3. Implementar um sistema de metas/desafios diários no aplicativo em conjunto com um sistema de recompensas (como troféus virtuais, possíveis descontos para os usuários mais engajados, leaderborads). 

Realização de campanhas/competições aos sábados, já que é o dia com maior média de atividades e que a maioria dos usuários realiza mais tempo de atividades. 

O envio de notificações nos dias da semana com menos atividade, em que os usuários tem uma média menor de tempo de atividade.

Oferecer workshops e recursos sobre higiene do sono, incluindo técnicas de relaxamento, criação de rotinas de sono consistentes e a importância do ambiente de sono para os assinantes dos planos da Bellabeat. Incluir também uma versão graruita que serve como prévia, para informar e estimular o usuários com sono inadequado, que são pouco mais de 50% dos presentes na pesquisa.

Fornecer informações sobre os benefícios do monitoramento do sono, através de notificações personalizadas, já que 54% dos usuários não utilizam (27% - 0 dias de uso) ou utilizam pouco (27% - 1 a 10 dias de uso) o recurso. Outra opção é realizar uma pequena pesquisa (não obrigatória), questionando o motivo de não utilizarem o monitoramento de sono, a partir de uma pergunta com um seletor de respostas, assim que abrirem o app.

Oferecer informações detalhadas, sobre os dados coletados incluindo descrições breves e diretas, assim como gráficos para facilitar o entendimento. O intuito é ajudar os usuários a entenderem melhor seus próprios habitos. 
