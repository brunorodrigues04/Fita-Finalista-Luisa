# 🎓 Fita Finalista — Experiência AR
## Arquitetura do Projeto

---

## 📁 Estrutura de Pastas

```
ar-finalista/
│
├── index.html              ← Ponto de entrada (MVP completo)
│
├── assets/
│   ├── targets.mind        ← ⚠️ GERAR COM MINDAR COMPILER (ver abaixo)
│   ├── avatar.webm         ← Vídeo do avatar (fundo transparente)
│   ├── music.mp3           ← Música de fundo
│   ├── voice.mp3           ← Voz do utilizador
│   └── photos/
│       ├── foto1.jpg
│       ├── foto2.jpg
│       └── foto3.jpg
│
└── README.md
```

---

## 🔧 Como Gerar o Ficheiro targets.mind

1. Vai a: https://hiukim.github.io/mind-ar-js-doc/tools/compile
2. Faz upload de **uma foto de boa qualidade da fita**
   - A foto deve ter bom contraste e detalhes únicos
   - Tirar foto plana, sem reflexos
3. Clica em "Compile"
4. Descarrega o ficheiro `targets.mind`
5. Coloca-o em `assets/targets.mind`

---

## 🎬 Preparar o Avatar (Opção A — Recomendada)

### Gravação
- Filma-te de frente, fundo verde (green screen) ou fundo muito simples
- Resolução mínima: 720p
- Duração: 15–30 segundos, com loop suave

### Remoção do fundo
Ferramentas gratuitas:
- **Adobe Express** (online) → remove.bg para vídeo
- **DaVinci Resolve** (gratuito) → efeito Delta Keyer
- **CapCut** → remoção de fundo automática

### Exportar
- Formato: **WebM com canal alpha (transparência)**
- Codec: VP9 (suporta transparência)
- Comando FFmpeg (se tiveres instalado):
```bash
ffmpeg -i input.mp4 -c:v libvpx-vp9 -pix_fmt yuva420p output.webm
```

---

## 📱 Deploy (Obrigatório HTTPS para câmara)

### Opção 1 — Netlify (mais simples)
1. Vai a https://netlify.com
2. Arrasta a pasta `ar-finalista/` para a área de deploy
3. Obtém URL tipo: `https://xxx.netlify.app`

### Opção 2 — Vercel
```bash
npm install -g vercel
cd ar-finalista
vercel
```

### ⚠️ Importante
- A API `getUserMedia()` **só funciona em HTTPS**
- `localhost` funciona para desenvolvimento

---

## 📲 Criar QR Code

1. Após o deploy, copia o URL
2. Vai a https://qr.io ou https://qrcode-monkey.com
3. Gera um QR personalizado (podes usar as cores douradas)
4. Imprime e cola na fita ou num cartão junto à fita

---

## 🏷️ Configurar NFC (opcional)

Usa a app **NFC Tools** (Android/iOS):
1. Instala a app
2. Escreve na tag: Record → URL → `https://teu-site.netlify.app`
3. Cola a tag NFC atrás da fita ou no packaging

---

## ⚙️ Personalização no index.html

Localiza o objeto `CONFIG` no JavaScript:

```javascript
const CONFIG = {
  targetMindFile: 'assets/targets.mind',
  avatarVideo: 'assets/avatar.webm',
  bgMusic: 'assets/music.mp3',
  voiceAudio: 'assets/voice.mp3',
  messages: [
    'Chegaste.',
    'Lutaste.',
    'Conseguiste.',
    '✦ Finalista ✦'
  ],
  particleColor: '#c9a84c',
  experienceDuration: 25000  // milissegundos
};
```

---

## 🧱 Stack Tecnológico

| Camada | Tecnologia |
|--------|-----------|
| Trigger | QR Code / NFC |
| Frontend | HTML5 + CSS3 + JS ES6+ |
| AR Engine | MindAR.js v1.2.5 |
| 3D Rendering | Three.js r150 |
| Animações | GSAP 3.12 |
| Tipografia | Cormorant Garamond + Space Mono |
| Deploy | Netlify / Vercel |
| Avatar | WebM com alpha channel |

---

## 🔄 Fluxo da Experiência

```
QR / NFC
   ↓
Abre browser → index.html
   ↓
Splash Screen (Iniciar)
   ↓
Pede permissão câmara
   ↓
MindAR inicia
   ↓
Utilizador aponta para fita
   ↓
Image tracking deteta fita
   ↓
[TIMELINE ATIVA]
t=0s  → Avatar aparece ao lado da fita
t=0.5s → Toast: "Chegaste."
t=2s  → Reproduz voz
t=3s  → Toast: "Lutaste."
t=5s  → Fotos flutuantes surgem
t=6s  → Toast: "Conseguiste."
t=9.5s → Toast: "✦ Finalista ✦"
t=25s → Mensagem final ecrã completo
```

---

## ✅ Checklist para TFC / Relatório

- [ ] Gerar targets.mind com foto da fita
- [ ] Gravar e exportar vídeo do avatar (WebM alpha)
- [ ] Adicionar música de fundo (MP3)
- [ ] Adicionar voz (MP3)
- [ ] Adicionar fotos em assets/photos/
- [ ] Deploy em Netlify/Vercel (HTTPS)
- [ ] Gerar QR code com o URL
- [ ] Testar em dispositivo real (Android/iOS)
- [ ] (Opcional) Configurar NFC tag

---

*Desenvolvido como MVP para sistema de experiência AR em objeto físico.*
