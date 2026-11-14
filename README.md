# Site Bashtree

Site de página única da Bashtree, com painel administrador (Decap CMS) para editar textos e imagens.

## Estrutura

| Pasta/arquivo | O que é |
|---|---|
| `index.html` | Estrutura da página e formulário de contato |
| `css/style.css` | Visual (cores, fontes, layout) |
| `js/main.js` | Lê os textos da pasta `content/` e monta a página |
| `content/*.json` | **Textos do site**, editados pelo painel |
| `images/` | Logotipo e imagens enviadas pelo painel (`images/uploads`) |
| `admin/` | Painel administrador (`/admin`) |
| `netlify.toml` | Configuração do Netlify |
| `docs/` | Anotações do projeto (não ficam públicas) |

## Rodar no computador

```bash
python -m http.server 8080
```
Abra http://localhost:8080. O formulário só envia de verdade depois de publicado no Netlify.

---

## Publicar no Netlify (passo a passo)

### 1. Colocar o código no GitHub
1. Crie uma conta em https://github.com (gratuita).
2. Crie um repositório chamado **site-Bashtree** (pode ser privado).
3. Envie os arquivos desta pasta para o repositório (com Git ou pelo botão *Add file → Upload files*). Não envie a pasta `.claude`.

### 2. Ajustar o painel
Em `admin/config.yml`, troque:
- `repo: laurosampaio78-ops/site-Bashtree` pelo seu usuário do GitHub;
- `site_url` e `display_url` pelo endereço final do site no Netlify.

### 3. Criar o site no Netlify
1. Crie uma conta em https://app.netlify.com (pode entrar com o GitHub).
2. **Add new project → Import an existing project → GitHub** e escolha o repositório **site-Bashtree**.
3. Deixe o *build command* vazio e o *publish directory* como `.` e clique em **Deploy**.
4. Em **Project configuration → Change project name**, use `bashtree` (o site fica em `bashtree.netlify.app`, se o nome estiver livre).

### 4. Ativar o login do painel (GitHub)
1. No GitHub: **Settings → Developer settings → OAuth Apps → New OAuth App**
   - Homepage URL: `https://bashtree.netlify.app`
   - Authorization callback URL: `https://api.netlify.com/auth/done`
2. Copie o **Client ID** e gere um **Client secret**.
3. No Netlify: **Project configuration → Access & security → OAuth → Install provider → GitHub** e cole os dois códigos.
4. Acesse `https://bashtree.netlify.app/admin` e clique em **Entrar com o GitHub**.

### 5. Receber os contatos por e-mail
1. No Netlify: **Forms → Enable form detection** e faça um novo deploy (*Deploys → Trigger deploy*).
2. Envie um teste pelo site.
3. Em **Forms → Form notifications → Add notification → Email notification**, informe o e-mail que vai receber os contatos.

O plano gratuito do Netlify aceita até 100 envios de formulário por mês.

### 6. Domínio próprio (depois)
Em **Domain management → Add a domain**, informe `bashtree.com.br` e siga as instruções de DNS no Registro.br.

## Como editar o site
1. Acesse `/admin` e entre com o GitHub.
2. Abra **Conteúdo do site** e escolha a seção.
3. Altere textos ou envie imagens e clique em **Publicar**.
4. Em cerca de 1 minuto o site atualiza sozinho.
