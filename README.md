<h1 align="center">🎮 8BitDo Ultimate 2C – Linux Fix</h1>

<p align="center">
  <strong>Correção completa para mapeamento de controle 8BitDo no Linux (Ubuntu / Pop!_OS)</strong>
</p>

<hr>

<h2>📝 Sobre o Projeto</h2>

<p>
O <b>8BitDo Ultimate 2C Wireless</b> pode ser reconhecido no Linux como um dispositivo D-Input genérico, causando problemas de compatibilidade com jogos e serviços como xCloud.
</p>

<h3>❌ Problemas comuns</h3>

<ul>
  <li>Analógico direito invertido ou travado</li>
  <li>Gatilhos (LT/RT) sem resposta analógica</li>
  <li>Mapeamento incorreto de botões</li>
  <li>Detecção como controle genérico</li>
</ul>

<h3>✅ Solução</h3>

<p>
Este projeto utiliza o <code>xboxdrv</code> para criar um controle virtual Xbox 360 totalmente compatível com jogos no Linux.
</p>

<hr>

<h2>🚀 Instalação</h2>

<h3>1. Instalar dependência</h3>

<pre><code>sudo apt update && sudo apt install xboxdrv -y</code></pre>

---

<h3>2. Criar script de correção</h3>

<pre><code>nano ~/8bitdo_fix.sh</code></pre>

<p>Cole o conteúdo:</p>

<pre><code>
#!/bin/bash
sudo xboxdrv \
--evdev /dev/input/event21 \
--evdev-absmap ABS_X=x1,ABS_Y=y1,ABS_RX=x2,ABS_RY=y2,ABS_Z=lt,ABS_RZ=rt,ABS_HAT0X=dpad_x,ABS_HAT0Y=dpad_y \
--evdev-keymap BTN_SOUTH=a,BTN_EAST=b,BTN_NORTH=x,BTN_WEST=y,BTN_TL=lb,BTN_TR=rb,BTN_THUMBL=tl,BTN_THUMBR=tr,BTN_SELECT=back,BTN_START=start,BTN_MODE=guide \
--axismap -y1=y1,-y2=y2 \
--mimic-xpad \
--silent
</code></pre>

<p>Dar permissão:</p>

<pre><code>chmod +x ~/8bitdo_fix.sh</code></pre>

---

<h2>🛠️ Atalho no sistema (opcional)</h2>

<pre><code>nano ~/.local/share/applications/8bitdo-xbox.desktop</code></pre>

<p>Conteúdo:</p>

<pre><code>
[Desktop Entry]
Name=Ativar Controle 8BitDo
Comment=Converte 8BitDo em controle Xbox
Exec=bash -c "$HOME/8bitdo_fix.sh"
Icon=gamepad
Terminal=true
Type=Application
Categories=Game;
</code></pre>

---

<h2>⚙️ Ajustes opcionais</h2>

<pre><code>
sudo udevadm control --reload-rules && sudo udevadm trigger
</code></pre>

<pre><code>
sudo modprobe -r xpad
sudo modprobe xpad
</code></pre>

---

<h2>🎮 Como usar</h2>

<ol>
  <li>Conecte o controle 8BitDo</li>
  <li>Abra o menu de aplicativos</li>
  <li>Execute "Ativar Controle 8BitDo"</li>
  <li>Digite a senha</li>
  <li>Pronto 🎉</li>
</ol>

<p align="center">
  <b>O controle será detectado como Xbox 360 Controller</b>
</p>

---

<h2>⚠️ Observações</h2>

<ul>
  <li>O device <code>event21</code> pode mudar</li>
  <li>Use <code>sudo evtest</code> para identificar corretamente</li>
</ul>

---

<h2>💡 Melhorias futuras</h2>

<ul>
  <li>Detecção automática do controle</li>
  <li>Execução automática ao conectar USB</li>
  <li>Versão GUI</li>
  <li>Substituir evdev fixo por udev rules</li>
</ul>

---

<p align="center">
  Feito para melhorar a compatibilidade do 8BitDo no Linux 🎮
</p>
