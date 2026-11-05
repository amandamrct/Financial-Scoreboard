# Colocar o Placar no ar com login e dados na nuvem

Sem configurar nada, o Placar salva só no navegador em que foi aberto. Com este guia, ele passa a ter login e a guardar os dados no Firebase, abrindo igual no celular e no computador. Firebase e Netlify têm planos gratuitos que sobram para uso pessoal.

## 1. Criar o projeto no Firebase

1. Entre em **console.firebase.google.com** com uma conta Google.
2. Toque em **Criar projeto**, dê um nome (por exemplo, `placar-financeiro`) e pode desligar o Google Analytics.

## 2. Ligar o login por e-mail e senha

1. No menu: **Criação › Authentication › Vamos começar**.
2. Em "Método de login", escolha **E-mail/senha**, ative a primeira chave e salve.

## 3. Criar o banco de dados e proteger

1. No menu: **Criação › Firestore Database › Criar banco de dados**.
2. Local: **southamerica-east1 (São Paulo)**. Modo: **produção**.
3. Na aba **Regras**, cole o conteúdo de [`firestore.rules`](firestore.rules), troque o e-mail pelo seu e toque em **Publicar**.

## 4. Colar as chaves no app

1. Na tela inicial do projeto, toque no ícone **</>** (Web), dê um apelido e toque em **Registrar app**. Não marque o Firebase Hosting.
2. Copie `apiKey`, `authDomain`, `projectId` e `appId` do bloco `firebaseConfig`.
3. Abra o `index.html` num editor de texto, procure **CONFIGURAÇÃO DO SEU SITE** e preencha:

```js
window.APP_CONFIG = {
  email: "voce@exemplo.com",
  firebase: {
    apiKey: "...",
    authDomain: "seu-projeto.firebaseapp.com",
    projectId: "seu-projeto",
    appId: "..."
  }
};
```

Essas chaves não são senha: ficam visíveis em qualquer site que usa Firebase. Quem protege os dados são as regras do passo 3.

## 5. Publicar

**GitHub Pages:** no repositório, **Settings › Pages**, em "Branch" escolha `main` e a pasta `/ (root)` e salve. Em alguns minutos o site fica em `https://SEU-USUARIO.github.io/Financial-Scoreboard/`.

**Netlify (opcional, para domínio próprio):** arraste a pasta em **app.netlify.com/drop**. Depois, em **Domain management › Add a domain**, informe o seu domínio e crie no painel de DNS o registro **CNAME** que o Netlify indicar. Não altere os registros MX e TXT que já existem: são eles que fazem o e-mail funcionar.

## 6. Primeiro acesso

1. Abra o site, digite o e-mail e uma senha nova e toque em **Criar meu acesso**.
2. Toque em **Carregar fixos de exemplo** e ajuste para os seus, ou em **Restaurar backup** se já usava o app.
3. Em **Dinheiro em conta**, informe o saldo atual de cada banco.

## 7. Virar "aplicativo" no celular

- **iPhone (Safari):** Compartilhar › **Adicionar à Tela de Início**.
- **Android (Chrome):** menu ⋮ › **Adicionar à tela inicial**.
