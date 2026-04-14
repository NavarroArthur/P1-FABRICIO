# Prova P1 — Banco de Dados Não Relacionais

**Disciplina:** Banco de Dados Não Relacionais  
**Aluno:** Arthur Navarro Azevedo Romariz Reis  
**Matrícula:** 202413706  
**Professor:** Fabricio Dias  
**Data:** 14/04/2026  

---

##  Descrição do Exercício

Prova individual utilizando **Docker + MongoDB** com as seguintes ferramentas permitidas:
- `mongosh` ou **MongoDB Compass**

### Requisitos de entrega:
- Comandos utilizados
- Prints dos resultados
- Entrega via **GitHub**

---

## Estrutura do Banco de Dados

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

<img width="1145" height="264" alt="image1" src="https://github.com/user-attachments/assets/e224a6d1-1d84-4d30-aa03-b3b581cf0968" />


---

### Conexão ao MongoDB Compass

Conexão realizada via **MongoDB Compass** ao `localhost` configurado no Docker Compose (porta padrão).

<img width="841" height="428" alt="image2" src="https://github.com/user-attachments/assets/08764159-b1bf-4a51-a561-58eefc404823" />


---

### Inserção dos Alunos

Os 5 alunos foram inseridos na collection `alunos` pelo recurso **ADD DATA** do MongoDB Compass.

<img width="445" height="752" alt="image3" src="https://github.com/user-attachments/assets/492136d3-1f40-44f8-baee-8e1203b1dcb5" />
<img width="343" height="186" alt="image4" src="https://github.com/user-attachments/assets/b81a5445-8746-4ffe-85f1-26dbccc40d19" />


---

## 🔍 Consultas Realizadas

### 1. Buscar todos os alunos

```js
db.alunos.find()
```

<img width="481" height="704" alt="image5" src="https://github.com/user-attachments/assets/60006f36-244f-49db-b60a-66d4cde4d2be" />
<img width="335" height="909" alt="image6" src="https://github.com/user-attachments/assets/0ce9e1bc-0f6e-4bd9-b2e9-929d422216f8" />


---

### 2. Buscar alunos do curso "ADS"

```js
db.alunos.find({ curso: "ADS" })
```

<img width="786" height="992" alt="image7" src="https://github.com/user-attachments/assets/1ff1818e-31a4-4074-b093-5ad75bfdd805" />


---

### 3. Buscar alunos com idade maior que 21

```js
db.alunos.find({ idade: { $gt: 21 } })
```

<img width="569" height="901" alt="image8" src="https://github.com/user-attachments/assets/fd2c7f50-54ae-43b1-8763-05be773826e9" />
<img width="398" height="627" alt="image9" src="https://github.com/user-attachments/assets/9b783caa-a50c-4236-96b1-c92df1563d27" />

---

### 4. Atualizar a idade de um aluno

```js
db.alunos.updateOne(
  { nome: "Nome do Aluno" },
  { $set: { idade: <nova_idade> } }
)
```

<img width="272" height="224" alt="image10" src="https://github.com/user-attachments/assets/d7397431-d972-418e-8915-b3dc0bb24e0e" />


---

### 5. Adicionar uma nova nota a um aluno

```js
db.alunos.updateOne(
  { nome: "Nome do Aluno" },
  { $push: { notas: <nova_nota> } }
)
```

<img width="366" height="226" alt="image11" src="https://github.com/user-attachments/assets/348fbfd8-73d5-41cb-b411-e56d12667f54" />


---

### 6. Remover um aluno

```js
db.alunos.deleteOne({ nome: "Nome do Aluno" })
```

<img width="350" height="104" alt="image12" src="https://github.com/user-attachments/assets/ae0ce2a8-9769-40d4-a7e7-522ba6d985cc" />


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

<img width="452" height="560" alt="image13" src="https://github.com/user-attachments/assets/45f0632a-1e70-47d1-9c58-54f9a260c244" />


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

<img width="384" height="364" alt="image14" src="https://github.com/user-attachments/assets/525e1709-8e86-49ef-8b57-9f6e31051ab3" />

---

##  Observação

> Caso haja provas iguais, a nota será **zero**.
