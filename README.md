# Classification Heart Failure
Nesse repositório tentei resolver umproblema de classificação. Apliquei dois modelos (regressão logística e árvore de decisão) e também comparei a performance entre dados balanceados e desbalanceados utilizando o método under sampling.

# Dados
[Link do Kaggle](https://www.kaggle.com/andrewmvd/heart-failure-clinical-data)

Neste projeto eu quero prever se alguma pessoa com algumas características tem chance de morte ou não. Mas antes disso, vamos explorar o conjunto de dados.

# Feature Engineering - Correlação
A correlação corresponde ao quanto uma variável está conectada com outra. Suponha uma função linear como segue: y = βx, onde y e x são variáveis e β é o coeficiente de inclinação. Quanto maior o β, o x é mais correlacionado com y.

Alta correlação pode prejudicar nosso modelo, então temos que cuidar disso.

Neste projeto vou considerar uma alta correlação que é mais de 70%. Pelo relatório do perfil dos pandas vimos que as variáveis não têm correlações superiores a 70%. A maioria é de 45% com fumo e sexo, veja

# Feature Engineering - Distribuição
A distribuição da variável é importante para nós porque representa a aleatoriedade dos nossos dados. Precisamos de dados distribuídos para ter bens variáveis independentes para prever a nossa variável dependente.

Há duas razões para remover variáveis com baixa distribuição:
Variável é aleatória, mas não nos ajudará a determinar nossa variável dependente porque os valores dessa variável não estão tão distribuídos quanto é necessário para gerar uma inteligência a partir dela.

Variável não é aleatória, então não é significativo determinar nossa variável dependente
Vimos também que as variáveis têm uma boa distribuição no relatório do perfil pandas. Eu coloquei um limite de 70-30 para uma boa distribuição, porque uma concentração de mais de 70% pode nos dar algum problema.

Podemos ter um problema com a distribuição do alvo "heart_failure". No nosso conjunto de dados quase 70% têm um valor 0, isto é, não tiveram insuficiência cardíaca.
Como queremos classificar entre duas classes ("tiveram insuficiência cardíaca" e "não tiveram insuficiência cardíaca"), talvez o nosso modelo dê 70% de precisão, mas dá-nos apenas o valor 0. Não é um bom modelo, vai sempre devolver apenas uma classe.
Chamamos de alarme falso. Podemos corrigi-lo quando rodamos nosso modelo. Com antecedência, vou usar o método under_sampling. Mas, quero mostrar os resultados com dados desequilibrados e equilibrados para comparação!

# Resultados - Ajuste dos dados com Regressão Logística

## Dados Desequilibrados
![image](https://user-images.githubusercontent.com/56306657/122310362-9145c200-cee6-11eb-9e1b-1d4111ab8d80.png)

## Dados Equilibrados
Under_sampling remove algumas observações da classe que aparecem mais e equilibra com a classe com menos frequência.
![image](https://user-images.githubusercontent.com/56306657/122309392-99046700-cee4-11eb-9697-53826b1f44e0.png)

# Montagem dos dados com Modelo de Árvore de Decisão
## Dados Desequilibrados
![image](https://user-images.githubusercontent.com/56306657/122309447-b3d6db80-cee4-11eb-9512-9c9ea30d5fb4.png)

## Dados equilibrados
![image](https://user-images.githubusercontent.com/56306657/122309507-ca7d3280-cee4-11eb-9dcc-a5fbee70b782.png)

# Conclusão
No nosso caso, o que importa? Estamos tentando prever se uma pessoa tem alta chance de ter uma parada de coração e imagine que tenha algum tratamento para essas pessoas, a nossa intenção é criar um modelo que para todas as pessoas que precisam de um tratamento o modelo sinalize a classe 1. Logo, precisamos observar a métrica recall, onde calcula a divisão da quantitade que o modelo acerta a classe 1 (VP) dividido pela que o modelo acerta a classe 1 (VP) mais o que o modelo erra na classe 1 (FP). Logo, ficamos com o modelo de Modelo de Árvore de Decisão com dados balanceados com 90% de recall.




