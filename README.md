# Controle de Devoluções — J&T

Sistema operacional para cadastro de ocorrências e liberação automática de pacotes para devolução.

**Com Firebase:** você e outra pessoa veem os mesmos dados em tempo real.

## Link online (GitHub Pages)

https://anderson390285.github.io/controle-devolucoes/

> Ative em: Settings → Pages → Source: **main** / **(root)**

---

## Configurar Firebase (obrigatório para compartilhar dados)

### 1. Criar o projeto
1. Acesse https://console.firebase.google.com
2. Clique em **Adicionar projeto** (ou "Create project")
3. Nome: `controle-devolucoes` (ou outro)
4. Pode desativar o Google Analytics
5. Criar projeto

### 2. Registrar o app Web
1. Na tela do projeto, clique no ícone **</>** (Web)
2. Apelido: `devolucoes-web`
3. **Não** marque Firebase Hosting (já usamos GitHub Pages)
4. Clique em **Registrar app**
5. **Copie** o objeto `firebaseConfig` que aparece (apiKey, projectId, etc.)

### 3. Ativar o Firestore
1. No menu lateral: **Build → Firestore Database**
2. **Criar banco de dados**
3. Escolha **Começar no modo de produção** (vamos ajustar as regras)
4. Local: `southamerica-east1` (São Paulo) ou o mais próximo

### 4. Regras de segurança (uso interno)
1. Aba **Regras**
2. Cole isto e publique:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

> ⚠️ Qualquer pessoa com o link do site consegue ler/escrever.  
> Serve para uso interno da equipe. Não divulgue o link publicamente.

### 5. Colar a configuração no sistema
1. Abra o arquivo `index.html` no GitHub (ou baixe e edite)
2. Procure por `firebaseConfig` (perto do início do `<script>`)
3. Substitua os valores `COLE_AQUI` pelos do seu projeto
4. Salve e faça commit (ou peça para o Grok atualizar no GitHub)

### 6. Testar
1. Abra o link do Pages no **seu** computador e no da outra pessoa
2. Cadastre um pacote em um lado
3. Em poucos segundos deve aparecer no outro (status verde: **Sincronizado com a nuvem**)

---

## Funcionalidades

- Cadastro de ocorrências (endereço incorreto, recusa, ausência, mudança, impossibilidade)
- Cálculo automático da data de liberação
- Controle de ausência 1/3, 2/3 e 3/3
- Registro de devoluções recebidas (motorista + base)
- Filtros, busca e exportação CSV
- **Sincronização em tempo real via Firebase** (quando configurado)
- Fallback em modo local (localStorage) se o Firebase não estiver configurado

## Bases

- F ATG-BA
- F ITI-BA
- F SBM-BA
