<h1 align="center">
  Help my plants - API
</h1>

<p align = "center">
Este é o backend da aplicação Help my plants. O objetivo dessa aplicação é educar e auxiliar os usuários a cuidarem das suas plantas, saber dos seus benefícios e incentivar as pessoas a terem mais plantas.

</p>

## **Endpoints**

A API tem um total de 7 endpoints, sendo em volta principalmente do usuário - podendo cadastrar seu perfil, acessar a database das plantas, adicionar as plantas em seu perfil, atualizar as informações das plantas já registradas em seu perfil e deletar as plantas que estão em seu perfil. 
<br/>
                    
O url base da API é https:/help-my-plants-backend.herokuapp.com/

---

## Rotas que não necessitam de autorização 🔓

<h2 align ='center'> Criação de usuário </h2>
<br/>

POST /users : Cadastrar usuários, 600

1. O campo - "email" e "password" são obrigatórios.
   
2. O campo "password" necessita de no mínimo 6 caracteres.

3. Os campos - "name", "interest" são opcionais.


4. O campo "interest" deve receber o interesse do usuário, devendo ser escrito dessa forma:
   1. "Hobby"                           
   2. "Estudante"
   3. "Profissional"

`POST /users  -  FORMATO DA REQUISIÇÃO `
```json
    {
      "email": "emaildousuario@email.com",
      "password": "123456",
      "name": "João Silva",
      "interest": "Hobby"
    }
```

Caso dê tudo certo, a resposta será assim:

`POST /users  -  FORMATO DA RESPOSTA - STATUS 201 `
```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJl1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImVtYWlsZG91c3VhcmlvQGVtY",
  "user": {
    "email": "emaildousuario@email.com",
    "name": "João Silva",
    "interest": "Hobby",
    "id": 8
  }
}
```

Caso Email já cadastrado:

`STATUS 400`

```
"Email already exists"
```

---

<h2 align ='center'> Login </h2>
<br/>

POST /login - Login do usuário, 600

1 - Para executar o login é necessário do email e senha.

`POST /login  -  FORMATO DA REQUISIÇÃO `
```json
    {
      "email": "emaildousuario@email.com",
      "password": "123456"
    }
```

Caso dê tudo certo, a resposta será assim:

`POST /login  -  FORMATO DA RESPOSTA - STATUS 200`
```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJl1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImVtYWlsZG91c3VhcmlvQGVtY",
  "user": {
    "email": "emaildousuario@email.com",
    "name": "João Silva",
    "interest": "Hobby",
    "id": 8
  }
}
```
Caso dê errado e o usuário não for cadastrado apresentará:

`STATUS 400`

```
"Cannot find user"
```
Caso a senha estiver incorreta

`STATUS 400`

```
"Incorrect password"
```

---
<br/>

## Rotas que necessitam de autorização 🔐 

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

Após o usuário estar logado, ele deve conseguir ter acesso ao database das plantas cadastradas.

<h2 align ='center'> Listando plantas </h2>
<br/>

GET /plants - Database das plantas cadastradas, 600

`GET /plants  -  FORMATO DA RESPOSTA - STATUS 200  `
```json
[
  {
    "name": "Samambaia",
    "cientific_name": "Phlebodium decumanum",
    "water": 1,
    "lighting": {
      "min": 1,
      "max": 2
    },
    "temperature": {
      "min": 15,
      "max": 30
    },
    "height": {
      "min": 80,
      "max": 120
    },
    "info": "Formam moitas volumosas por isso são ideais para colocar em vasos suspensos ou no alto de uma parede, para criar um jardim vertical. A samambaia se adapta perfeitamente a ambientes com o tipo de iluminação meia-sombra e não deve pegar muito vento.",
    "image": "https://ibb.co/1JJXwsg"
  },
  {
    "name": "Espada de São Jorge",
    "cientific_name": "Dracaena trifasciata",
    "water": 7,
    "lighting": {
      "min": 0,
      "max": 1
    },
    "temperature": {
      "min": 15,
      "max": 30
    },
    "height": {
      "min": 60,
      "max": 100
    },
    "info": "Com folhas longas e achatadas, a Espada de São Jorge é uma ótima escolha para quem não tem muito tempo para dedicar às plantas, pois ela não exige muitos cuidados. Além disso, se adapta bem a ambientes com ar-condicionado.",
    "image": "https://ibb.co/xSYMzw6"
  }
]

```

---

<h2 align ='center'> Listando plantas do usuário </h2>
<br/>
GET /userPlants - Recebe a lista de todas as plantas vinculadas ao usuário, 660

`GET /userPlants  -  FORMATO DA RESPOSTA - STATUS 200  `
```json
[
  {
    "name": "Samambaia",
    "cientific_name": "Phlebodium decumanum",
    "water": 1,
    "lighting": {
      "min": 1,
      "max": 2
    },
    "temperature": {
      "min": 15,
      "max": 30
    },
    "height": {
      "min": 80,
      "max": 120
    },
    "info": "Formam moitas volumosas por isso são ideais para colocar em vasos suspensos ou no alto de uma parede, para criar um jardim vertical. A samambaia se adapta perfeitamente a ambientes com o tipo de iluminação meia-sombra e não deve pegar muito vento.",
    "image": "https://ibb.co/1JJXwsg"
  },
  {
    "name": "Espada de São Jorge",
    "cientific_name": "Dracaena trifasciata",
    "water": 7,
    "lighting": {
      "min": 0,
      "max": 1
    },
    "temperature": {
      "min": 15,
      "max": 30
    },
    "height": {
      "min": 60,
      "max": 100
    },
    "info": "Com folhas longas e achatadas, a Espada de São Jorge é uma ótima escolha para quem não tem muito tempo para dedicar às plantas, pois ela não exige muitos cuidados. Além disso, se adapta bem a ambientes com ar-condicionado.",
    "image": "https://ibb.co/xSYMzw6"
  }
]

```

---

<h2 align ='center'> Vinculando plantas ao usuário </h2>
<br/>
POST /userPlants/?userId  -  Permite ao usuário adicionar plantas em seu perfil.


`POST /userPlants/?userId  -  FORMATO DA REQUISIÇÃO `
```json
[
  {
    "name": "Samambaia",
    "cientific_name": "Phlebodium decumanum",
    "water": 1,
    "lighting": {
        "min": 1,
        "max": 2
    },
    "temperature": {
        "min": 15,
        "max": 30
    },
    "height": {
        "min": 80,
        "max": 120
    },
    "info": "Formam moitas volumosas por isso são ideais para colocar em vasos suspensos ou no alto de uma parede, para criar um jardim vertical. A samambaia se adapta perfeitamente a ambientes com o tipo de iluminação meia-sombra e não deve pegar muito vento.",
    "image": "https://ibb.co/1JJXwsg",
  }
]

```

Caso dê tudo certo, a resposta será assim:

`PPOST /userPlants/?userId  -  FORMATO DA RESPOSTA - STATUS 200`
```json
[
  {
    "userID": 6,
    "name": "Samambaia",
    "cientific_name": "Phlebodium decumanum",
    "water": 1,
    "lighting": {
        "min": 1,
        "max": 2
    },
    "temperature": {
        "min": 15,
        "max": 30
    },
    "height": {
        "min": 80,
        "max": 120
    },
    "info": "Formam moitas volumosas por isso são ideais para colocar em vasos suspensos ou no alto de uma parede, para criar um jardim vertical. A samambaia se adapta perfeitamente a ambientes com o tipo de iluminação meia-sombra e não deve pegar muito vento.",
    "image": "https://ibb.co/1JJXwsg",
    "id": 1
  }
]

```

---

<h2 align ='center'> Atualizando informações das plantas do usuário </h2>
<br/>
PATCH /userPlants/:plants_id -  Permite ao usuário atualizar as informações de plantas já registradas em seu perfil.

`PATCH /userPlants/:plants_id  -  FORMATO DA RESPOSTA - STATUS 200  `
```json
{
  "name": "Samambaia Americana",
  "cientific_name": "Phlebodium decumanum",
  "water": 1,
  "lighting": {
    "min": 1,
    "max": 2
  },
  "temperature": {
    "min": 15,
    "max": 30
  },
  "height": {
    "min": 80,
    "max": 120
  },
  "info": "Formam moitas volumosas por isso são ideais para colocar em vasos suspensos ou no alto de uma parede, para criar um jardim vertical. A samambaia se adapta perfeitamente a ambientes com o tipo de iluminação meia-sombra e não deve pegar muito vento.",
  "image": "https://ibb.co/1JJXwsg",
  "id": 1
}

```

Caso passe o ID errado ou inválido apresentará:

`STATUS 404`

---

<h2 align ='center'> Deletando planta vinculada ao usuário</h2>
<br/>
DELETE /userPlants/:plants_id -  Permite ao usuário atualizar as informações de plantas já registradas em seu perfil.

`DELETE /userPlants/:plants_id  -  FORMATO DA RESPOSTA - STATUS 200  `
```
Não é necessário um corpo da requisição.
```
--------------------------------------------------