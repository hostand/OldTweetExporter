# Obter antigos tweets programaticamente
Um projeto escrito em Python para obter tweets antigos, ignorando algumas limitações da API oficial do Twitter.

## Detalhes
A API oficial do Twitter tem a limitação das restrições de tempo, você não pode obter tweets mais antigos do que uma semana. 
Quando você entra na página do Twitter, um carregador de rolagem é iniciado, se você rolar para baixo, começa a receber mais e mais tweets, através de chamadas para um provedor JSON. Assim mimetizando essa funcionalidade obtemos a melhor vantagem da Pesquisa do Twitter nos navegadores, ele pode pesquisar os mais antigos tweets.

## Pré-requisitos
Este pacote assume o uso do Python 2.x.

As dependências esperadas do pacote estão listadas no arquivo "requirements.txt" para PIP, você precisa executar o seguinte comando para obter dependências:

```
pip install -r requirements.txt
```

## Componentes
  - ** Tweet: ** Classe modelo para dar algumas informações sobre um tweet específico.
  - id (str)
  - permalink (str)
  - username (str)
  - text (str)
  - date (date)
  - retweets (int)
  - favorites (int)
  - mentions (str)
  - hashtags (str)
  - geo (str)

- **TweetManager:**  Classe que ajuda a obter tweets no modelo do ** Twitter **. 
  - getTweets (**TwitterCriteria**): Retorna a lista de tweets recuperados usando uma instância do ** TwitterCriteria **.

- **TwitterCriteria:** Parâmetros de pesquisa a serem usados ​​em conjunto com o ** TweetManager **.
  - setUsername (str): Um nome de usuário específico opcional de uma conta do Twitter. Sem "@".
  - setSince (str. "yyyy-mm-dd"): uma data inicial para restringir a pesquisa.
  - setUntil (str. "yyyy-mm-dd"):  uma data final superior para restringir a pesquisa.
  - setQuerySearch (str): Um texto de consulta a ser correspondido.
  - setTopTweets (bool): Se verdadeiro somente os Top Tweets serão recuperados.
  - setNear(str): uma área de geolocalização de referência de onde os tweets foram gerados.
  - setWithin (str): um raio de distância a partir da localização "próxima" (por exemplo, 15mi -- 15 milhas). 
  - setMaxTweets (int): o número máximo de tweets a serem recuperados. Se esse número não for definido ou menor que 1, todos os tweets possíveis serão recuperados.
  
- **Main:** Exemplos de como usar.

- **Exporter:** Exportar tweets para um arquivo csv chamado "output_got.csv".

## Exemplos de uso 
- Obter tweets por nome de usuário
``` python
	tweetCriteria = got.manager.TweetCriteria().setUsername('barackobama').setMaxTweets(1)
	tweet = got.manager.TweetManager.getTweets(tweetCriteria)[0]
	  
    print tweet.text
```    
- Obter tweets por pesquisa de texto
``` python
	tweetCriteria = got.manager.TweetCriteria().setQuerySearch('europe refugees').setSince("2015-05-01").setUntil("2015-09-30").setMaxTweets(1)
	tweet = got.manager.TweetManager.getTweets(tweetCriteria)[0]
	  
    print tweet.text
```    
- Obter tweets por nome de usuário e datas início e fim
``` python
	tweetCriteria = got.manager.TweetCriteria().setUsername("barackobama").setSince("2015-09-10").setUntil("2015-09-12").setMaxTweets(1)
	tweet = got.manager.TweetManager.getTweets(tweetCriteria)[0]
	  
    print tweet.text
```
- 10 últimos tweets de determinado usuário
``` python
	tweetCriteria = got.manager.TweetCriteria().setUsername("barackobama").setTopTweets(True).setMaxTweets(10)
	# first one
	tweet = got.manager.TweetManager.getTweets(tweetCriteria)[0]
	  
    print tweet.text
```

## Exemplos de uso de linha de comando
- Ajuda como utilizar
```
    python Exporter.py -h
``` 
- Obter tweets por nome de usuário
```
    python Exporter.py --username "barackobama" --maxtweets 1
```    
- Obter tweets por pesquisa de texto
```
    python Exporter.py --querysearch "europe refugees" --maxtweets 1
```    
- Obter tweets por nome de usuário e datas início e fim
```
    python Exporter.py --username "barackobama" --since 2015-09-10 --until 2015-09-12 --maxtweets 1
```
- 10 últimos tweets de determinado usuário
```
    python Exporter.py --username "barackobama" --maxtweets 10 --toptweets
```
