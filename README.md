# vida — app de hábitos (PWA)

App de acompanhamento de hábitos (exercício, estudo, dieta, água e sono) para
Henrique e Júlia. Funciona como site e pode ser **instalado** no Android e no
iPhone como um app, hospedado de graça no **GitHub Pages**.

## Conteúdo do projeto

```
vida/
├── index.html              ← o app
├── manifest.json           ← configuração do PWA (nome, ícones)
├── sw.js                   ← service worker (uso offline / instalável)
├── Codigo.gs               ← script do Google Sheets (opcional, p/ salvar na planilha)
└── assets/
    ├── icon-192.png        ← ícone do app
    ├── icon-512.png        ← ícone do app
    ├── apple-touch-icon.png← ícone do app (iPhone)
    ├── henrique.png        ← imagem do perfil Henrique (elefante)
    └── julia.png           ← imagem do perfil Júlia (suricato)
```

> As imagens `henrique.png` e `julia.png` são **placeholders**. Troque-as
> pelas suas (mesmo nome e pasta). O ideal é PNG quadrado com fundo
> transparente. Os ícones do app foram gerados a partir do seu logo.

---

## 1) Publicar no GitHub Pages

1. Crie uma conta no GitHub (se ainda não tiver) e clique em **New repository**.
   Dê um nome, por exemplo `vida`, e deixe **Public**. Crie o repositório.
2. Na página do repositório, clique em **Add file → Upload files**.
3. Arraste **todo o conteúdo da pasta `vida`** (o `index.html`, o
   `manifest.json`, o `sw.js` e a pasta `assets` com as imagens).
   Importante: o `index.html` precisa ficar na **raiz** do repositório, e as
   imagens dentro de **`assets/`**. Clique em **Commit changes**.
4. Vá em **Settings → Pages**.
5. Em **Build and deployment → Source**, escolha **Deploy from a branch**.
   Em **Branch**, selecione **main** e a pasta **/ (root)**. Clique em **Save**.
6. Aguarde ~1 minuto. O endereço do app aparece no topo dessa mesma página,
   algo como:
   `https://SEU-USUARIO.github.io/vida/`
7. Abra esse endereço no navegador. Pronto — o app está no ar.

---

## 2) Instalar no celular (vira "app" na tela inicial)

**Android (Chrome):**
1. Abra o endereço do app no Chrome.
2. Toque no menu **⋮** (canto superior direito).
3. Toque em **Instalar app** (ou **Adicionar à tela inicial**).
4. Confirme. O ícone do *vida* aparece na tela inicial e abre em tela cheia.

**iPhone / iPad (Safari):**
1. Abra o endereço do app no **Safari** (precisa ser o Safari).
2. Toque no botão **Compartilhar** (quadrado com seta para cima).
3. Role e toque em **Adicionar à Tela de Início**.
4. Toque em **Adicionar**. O ícone do *vida* aparece na tela inicial.

> Depois de instalado, ele funciona mesmo offline (os dados ficam no próprio
> aparelho). Para sincronizar entre celulares, conecte à planilha (passo 3).

---

## 3) (Opcional) Conectar à planilha do Google Sheets

Sem esta etapa o app já funciona, guardando os dados no próprio navegador.
Para que Henrique e Júlia compartilhem os mesmos dados, conecte à planilha:

1. Abra a planilha no Google Sheets → **Extensões → Apps Script**.
2. Apague o conteúdo e cole o arquivo **`Codigo.gs`**. Salve.
3. **Implantar → Nova implantação → App da Web**:
   - *Executar como:* **Eu**
   - *Quem tem acesso:* **Qualquer pessoa**
   - Implante e autorize. Copie a URL que termina em **`/exec`**.
4. Abra o `index.html`, e na 1ª linha do `<script>` cole a URL:
   ```js
   const CONFIG = { API_URL: "https://script.google.com/macros/s/XXXX/exec" };
   ```
5. Envie o `index.html` atualizado para o GitHub novamente (Upload files →
   Commit). Pronto: o app passa a ler e gravar direto na planilha.

**Formato das abas** (linha 4 = cabeçalho; registros a partir da linha 5):

| B | C | D | E | F | G | H | I | J |
|---|---|---|---|---|---|---|---|---|
| Data | Exercício | Dieta: Café | Dieta: Almoço | Dieta: Lanche | Dieta: Jantar | Água | Estudo | Sono |

- Deixe as abas **"Henrique"** e **"Júlia"** com esses mesmos cabeçalhos.
- **Água** e **Sono** devem ser colunas livres (número), sem validação de lista.
- O script localiza as colunas pelo nome, então funciona mesmo que falte
  alguma — as que faltarem ficam vazias até você adicioná-las.

---

## Atualizando o app depois

Qualquer mudança é só subir o arquivo novo para o GitHub (Upload files →
Commit). O GitHub Pages republica sozinho em segundos. Se o celular não
atualizar na hora, feche e reabra o app (o service worker troca a versão).
