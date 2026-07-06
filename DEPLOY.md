# NEXUS HOME — Deploy no GitHub + Vercel

## Arquivos deste pacote
- `index.html` — o app completo (com as melhorias visuais e correções aplicadas)
- `manifest.json` — configuração do PWA (nome, ícones, tela cheia)
- `sw.js` — service worker (cache básico + instalação como app)
- `icon-192.png` / `icon-512.png` — ícones gerados para o app
- `vercel.json` — headers de permissão explícitos para câmera/microfone/localização

## Passo a passo

### 1. Subir no GitHub
1. Crie um repositório novo (ex: `nexus-home`).
2. Envie **todos os arquivos desta pasta** para a raiz do repositório (não dentro de subpasta).

### 2. Conectar na Vercel
1. Em vercel.com → **Add New Project** → importe o repositório do GitHub.
2. Framework Preset: escolha **"Other"** (é um site estático puro, sem build).
3. Build Command: deixe vazio.
4. Output Directory: deixe vazio ou `.` (raiz).
5. Deploy.

### 3. Por que isso resolve a permissão de câmera/microfone
O navegador só pede permissão de câmera/mic em conexões seguras (`https://`).
A Vercel entrega HTTPS automaticamente em qualquer domínio `.vercel.app`, então
assim que o app abrir pelo link da Vercel (não mais como arquivo local), o
navegador vai exibir o popup de permissão normalmente.

Além disso, o `vercel.json` já inclui o header `Permissions-Policy` liberando
`camera`, `microphone` e `geolocation` explicitamente — importante caso você
no futuro coloque o app dentro de um iframe (ex: um app "casca" nativo).

### 4. Teste após o deploy
- Abra o link `https://seu-projeto.vercel.app` **no celular**, pelo Chrome/Safari.
- Vá em **Monitoramento → Celular como Câmera** e toque em "Ativar câmera" — deve aparecer o popup de permissão.
- Vá em **Monitoramento → Celular como Escuta Ambiente** e ative — deve aparecer o popup de permissão de microfone.
- Se aparecer o alerta "conexão insegura", confirme que a URL começa com `https://`.
- Se a permissão foi negada uma vez, o Chrome não pergunta de novo sozinho — libere manualmente em
  **Configurações do site → Câmera/Microfone → Permitir** e recarregue a página.

### 5. Instalar como app no celular (PWA)
No navegador do celular → menu (⋮) → "Adicionar à tela inicial" / "Instalar app".
Isso usa o `manifest.json` e o `sw.js` já configurados.
