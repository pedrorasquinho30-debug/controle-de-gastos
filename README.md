# Controle de Gastos

Esse projeto é um site para controlar os gastos do mês. A pessoa cria uma conta, entra com e-mail e senha e vai anotando o que gastou. O site mostra tudo organizado por dia, tipo um cronograma, e tem uma página de resumo para ver quanto foi gasto no total.

Eu usei o Firebase para fazer o login (Authentication), guardar os dados (Firestore) e colocar o site no ar (Hosting).

Site no ar: https://controle-de-gastos-43857.web.app

## O que o site faz

- **Início:** página inicial que explica o que é o site.
- **Registro:** cria uma conta com nome, e-mail e senha.
- **Entrar:** faz login com e-mail e senha. Tem também o botão de sair.
- **Gastos:** mostra os gastos do mês separados por dia, com o total de cada dia e o total do mês. Dá para trocar de mês com os botões de anterior e próximo.
- **Adicionar, editar e excluir gastos:** dá para adicionar um gasto novo e depois mudar o nome, o valor, a data ou a categoria. Também dá para excluir.
- **Resumo:** mostra o total do mês, a média por dia, quantos gastos foram feitos, uma comparação com o mês passado, os gastos por categoria, os 5 maiores gastos e um gráfico dos últimos 6 meses.

As páginas de Gastos e Resumo só abrem se a pessoa estiver logada. Se não estiver, o site manda para a página de login.

## Tecnologias usadas

- HTML, CSS e JavaScript (tudo no mesmo arquivo, sem framework)
- Firebase Authentication
- Cloud Firestore
- Firebase Hosting

## Arquivos do projeto

- `public/index.html`: o site inteiro (páginas, estilo e código).
- `firebase.json`: configuração do Hosting e do Firestore.
- `firestore.rules`: regras de segurança do banco de dados.
- `.firebaserc`: guarda qual projeto do Firebase está sendo usado.
- `prints/`: pasta com os prints ou o vídeo do site funcionando.

## Como os dados são guardados

Cada gasto fica salvo no Firestore em `users/{id do usuário}/expenses`. Cada gasto tem nome, valor, data e categoria. Nas regras do banco, deixei que cada usuário só consiga ver e mexer nos próprios gastos.

O CRUD funciona assim:

- **Criar:** quando preenche o formulário de novo gasto (`addDoc`).
- **Ler:** a lista de gastos é carregada e atualiza sozinha (`onSnapshot`).
- **Atualizar:** no botão Editar (`updateDoc`).
- **Deletar:** no botão Excluir (`deleteDoc`).

## Como rodar no computador

Precisa ter o [Node.js](https://nodejs.org) instalado.

1. Baixe o projeto e abra um terminal dentro da pasta `controle-de-gastos`.

2. Instale o Firebase CLI e faça login na sua conta do Google:
   ```
   npm install -g firebase-tools
   firebase login
   ```

3. No [console do Firebase](https://console.firebase.google.com), abra o projeto e faça duas coisas:
   - Em Authentication, ative o método de login por **E-mail/senha**.
   - Em Firestore Database, clique em **Criar banco de dados**.

4. Para abrir o site localmente, rode:
   ```
   firebase emulators:start --only hosting
   ```
   Depois abra o endereço que aparecer no terminal (geralmente http://localhost:5000).

   Se não quiser usar o Firebase CLI para isso, também dá para rodar `npx serve public`.

O site local usa o Authentication e o Firestore do projeto que está configurado dentro do `public/index.html`, na parte do `firebaseConfig`. Se quiser usar outro projeto do Firebase, é só trocar esses dados pelos do seu app web.

## Como publicar

Dentro da pasta do projeto, rode:

```
firebase deploy
```

Isso envia o site e também as regras do Firestore para o Firebase.


