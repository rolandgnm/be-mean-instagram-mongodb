
# MongoDB - Aula 04 - Exercício
autor: Roland Gabriel

## **Adicionar** 2 ataques ao mesmo tempo para os seguintes pokemons: Pikachu, Squirtle, Bulbassauro e Charmander.
```javascript
be-mean-pokemons> p.find(q)
{
  "_id": ObjectId("564b1dad25337263280d047a"),
  "attack": 52,
  "created": "2013-11-03T15:05:41.271082",
  "defense": 43,
  "height": "6",
  "hp": 39,
  "name": "Charmander",
  "speed": 65,
  "types": [
    "fire"
  ],
  "moves": [
    "desvio"
  ],
  "description": "Essa é uma descrição legal!",
  "attacks": [
    "Attack 1",
    "Attack 2"
  ]
}
{
  "_id": ObjectId("564b1db125337263280d04a7"),
  "attack": 55,
  "created": "2013-11-03T15:05:41.317235",
  "defense": 40,
  "height": "4",
  "hp": 35,
  "name": "Pikachu",
  "speed": 90,
  "types": [
    "electric"
  ],
  "moves": [
    "desvio"
  ],
  "description": "Essa é uma descrição legal!",
  "attacks": [
    "Attack 1",
    "Attack 2"
  ]
}
{
  "_id": ObjectId("564b1db425337263280d04b6"),
  "attack": 48,
  "created": "2013-11-03T15:05:41.278310",
  "defense": 65,
  "height": "5",
  "hp": 44,
  "name": "Squirtle",
  "speed": 43,
  "types": [
    "water"
  ],
  "moves": [
    "desvio"
  ],
  "description": "Essa é uma descrição legal!",
  "attacks": [
    "Attack 1",
    "Attack 2"
  ]
}
{
  "_id": ObjectId("564b1de325337263280d068c"),
  "attack": 49,
  "created": "2013-11-03T15:05:41.260678",
  "defense": 49,
  "height": "7",
  "hp": 45,
  "name": "Bulbasaur",
  "speed": 45,
  "types": [
    "poison",
    "grass"
  ],
  "moves": [
    "desvio"
  ],
  "description": "Essa é uma descrição legal!",
  "attacks": [
    "Attack 1",
    "Attack 2"
  ]
}
Fetched 4 record(s) in 3ms

```



## **Adicionar** 1 movimento em todos os pokemons: `desvio`.##
```javascript
be-mean-pokemons> p.update(q,mod,options)
Updated 610 existing record(s) in 43ms
WriteResult({
  "nMatched": 610,
  "nUpserted": 0,
  "nModified": 610
})

```
```javascript
{
  "_id": ObjectId("564b1dae25337263280d048c"),
  "attack": 105,
  "created": "2013-11-03T15:05:41.452237",
  "defense": 75,
  "height": "12",
  "hp": 105,
  "name": "Muk",
  "speed": 50,
  "types": [
    "poison"
  ],
  "moves": [
    "desvio"
  ]
}

```

## **Adicionar** o pokemon `AindaNaoExisteMon` caso ele não exista com todos os dados com o valor `null` e a descrição: "Sem maiores informações".##
```javascript
q
{
 "name": /AindaNaoExisteMon/i
}

op
{
  "upsert": true
}
```
```javascript
mod
{
  "$setOnInsert": {
    "attack": null,
    "created": null,
    "defense": null,
    "height": null,
    "hp": null,
    "name": "AindaNaoExisteMon",
    "speed": null,
    "types": null,
    "moves": null,
    "description": "Sem maiores informações"
  }
}
```

```javascript
be-mean-pokemons> p.update(q,mod,op)
Updated 1 new record(s) in 1ms
WriteResult({
  "nMatched": 0,
  "nUpserted": 1,
  "nModified": 0,
  "_id": ObjectId("5651ed5106eae0cfc074d4e2")
})

```
```javascript
p.find(q)
{
  "_id": ObjectId("5651ed5106eae0cfc074d4e2"),
  "attack": null,
  "created": null,
  "defense": null,
  "height": null,
  "hp": null,
  "name": "AindaNaoExisteMon",
  "speed": null,
  "types": null,
  "moves": null,
  "description": "Sem maiores informações"
}

```



## Pesquisar todos o pokemons que possuam o ataque `investida` e mais um que você adicionou, escolha seu pokemon favorito.##
```javascript
be-mean-pokemons> q
{
  "attacks": {
    "$in": [
      /investida/i,
      /attack 1/i
    ]
  }
}
```

```javascript
be-mean-pokemons> p.find(q)
{
  "_id": ObjectId("564b1dad25337263280d047a"),
  "attack": 52,
  "created": "2013-11-03T15:05:41.271082",
  "defense": 43,
  "height": "6",
  "hp": 39,
  "name": "Charmander",
  "speed": 65,
  "types": [
    "fire"
  ],
  "moves": [
    "desvio"
  ],
  "description": "Essa é uma descrição legal!",
  "attacks": [
    "Attack 1",
    "Attack 2"
  ]
}

    ...
    {
      "_id": ObjectId("564b1dad25337263280d047b"),
      "attack": 64,
      "created": "2013-11-03T15:05:41.273462",
      "defense": 58,
      "height": "11",
      "hp": 58,
      "name": "Charmeleon",
      "speed": 80,
      "types": [
        "fire"
      ],
      "moves": [
        "desvio"
      ],
      "description": "Essa é uma descrição legal!",
      "attacks": [
        "investida"
      ]
    }
    Fetched 5 record(s) in 4ms

```


## Pesquisar **todos** os pokemons que possuam os ataques que você adicionou, escolha seu pokemon favorito.##
```javascript
be-mean-pokemons> q
{
  "attacks": {
    "$exists": true
  }
}

```
```javascript
be-mean-pokemons> p.find(q)
{
  "_id": ObjectId("564b1dad25337263280d047a"),
  "attack": 52,
  "created": "2013-11-03T15:05:41.271082",
  "defense": 43,
  "height": "6",
  "hp": 39,
  "name": "Charmander",
  "speed": 65,
  "types": [
    "fire"
  ],
  "moves": [
    "desvio"
  ],
  "description": "Essa é uma descrição legal!",
  "attacks": [
    "Attack 1",
    "Attack 2"
  ]
}
{
  "_id": ObjectId("564b1db125337263280d04a7"),
  "attack": 55,
  "created": "2013-11-03T15:05:41.317235",
  "defense": 40,
  "height": "4",
  "hp": 35,
  "name": "Pikachu",
  "speed": 90,
  "types": [
    "electric"
  ],
  "moves": [
    "desvio"
  ],
  "description": "Essa é uma descrição legal!",
  "attacks": [
    "Attack 1",
    "Attack 2"
  ]
}
{
  "_id": ObjectId("564b1db425337263280d04b6"),
  "attack": 48,
  "created": "2013-11-03T15:05:41.278310",
  "defense": 65,
  "height": "5",
  "hp": 44,
  "name": "Squirtle",
  "speed": 43,
  "types": [
    "water"
  ],
  "moves": [
    "desvio"
  ],
  "description": "Essa é uma descrição legal!",
  "attacks": [
    "Attack 1",
    "Attack 2"
  ]
}
{
  "_id": ObjectId("564b1de325337263280d068c"),
  "attack": 49,
  "created": "2013-11-03T15:05:41.260678",
  "defense": 49,
  "height": "7",
  "hp": 45,
  "name": "Bulbasaur",
  "speed": 45,
  "types": [
    "poison",
    "grass"
  ],
  "moves": [
    "desvio"
  ],
  "description": "Essa é uma descrição legal!",
  "attacks": [
    "Attack 1",
    "Attack 2"
  ]
}
{
  "_id": ObjectId("564b1dad25337263280d047b"),
  "attack": 64,
  "created": "2013-11-03T15:05:41.273462",
  "defense": 58,
  "height": "11",
  "hp": 58,
  "name": "Charmeleon",
  "speed": 80,
  "types": [
    "fire"
  ],
  "moves": [
    "desvio"
  ],
  "description": "Essa é uma descrição legal!",
  "attacks": [
    "investida"
  ]
}
Fetched 5 record(s) in 4ms

```

## Pesquisar **todos** os pokemons que não são do tipo `elétrico`.##
```javascript
q
{
  "types": {
    "$nin": [
      "electric"
    ]
  }
}

```
```javascript
be-mean-pokemons> p.find(q)
{
  "_id": ObjectId("564b1dad25337263280d047d"),
  "attack": 83,
  "created": "2013-11-03T15:05:41.282985",
  "defense": 100,
  "height": "16",
  "hp": 79,
  "name": "Blastoise",
  "speed": 78,
  "types": [
    "water"
  ],
  "moves": [
    "desvio"
  ],
  "description": "Essa é uma descrição legal!"
}
{
  "_id": ObjectId("564b1dad25337263280d047e"),
  "attack": 30,
  "created": "2013-11-03T15:05:41.285736",
  "defense": 35,
  "height": "3",
  "hp": 45,
  "name": "Caterpie",
  "speed": 45,
  "types": [
    "bug"
  ],
  "moves": [
    "desvio"
  ],
  "description": "Essa é uma descrição legal!"
}
{
  "_id": ObjectId("564b1dad25337263280d047c"),
  "attack": 63,
  "created": "2013-11-03T15:05:41.280718",
  "defense": 80,
  "height": "10",
  "hp": 59,
  "name": "Wartortle",
  "speed": 58,
  "types": [
    "water"
  ],
  "moves": [
    "desvio"
  ],
  "description": "Essa é uma descrição legal!"
}
{
  "_id": ObjectId("564b1dad25337263280d047f"),
  "attack": 20,
  "created": "2013-11-03T15:05:41.288107",
  "defense": 55,
  "height": "7",
  "hp": 50,
  "name": "Metapod",
  "speed": 30,
  "types": [
    "bug"
  ],
  "moves": [
    "desvio"
  ],
  "description": "Essa é uma descrição legal!"
}
{
  "_id": ObjectId("564b1dad25337263280d0479"),
  "attack": 56,
  "created": "2013-11-03T15:05:41.305777",
  "defense": 35,
  "height": "3",
  "hp": 30,
  "name": "Rattata",
  "speed": 72,
  "types": [
    "normal"
  ],
  "moves": [
    "desvio"
  ],
  "description": "Essa é uma descrição legal!"
}
    `...`
Fetched 20 record(s) in 46ms -- More[true]
```
count() dessa pesquisa

## Pesquisar **todos** os pokemons que tenham o ataque `investida` **E** tenham a defesa **não menor ou igual** a 49.##
```javascript
q
{
  "$and": [
    {
      "attacks": {
        "$in": [
          /investida/i
        ]
      }
    },
    {
      "defense": {
        "$not": {
          "$lte": 49
        }
      }
    }
  ]
}
```
```javascript
be-mean-pokemons> p.find(q)
{
  "_id": ObjectId("564b1dad25337263280d047b"),
  "attack": 64,
  "created": "2013-11-03T15:05:41.273462",
  "defense": 58,
  "height": "11",
  "hp": 58,
  "name": "Charmeleon",
  "speed": 80,
  "types": [
    "fire"
  ],
  "moves": [
    "desvio"
  ],
  "description": "Essa é uma descrição legal!",
  "attacks": [
    "investida"
  ]
}
Fetched 1 record(s) in 1ms

```

## Remova **todos** os pokemons do tipo água e com attack menor que 50.
```javascript
q
{
  "$and": [
    {
      "types": {
        "$in": [
          /water/i
        ]
      }
    },
    {
      "attack": {
        "$lt": 50
      }
    }
  ]
}
```

```javascript
be-mean-pokemons> p.remove(q)
Removed 21 record(s) in 4ms
WriteResult({
  "nRemoved": 21
})

```
