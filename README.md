<h1 align="center">🎮 8BitDo Ultimate 2C – Linux Fix</h1>

<p align="center">
  <strong>Correção completa para mapeamento de 16 botões (Modo Xbox) no Linux (Ubuntu / Pop!_OS)</strong>
</p>

<hr>

<h2>📝 Sobre o Projeto</h2>
<p>
O <b>8BitDo Ultimate 2C Wireless</b> pode ser reconhecido no Linux como um dispositivo <i>D-Input genérico</i>, causando problemas de compatibilidade.
</p>

<h3>❌ Problemas comuns</h3>
<ul>
  <li>Analógico direito travado ou invertido</li>
  <li>Gatilhos (LT/RT) sem resposta analógica</li>
  <li>Apenas 11 botões detectados (o xCloud exige 16)</li>
</ul>

<h3>✅ Solução</h3>
<p>
Este projeto utiliza o <code>xboxdrv</code> para criar um <b>controle virtual de Xbox 360</b>, corrigindo eixos, botões e gatilhos via <b>mapeamento evdev</b>.
</p>

<hr>

<h2>🚀 Pré-requisitos</h2>
<p>Instale o driver necessário:</p>

<pre><code>sudo apt update && sudo apt install xboxdrv -y</code></pre>

<hr>

<h2>🛠️ Instalação</h2>

<h3>1. Criar o Script de Correção</h3>

<pre><code>vim ~/8bitdo_fix.sh</code></pre>

<p>Cole o conteúdo abaixo:</p>

<div style="background-color:#1e1e1e;color:#d4d4d4;padding:15px;border-radius:8px;">
<pre><code>#!/bin/bash
sudo xboxdrv \
--evdev /dev/input/event21 \
--evdev-absmap ABS_X=x1,ABS_Y=y1,ABS_RX=x2,ABS_RY=y2,ABS_Z=lt,ABS_RZ=rt,ABS_HAT0X=dpad_x,ABS_HAT0Y=dpad_y \
--evdev-keymap BTN_SOUTH=a,BTN_EAST=b,BTN_NORTH=x,BTN_WEST=y,BTN_TL=lb,BTN_TR=rb,BTN_THUMBL=tl,BTN_THUMBR=tr,BTN_SELECT=back,BTN_START=start,BTN_MODE=guide \
--axismap -y1=y1,-y2=y2 \
--mimic-xpad \
--silent
</code></pre>
</div>

<p>Dê permissão de execução:</p>

<pre><code>chmod +x ~/8bitdo_fix.sh</code></pre>

<hr>

<h3>2. Criar Atalho no Menu (Opcional)</h3>

<pre><code>vim ~/.local/share/applications/8bitdo-xbox.desktop</code></pre>

<p>Cole o conteúdo:</p>

<div style="background-color:#1e1e1e;color:#d4d4d4;padding:15px;border-radius:8px;">
<pre><code>[Desktop Entry]
Name=Ativar Controle 8BitDo
Comment=Converte 8BitDo 2C para modo Xbox
Exec=gnome-terminal -- bash -c "sudo ~/8bitdo_fix.sh; exec bash"
Icon=input-gaming
Terminal=false
Type=Application
Categories=Game;
</code></pre>
</div>

<hr>

<h2>⚙️ Ajustes Opcionais</h2>

<p>Atualizar regras do sistema:</p>

<pre><code>sudo udevadm control --reload-rules && sudo udevadm trigger</code></pre>

<p>Recarregar driver do Xbox:</p>

<pre><code>sudo modprobe -r xpad
sudo modprobe xpad</code></pre>

<hr>

<h2>🎮 Como Usar</h2>

<ol>
  <li>Conecte o adaptador USB do controle</li>
  <li>Abra o menu de aplicativos</li>
  <li>Execute <b>"Ativar Controle 8BitDo"</b></li>
  <li>Digite sua senha</li>
  <li>Pronto! 🎉</li>
</ol>

<p>O controle será reconhecido como:</p>

<p align="center"><b>Microsoft Xbox 360 Controller</b></p>

<hr>

<h2>⚠️ Observações</h2>

<ul>
  <li>O número do dispositivo (<code>event21</code>) pode variar</li>
</ul>

<p>Use para identificar corretamente:</p>

<pre><code>ls /dev/input/</code></pre>

<p>Ou:</p>

<pre><code>sudo evtest</code></pre>

<ul>
  <li>Verifique se não há conflitos com outros drivers</li>
</ul>

<hr>

<h2>💡 Melhorias Futuras</h2>

<ul>
  <li>Detecção automática do device (<code>eventX</code>)</li>
  <li>Inicialização automática via systemd</li>
  <li>Interface gráfica simples (GUI)</li>
</ul>

<hr>

<h2>🤝 Contribuição</h2>

<p>
Pull requests são bem-vindos!  
Sinta-se livre para contribuir com melhorias.
</p>

<hr>

<h2>📄 Licença</h2>

<p>Projeto open-source para uso livre.</p>

<hr>

<p align="center">
  <i>Feito para melhorar a experiência com Xbox Cloud Gaming no Linux 🎮</i>
</p>

<img width="1500" height="1500" alt="image" src="https://github.com/user-attachments/assets/efb18f7c-f441-4a03-a3ca-11cec16064e5" />
