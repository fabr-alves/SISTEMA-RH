# CSVA RH

Sistema de controle operacional e RH, pronto para ser versionado no GitHub e publicado como site estático no Vercel.

## Estrutura

- `index.html`: aplicação completa.
- `mapa-ferias.html`: módulo independente exibido na nova aba **Mapa de Férias**.
- `vercel.json`: configuração do site no Vercel.
- `firestore.rules`: regras de acesso do Cloud Firestore.
- `firebase.json` e `.firebaserc`: configuração opcional para publicar as regras pelo Firebase CLI.

## 1. Publicar no GitHub

1. Crie um repositório vazio no GitHub.
2. Envie todos os arquivos desta pasta para a raiz do repositório.
3. Use a branch `main` como branch principal.

Também é possível fazer o primeiro envio por terminal:

```bash
git init
git add .
git commit -m "Publica CSVA RH"
git branch -M main
git remote add origin URL_DO_SEU_REPOSITORIO
git push -u origin main
```

## 2. Publicar no Vercel

1. No painel do Vercel, clique em **Add New > Project**.
2. Importe o repositório criado no GitHub.
3. Em **Framework Preset**, selecione **Other**.
4. Não informe comando de build.
5. Mantenha a raiz do repositório como diretório do projeto.
6. Clique em **Deploy**.

O sistema é formado por HTML e JavaScript executados no navegador, portanto não necessita de etapa de build.

O arquivo `mapa-ferias.html` deve permanecer na mesma pasta do `index.html`. O mapa mantém seu próprio cadastro, períodos de férias e backup local, sem remover ou modificar os módulos anteriores do CSVA RH.

## 3. Autorizar o domínio no Firebase

Depois do primeiro deploy, copie o domínio fornecido pelo Vercel, semelhante a:

```text
nome-do-projeto.vercel.app
```

No Firebase Console:

1. Abra **Authentication**.
2. Entre em **Settings > Authorized domains**.
3. Clique em **Add domain**.
4. Adicione somente o domínio, sem `https://` e sem barras.
5. Confirme que o método **Email/Password** está habilitado em **Sign-in method**.

Se posteriormente configurar um domínio próprio, adicione esse domínio também.

## 4. Publicar as regras do Firestore

As regras são necessárias para que somente usuários aprovados acessem os dados e para que o menu administrativo permaneça protegido.

### Pelo Firebase Console

1. Abra **Firestore Database > Rules**.
2. Copie todo o conteúdo de `firestore.rules`.
3. Clique em **Publish**.

### Pelo Firebase CLI

Com o Firebase CLI instalado e autenticado:

```bash
firebase deploy --only firestore:rules
```

## Administrador

O menu **Acessos** é liberado exclusivamente para a conta administrativa configurada no sistema. A senha não fica armazenada neste repositório.

## Atualizações futuras

Depois que o GitHub estiver conectado ao Vercel, cada atualização enviada para a branch principal criará automaticamente uma nova publicação.
