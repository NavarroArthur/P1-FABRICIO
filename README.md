# Prova P1 — Banco de Dados Não Relacionais

**Disciplina:** Banco de Dados Não Relacionais  
**Aluno:** Arthur Navarro Azevedo Romariz Reis  
**Matrícula:** 202413706  
**Professor:** Fabricio Dias  
**Data:** 14/04/2026  

---

## 📋 Descrição do Exercício

Prova individual utilizando **Docker + MongoDB** com as seguintes ferramentas permitidas:
- `mongosh` ou **MongoDB Compass**

### Requisitos de entrega:
- Comandos utilizados
- Prints dos resultados
- Entrega via **GitHub**

---

## 🗄️ Estrutura do Banco de Dados

- **Banco:** `escola` *(renomeado para `faculdadedevassourasmarica` para diferenciação)*
- **Collection:** `alunos`

### Modelo de documento:

```json
{
  "nome": "João Silva",
  "idade": 20,
  "curso": "ADS",
  "notas": [7, 8, 9],
  "endereço": {
    "cidade": "Maricá",
    "estado": "RJ"
  }
}
```

---

## 🛠️ Resolução

### Configuração do Docker Compose

Foi criado um **Docker Compose** para executar o MongoDB. O banco foi nomeado `faculdadedevassourasmarica` para diferenciá-lo do nome genérico solicitado (`escola`).

![Docker Compose](images/image1.png)

---

### Conexão ao MongoDB Compass

Conexão realizada via **MongoDB Compass** ao `localhost` configurado no Docker Compose (porta padrão).

![Conexão MongoDB Compass](images/image2.png)

---

### Inserção dos Alunos

Os 5 alunos foram inseridos na collection `alunos` pelo recurso **ADD DATA** do MongoDB Compass.

![Alunos inseridos - parte 1](images/image3.png)

![Alunos inseridos - parte 2](images/image4.png)

---

## 🔍 Consultas Realizadas

### 1. Buscar todos os alunos

```js
db.alunos.find()
```

![Buscar todos os alunos - parte 1](images/image5.png)

![Buscar todos os alunos - parte 2](images/image6.png)

---

### 2. Buscar alunos do curso "ADS"

```js
db.alunos.find({ curso: "ADS" })
```

![Buscar alunos do curso ADS](images/image7.png)

---

### 3. Buscar alunos com idade maior que 21

```js
db.alunos.find({ idade: { $gt: 21 } })
```

![Buscar alunos com idade > 21 - parte 1](images/image8.png)

![Buscar alunos com idade > 21 - parte 2](images/image9.png)

---

### 4. Atualizar a idade de um aluno

```js
db.alunos.updateOne(
  { nome: "Nome do Aluno" },
  { $set: { idade: <nova_idade> } }
)
```

![Atualizar idade de um aluno](images/image10.png)

---

### 5. Adicionar uma nova nota a um aluno

```js
db.alunos.updateOne(
  { nome: "Nome do Aluno" },
  { $push: { notas: <nova_nota> } }
)
```

![Adicionar nova nota](images/image11.png)

---

### 6. Remover um aluno

```js
db.alunos.deleteOne({ nome: "Nome do Aluno" })
```

![Remover um aluno](images/image12.png)

---

### 7. Média de notas por aluno

```js
db.alunos.aggregate([
  {
    $project: {
      nome: 1,
      media: { $avg: "$notas" }
    }
  }
])
```

![Média de notas por aluno](images/image13.png)

---

### 8. Quantidade de alunos por curso

```js
db.alunos.aggregate([
  {
    $group: {
      _id: "$curso",
      quantidade: { $sum: 1 }
    }
  }
])
```

![Quantidade de alunos por curso](images/image14.png)

---

## ⚠️ Observação

> Caso haja provas iguais, a nota será **zero**.
