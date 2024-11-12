<h1> Projeto Filmes Netflix </h1>

<br>

<a href="https://app.powerbi.com/groups/me/reports/e71db363-e2b0-4147-8e87-68c43e37e3a7/ecae17acacc2d71c9722?experience=power-bi"> Acesse o Dashboard </a>

<hr>

Este projeto tem como intuito trazer informações para uma posterior análise de dados relacionados ao catálogo de filmes da empresa Netflix.

<h1>Entendo a Base de Dados</h1>

Puxei os dados de uma única tabela chamada de "n_movies" na extensão .csv com as seguintes colunas:

![Dados](https://github.com/user-attachments/assets/d7d81096-a4b1-403e-b99e-6927f9cce28e)

<br>
<br>

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

<h1>Tratamento dos Dados - ETL</h1>

Primeiramente, antes de tudo, preciso vê se meus dados estão da forma correta, observando a fonte de dados vi que alguns estavam com formatação e digitação imprópria para trazer pra dentro do meu ambiente do Power BI.

Para começar meu tratamento de dados do processo de ETL, vou abrir dentro do Power BI o PowerQuery, onde eu farei todo o processo de tratamento.

![01](https://github.com/user-attachments/assets/9df38dda-179f-4a3c-9697-70f63f6db422)

<br>
<br>

Faço as seguintes transformações:

IMPORTANTE - Todas as transformações serão feitas usando o padrão dos Estados Unidos.

Nas colunas <b>"rating"</b> e <b>"votes"</b> altero o tipo de dado para "Usando a Localidade" > "Número Decimal" > "Ingês Estados Unidos"

![02](https://github.com/user-attachments/assets/43e0c4dc-9726-4efb-8f14-f1f835c96fac)

<br>
<br>

Na coluna <b>"duration"</b>, farei a extração para ter apenas os números, removendo a palavra <b>"min"</b> após os mesmos. Faço também a transformação do tipo de dado para <b>"Número Inteiro"</b>.

![03](https://github.com/user-attachments/assets/c9d61cf6-42bf-4ff5-b2bf-bcd17eadc96e)

<br>
<br>

Agora vou fazer o tratamento mais complexo, que será da coluna <b>"year"</b>.

Irei adicionar uma coluna de exemplo da seleção, para a IA do PoweBi me ajudar a criar um padrão para a nova coluna de <b>"year"</b> chamando-a de <b>"Ano"</b> com base nos dados da coluna <B>"year"</b>.

Após a transformação eu extraio apenas o ano no formato de <b>"YYYY"</b>.

Após a criação da nova coluna <b>"Ano"</b>, faço a transformação do tipo de dado para <b>"Número Inteiro"</b>.
 
Após a transformação do tipo de dados a coluna ficou com um erro, então faço remoção desse erro (Apenas uma dado estava no formato errado) e a remoção também de dados vazios (com dados vazios não consigo realizar análises).

![04](https://github.com/user-attachments/assets/96c3a238-f200-46a7-9f1e-f361e5429e39)

<br>
<br>

Na coluna <b>"genre"</b> preciso extrair o primeiro gênero da coluna, tem três genêros em cada filme porém o primeiro gênero é o predominante de cada filme.

![05](https://github.com/user-attachments/assets/e5cda048-4c1a-45c5-91e3-0d4e3aeb5db5)

<br>
<br>

Agora a minha tabela <b>"n_movies"</b> está com todas as suas respectivas formatações completas.

Vou renomear de <b>"n_movies"</b> para <b>"fTitulos"</b>. o <b>"f"</b> no começo do nome é apenas para exemplificar que é uma tabela Fato e não Dimensão (utilizo o <b>"d"</b> no começo).

![06](https://github.com/user-attachments/assets/c81d823c-5ae2-4fd6-bb0d-e1ae749b38a5)

<br>
<br>

Agora com meus dados tratados posso realizar a criação do meu Dashboard!

<hr>
<br>
<br>

<h1>Criação das Medidas Fundamentais</h1>

A criação de medidas utilizando a linguagem DAX (Data Analysis Expressions) é fundamental para os tipos de análise que irei fazer posteriormente na criação dos gráficos que compõem meu Dashboard.

Comecei criando uma tabela chamada <b>"Medidas"</b> com a funcção única e exclusivamente de serir como um repositório para guradar e organizar as medidas que eu vou criar.

![01](https://github.com/user-attachments/assets/04e9d59f-a818-40ef-a80a-eb4b8be0721c)

<br>
<br>

A primeira medida que criei foi a <b>"Total Titulos"</b> para saber quantos filmes existem pelo titulo.

Utilizei a função DISTINCTCOUNT para buscar os valores únicos dos titulos na coluna <b>"title"</b> da tabela <b>"f_Titulos"</b>.

![2](https://github.com/user-attachments/assets/91c5987c-087f-40a3-9fcb-594b4fe5b479)

<br>
<br>

A próxima medida será a de <b>"Total Votos"</b> que exibirá quantos votos tiveram o filme especificado.

Trago a função SUM para fazer a soma dos votos que estão na coluna <b>"votes"</b> da tabela <b>"fTitulos"</b>.

![03](https://github.com/user-attachments/assets/eb1b6fe1-cc34-47e8-80d3-dd1c57e9d7bc)

<br>
<br>

Criarei mais uma medida chama de <b>"Score Médio"</b>, ela exibiriá as notas dos filmes (titulos).

Utilizo a função AVERAGE para me trazer a média dos scores (notas) da coluna <b>"rating"</b> da tabela <b>"fTitulos"</b>.

![04](https://github.com/user-attachments/assets/cc28d2a9-96e7-429b-8891-ad71ea9799d4)

<br>
<br>

Vou criar mais uma medida chama de <b>"Total Generos"</b> que exibirá a quantidade de Generos diferentes que existem nos filmes.

Utilizo a função DISTINCTCOUNT da colunas de <b>"genre"</b> da tabela <b>"fTitulos"</b> justamente para buscar todos os valores distintos de generos.

![05](https://github.com/user-attachments/assets/a596c2a5-39df-4844-aaad-3e2db96f1648)

<br>
<br>

Vou criar a medida de <b>"Votos por Titulo"</b> que irá exibir a quantidade média de votos por filmes.

Utilizo a função DIVIDE para fazer a divisão das medidas já criadas <b>"Total Votos"</b> e <b>"Total Titulos"</b>.

![06](https://github.com/user-attachments/assets/64e9e4a9-84cb-4713-b89a-02378be57796)

<br>
<br>

Nessa etapa criarei uma tabela fundamental para a realização das análises.

Essa tabela será uma tabela de inteligência de tempo, contendo dados de Data.

A tabela se chamará <b>vAno</b>.

Crio uma variável chamada <b>"vAnoMin"</b> e ela irá guardar os dados com valor mínimo da coluna <b>"Ano"</b> da tabela <b>"fTitulos"</b>

Crio a segunda variável chamada <b>"vAnoMax"</b> e ela irá guardar os dados com valor máximo da coluna <b>"Ano"</b> da tabela <b>"fTitulos"</b>

Agora retorno como valor as variáveis criadas incrementando de 1 em 1.

Logo após criada eu faço a relação da tabela <b>"dAno"</b> com a tabela <b>"fTitulos"</b>

![07](https://github.com/user-attachments/assets/ff81dea8-2d39-446b-be7b-af95475899c9)

<br>
<br>

Com os dados limpos e as medidas fundamentais para a criação dos meus gráficos já criadas, posso partir para criação da minha primeira página de Dashboard.

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

![08](https://github.com/user-attachments/assets/8e91736f-a2e3-47a7-aaa9-9d0df780d33c)

<br>
<br>

Ainda no gráfico de tabelas, irei criar uma formatação condicional para o campo títulos.

Vou criar uma medida chamada <b>"Condição"</b>

Exemplificando a medida:

Criei duas váriaveis para me mostrar o filme selecionado, porém uma é para usar no visual e a outra para usar no filtro.

Na condição do RETURN eu trago um IF, caso o filme seja igual ao do selecionado no filtro de filmes, ele traz o valor sim, e na tabela ficam filtrados em primeiro todos os filmes que estão selecionados no filtro de filmes.

![09](https://github.com/user-attachments/assets/43043cb1-2568-410f-8f68-a8c554815de6)

<br>
<br>

Agora sempre que eu filtrar por um filme especifico, a condição estando sim trás em destacado o filme na tabela.

obs: Retirei a coluna <b>"Ano"</b> da tabela, pois a mesma não estavá deixando eu filtrar pelo nome do filme.

![10](https://github.com/user-attachments/assets/c9785438-8159-40e8-810a-37e5409b6afb)

<br>
<br>

O gráfico de Tabela me serviu apenas como base para eu criar as etapas anteriormente.

Trocarei o gráfico de Tabela pelo gráfico de Dispersão

Adicionei os dados no gráfico de Dispersão da seguinte forma:

No campo valores adicionei a coluna <b>"title"</b> da tabela <b>"fTitulosA"</b>

No campo <b>"Eixo X"</b> adicionei a coluna <b>"Ano"</b> da tabela <b>"fFiltrosA"</b>

No campo <b>"Eixo Y"</b> adicionei a medida <b>"Score Médio"</b>

No campo <b>"Tamanho"</b> adicionei a medida <b>"Total Votos"</b>

Cada bolinha desse gráfico corresponde a um título filtrado pelos anos do Eixo X. Quanto maior a bolinha, mais votos o filme teve.

![11](https://github.com/user-attachments/assets/a20e0eca-39bd-4674-bdf2-109376e67638)

<br>
<br>

Agora vou fazer uma formatação condicional neste gráfico.

O intuito será pintar o filme selecionado no filtro com as bolinhas brancas, e o resto com as bolinhas vermelhas.

Para conseguir esse resultado tive que mexer na minha medida já criada <b>"Condição"</b>.

Coloquei o hexadecimal "#ECE8E8" (branco) para o Sim da condição IF

Coloquei o hexadecimal "#EF444070" (vermelho) para o Não da condição IF

![12](https://github.com/user-attachments/assets/4a919123-f178-48e7-b79b-43821c040ea6)

<br>
<br>

Agora vou criar uma matriz para servir como filtro para os títulos.

Na Matriz criada adicionei os seguintes dados:

No campo Linhas adicionei a coluna <b>"title"</b> da tabela <b>"fTitulosB"</b>.

![13](https://github.com/user-attachments/assets/f8707b72-bb98-4b68-97ab-d13a64108cfd)

<br>
<br>

Agora irei criar um parâmetro para fazer o filtro dos filmes de acordo com a nota dada a eles.

Para isso, preciso criar um parâmetro de intervalo numérico.

Faço a incrementação de 1 em 1, com o mínimo em nota 0 e o máximo em nota 10. 

![14](https://github.com/user-attachments/assets/536496f7-5507-48a4-8646-ad599713990d)

<br>
<br>

Agora preciso de uma medida para usar no meu parâmetro.

Irei reutilizar a medida <b>"Condição"</b> para essa finalidade.

Adicionei duas novas variáveis ao código da medida que foi o <b>vMinFaixa</b> e <b>vMaxFaixa</b> que são o máximo e o mínimo do parâmetro criado.

Troquei oIF por um SWITCH pois iria usar mais que duas opções:

Se a nota média do filme contido na medida <b>"Score Médio"</b> for maior que a máxima escolhida no filtro do parâmetro criado, pinta a bolinha de transparente, ou seja, ela não irá aparacer.

Se a nota média do filme contido na medida <b>"Score Médio"</b> for menor que a mínima escolhida no filtro do parâmetro criado, pinta a bolinha também de transparente.

![15](https://github.com/user-attachments/assets/e7838866-a022-4078-af51-1a218197d4c1)

<br>
<br>

Agora criarei outro parâmetro para filtrar por maiores e menores médias de notas dos filmes.

Porém farei diferente, esse parâmetro irei digitar "na mão", criando uma tabela invés da opção de parâmetro, e configurando-a como se fosse um parâmetro.

Cirei a tabela chamada <b>"Parâmetro Total Votos"</b>, uma coluna chamada <b>"id"</b>, e uma coluna chamada <b>"condicao"</b>

Na coluna <b>"id"</b> é o identificador.

Na coluna condicao coloquei os seguintes dados:

Todos

Acima da Média

Baixo da Média

![16](https://github.com/user-attachments/assets/99c73c7d-7b1c-4d99-b4ef-9de5e642e9e3)

<br>
<br>

Agora vou criar um gráfico de segmentação de dados justamente para colocar o parâmetro que criei anteriormente como filtro.

Adicionei os seguintes dados no gráfico:

No campo de Valores adicionei a coluna <b>"Condicao"</b> do <b>"Parâmetro Total Votos"</b>

![17](https://github.com/user-attachments/assets/28230fc1-622a-4e38-8dd1-1907890fd4fc)

<br>
<br>

Agora para fazer este filtro criado funcionar, irei reaproveitar novamente nossa medida Frankestein <b>"Condicao"</b>

Criei a variável <b>vMediaVotos</b> e utilizei a medida <b>"Votos por Titulo"</b> para buscar todos os votos, e a função ALL para buscar os votos de todos os titulos de toda a tabela <b>"fTitulosA"</b> ignorando seus filtros.

Crio outra variável chamada de <b>vCondicaoSelecionada</b> com a função SELECTEDVALUE para selecionar da coluna <b>"id"</b> da tabela <b>"Parametro Total Votos"</b> que é a tabela que criei para filtrar os filmes pela média de votos.

Agora dentro do SWITCH adiciono a seguinte condição:

Adiciono a variável <b>"vCondicaoSelecionada"</b> igual ao valor 2 da nossa tabela de <b>"Parametro Total Votos"</b> e (&&) se for menor que a nossa média de votos presentes na variável <b>"vMediaVotos"</b>, pinta de transparente.

Adiciono a mesma variável <b>"vCondicaoSelecionada"</b> novamente, agora igualando o valor 3 da nossa tabela de <b>"Parametro Total Votos"</b> e (&&) se for maior que a nossa média de votos presentes na variável <b>"vMediaVotos"</b>, pinta de transparente também.

![18](https://github.com/user-attachments/assets/036885f3-b64e-4b48-9ac4-d64c4d40d6a3)

<br>
<br>

Agora para finalizar a página irei criar um gráfico de Segmentação de Dados para filtrar por gêneros dos filmes.

Aciciono os seguintes dados no gráfico de Segmentação de Dados:

Na aba Campo adiciono a coluna <b>"genrer"</b> da tabela <b>"dGenero"</b>.

![19](https://github.com/user-attachments/assets/472d85c1-e8f9-4192-9855-d856458cfb68)

<hr>
<br>
<br>

<h1>Tooltip da Página Netflix</h1>

Agora vamos criar uma página chamada "Toooltip" para utilizarmos no gráfico de dispersão da página "Netflix" criada anteriormente.

Começo criando a página nova e ativando a mesma como uma dica de ferramenta.

Depois coloco um Background na página.

Vou fazer a criação de três gráficos de cartão

Cartão 1 exibirá o nome do título:

Recebe na aba Campo a coluna <b>"title"</b> da tabela <B>"fTitulosA"</b>

Cartão 2 exibirá quantidade de votos:

Recebe na aba Campo a coluna a medida <b>"Total Votos"</b> que renomeie para <b>"Votos"</b>

Cartão 3 exibirá a quantidade de score médio (votos):

Recebe na aba Campo a coluna a medida <b>"Score Médio"</b>

Por fim a página de tooltip ficou da seguinte da forma:

![01](https://github.com/user-attachments/assets/fd1b8597-96c7-40d9-9964-169e465860f1)

<br>
<br>

Basta eu adicionar o Tooltip no gráfico de dispersão da Página Netflix.

Agora quando passa o mouse em cima da bolha no gráfico, o Tooltip aparece da seguinte forma:

![02](https://github.com/user-attachments/assets/f29ac7c0-a341-475e-a527-81c1591361b8)

<hr>
<br>
<br>















































