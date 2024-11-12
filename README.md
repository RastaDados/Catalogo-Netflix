<h1> Projeto Filmes Netflix </h1>

<br>

Este projeto tem como intuito trazer informações para uma posterior análise de dados relacionados ao catálogo de filmes da empresa Netflix.

<h1>Entendo a Base de Dados</h1>

Puxei os dados de uma única tabela chamada de "n_movies" na extensão .csv com as seguintes colunas:

<h3>title</h3>
Essa coluna contém os dados referentes ao nome dos títulos (filmes, séries, doramas, etc.

<h3>year</h3>
Essa coluna contém os dados referentes ao ano dos títulos.

<h3>certificate</h3>
Essa coluna contém os dados referentes a classificação indicativa do título.

<h3>duration</h3>
Essa coluna contém os dados referentes a duração em minutos dos títulos, geralmente em séries tem a duração de cada episódio.

<h3>genre</h3>
Essa coluna contém os dados referentes ao gênero do filme, contém três gêneros com separadores de vírgula, sendo o primeiro gênero o predominante.

<h3>rating</h3>
Essa coluna contém os dados referentes à nota de cada título.

<h3>description</h3>
Essa coluna contém os dados referentes á descrição do título (sinopse).

<h3>stars</h3>
Essa coluna contém os dados referentes aos atores principais que participaram do título.

<h3>votes</h3>
Essa coluna contém os dados referentes a quantidade de votos cada título teve.

<hr>
<br>
<br>

<h1>Página Inicial</h1>

Irei criar a primeira página do Dashbaord, a <b>Página Inicial</b> será o pontapé para o cliente navegar entre as páginas do Dashboard.

Para começar, mudarei o Background da página para me auxiliar na construção dos gráficos e já alocá-los corretamente.

Após alocado o Background vou criar um botão com a ação de navegar para a página <b>Netflix</b> que será criada posteriormente.

Após todas as etapas, a <b>Página Inicial</b> ficou assim:

![01](https://github.com/user-attachments/assets/fec9a9aa-b412-40c9-bc7c-a5c1c8c270fc)

<hr>
<br>
<br>

<h1>Página Netflix</h1>

Nessa página ficarão todos os gráficos para uma posterior análise dos mesmos, será a única página além da página inicial nesse Dashboard.

Agora vou construir o layout da primeira página.

Eu começo mudando a dimensão da página, colocando as medidas de 1.100 (altura), 1.900 (largura);

Logo após já coloco o background da página, pois com o background já aplicado torna muito mais fácil de criar os gráficos na página, pois já fica evidente aonde tenho que organizá-los por conta do Layout presente na imagem que servirá como Background.

![01](https://github.com/user-attachments/assets/0409e8b3-b3ce-407f-8040-0c8956a0cb1f)

<br>
<br>

Agora vou começar a construção dos meus gráficos.

Os primeiros gráficos que serão construídos vão ser gráficos de Cartões.

<h2>Primeiro Cartão</h2>

Na aba Campos coloco a medida <b>"Total Generos"</b>

Na parte de estilização eu posso colocar uma medida do formato texto no campo de subtítulo, então irei criar a medida para utilizar essa funcionalidade do cartão.

A medida criada se chamará <b>"Card Titulos".</b>

Medida criada:

Card Titulos = FORMAT([Total Titulos], "#0") 

Explicando a medida é bem simples, farei a transformação da medida Total Titulos em string, mas ainda a deixando como um número.

Vou criar mais uma medida chamada <br>"Card Generos"</b> que será meu título do gráfico de Cartão

Medida Criada:

Card Generos = [Total Genero] & "Gêneros"

Explicando a medida, trás em texto o total de gêneros e acrescenda a palavra "Gêneros" ao final do texto.

![02](https://github.com/user-attachments/assets/4adce409-7b30-4c9f-bb55-868013aa4b18)

<br>
<br>

Agora farei a criação do outro Cartão

Esse cartão tem como finalidade exibir o Total de votos e total de votos por título.

Farei a criação de duas medidas novas, para o título e o subtítulo do cartão

A primeira medida para o titulo se chamará <b<"Card Votos por Titulos"</b>

Medida Ccriada:

Card Votos por Titulos = FORMAT([Votos por Titulo], "#,0") & " votos por título"

Exemplificando a medida, ela trás os votos por titulos da medida <b>"Votos por Titulos"</b> e acrescenda a frase "votos por título" ao final. O FORMAT serve para formatar o valor em um numero decimal passando a expressão <b>"#,0"</b>.

A segunda medida para o subtítulo se chamará  <b>"Card Votos"</b>

Medida Criada: 

Card Votos = FORMAT([Total Votos], "#,0")

Exemplificando a medida, ela puxa os dados de total de votos da medida <b>"Total Votos"</b> e o FORMAT transforma esse resultado em um número decimal passando a expressão <b>"#,0"</b>.

![03](https://github.com/user-attachments/assets/f39a31f7-64f4-40f2-a9b4-1d4f36550198)

<br>
<br>

Agora criei um gráfico de Segmentação de Dados.

Esse gráfico servirá para fazer um filtro na página de acordo com o(s) ano(s) escolhidos.

Na aba Campo ele recebe a coluna <b>"Ano"</b> da tabela <b>"dAno".</b>

![04](https://github.com/user-attachments/assets/4f461ebb-9542-4206-8435-93faf2630b7b)

<br>
<br>

Vou criar um gráfico de tabela para exibir o titulo, ano, score médio e total de votos.

Na campo Colunas:

Adicionei a coluna <b>"title"</b> da tabela <b>"fTitulos"</b> e renomeie para Títulos.

Adicionei a coluna <b>"ano"</b> da tabela <b>"dAno"</b>

Adicionei a medida <b>"Score Médio"</b> e renomeie para <b>"Nota Média"</b>

Adicionei a medida <b>"Total Votos"</b>

Logo após a criação dessa tabela, criei um grafico de Segmentação de Dados

<br>

Na aba Campos :

Adicionei a coluna <b>"title"<b> da tabela <b>"fTitulos"</b> e renomeie para <b>"Títulos".</b>

![05](https://github.com/user-attachments/assets/5cadeb7e-abce-40c5-94fb-ba08550f8286)

<br>
<br>

Porém não quero filtrar o título, e sim destacar. Para isso preciso duplicar a tabela de <b>"fTitulos"</b>, e qualquer mudança em uma acarretará em uma mudança automática na outra, pois uma sera referência da outra.

Agora renomeio a minha primeira tabela de <b>"fTitulos"</b> para <b>"fTitulosA"</b> e a tabela duplicada como <b>"fTitulosB"</b>

Também criarei uma nova tabela dimensão dos dados de Genêro a partir da coluna <b>"genrer"</b>, para poder filtrar por gêneros no meu gráfico. Após a criação da tabela <b>"dGenero"</b> contendo apenas a coluna <b>"genrer"</b> da tabela <b>"fTitulos"</b> eu retiro todos os valores duplicados da mesma.

Para ficar melhor a compreensão, a coluna contida na tabela <b>"fTitulosA"</b> eu utilizarei no campo do gráfico como valor, e a mesma coluna da outra tabela <b>"fTitulosB</b> irei usar como um filtro do gráfico.

![06](https://github.com/user-attachments/assets/3a83b4ab-9fe6-4999-bfcc-41645739ffbd)

<br>
<br>

Para realizar o relacionamento dessa tabela recém criada eu preciso de uma coluna com uma <b>SurrogateKey (SK)</b>.

Crio uma coluna de índice, enumerada de 1 até o fim do número do dado presente na tabela.

Na minha tabela <b>"fTitulosA"</b> vou trazer minha coluna criada com a <b>"SK"</b> para a tabela <b>"fTitulosA"</b> atrvés da mesclagem de colunas.

E depois de trazer essa coluna, eu deleto (drop) a coluna de <b>"genrer"</b> da tabela <b>"fTitulosA"</b>

Como a tabela <b>"fTitulosB"</b> é uma referência da tabela <b>"fTitulosA"</b> todas esas etapas realizadas na <b>"fTitulosA"</b> já estão refletidas na tabela <b>"fTitulosB"</b>.

![07](https://github.com/user-attachments/assets/ec031d98-46de-435f-9ec8-67396f8096cf)

<br>
<br>

Agora faço o relacionamento das novas tabelas.

Relaciono o <b>"dAno"</b> com <b>"fTitulosB"</b> através da coluna <b>"Ano"</b>.

O resto dos relacionamentos o Power BI criou automaticamente. (Oh ferramentazinha boa viu!)

































