# MongoDB - Aula 01 - Exercício
autor: Roland Gabriel Nogueira Molina


## Importando os restaurantes

    ```
      Roland$ mongoimport -d be-mean -c restaurantes --drop --file ./data/restaurantes.json
    2015-11-14T17:03:46.210-0300	connected to: localhost
    2015-11-14T17:03:46.210-0300	dropping: be-mean.restaurantes
    2015-11-14T17:03:49.003-0300	imported 25359 documents

    ```

## Contando os restaurantes

    ```
    suissacorp(mongod-3.0.6) be-mean> db.restaurantes.find({}).count()
    X

    ```

    ```
    Roland(mongod-3.0.7) be-mean> db.restaurantes.count()
    25359
    
    ```
