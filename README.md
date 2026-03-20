
 <h1 align="center">🎮 8BitDo Ultimate 2C - Linux Fix</h1>
    
<p align="center">
        <strong>Solução definitiva para mapeamento de 16 botões (Modo Xbox) no Linux (Pop!_OS / Ubuntu)</strong>
    </p>

   <hr>
    <h2>📝 Sobre o Projeto</h2>
    <p>
        O <b>8BitDo Ultimate 2C Wireless</b> costuma ser identificado no Linux apenas no modo <i>D-Input</i> genérico, o que causa bugs críticos:
    </p>
    <ul>
        <li>Analógico direito travado ou invertido.</li>
        <li>Gatilhos (LT/RT) não reconhecidos como analógicos.</li>
        <li>Apenas 11 botões detectados (o xCloud exige 16).</li>
    </ul>
    <p>Este projeto utiliza o <code>xboxdrv</code> para criar um "clone" virtual de um controle de Xbox 360, corrigindo todos os eixos via mapeamento <b>evdev</b>.</p>
    <h2>🚀 Pré-requisitos</h2>
    <p>Instale o driver necessário via terminal:</p>
    <pre><code>sudo apt update && sudo apt install xboxdrv -y</code></pre>
    <h2>🛠️ Passo a Passo</h2>
    <h3>1. Criar o Script de Correção</h3>
    <p>Use o <b>Vim</b> para criar o arquivo na sua pasta pessoal:</p>
    <pre><code>vim ~/8bitdo_fix.sh</code></pre>  
    <p>Cole o código abaixo (calibrado para o modelo 2C):</p>
    <div style="background-color: #1e1e1e; color: #d4d4d4; padding: 15px; border-radius: 8px;">
        <pre><code>#!/bin/bash
sudo xboxdrv --evdev /dev/input/by-id/usb-8BitDo_8BitDo_Ultimate_2C_Wireless_Controller_D08018A781-event-joystick \
--evdev-absmap ABS_X=x1,ABS_Y=y1,ABS_RX=x2,ABS_RY=y2,ABS_Z=lt,ABS_RZ=rt,ABS_HAT0X=dpad_x,ABS_HAT0Y=dpad_y \
--evdev-keymap BTN_SOUTH=a,BTN_EAST=b,BTN_NORTH=x,BTN_WEST=y,BTN_TL=lb,BTN_TR=rb,BTN_THUMBL=tl,BTN_THUMBR=tr,BTN_SELECT=back,BTN_START=start,BTN_MODE=guide \
--axismap -y1=y1,-y2=y2 \
--mimic-xpad --silent</code></pre>
    </div>
    <p>Dê permissão de execução:</p>
    <pre><code>chmod +x ~/8bitdo_fix.sh</code></pre>
    <h3>2. Criar Atalho no Menu (App)</h3>
    <p>Para abrir o controle com um clique no menu de aplicativos:</p>
    <pre><code>vim ~/.local/share/applications/8bitdo-xbox.desktop</code></pre>
    <p>Cole o conteúdo:</p>
    <div style="background-color: #1e1e1e; color: #d4d4d4; padding: 15px; border-radius: 8px;">
        <pre><code>[Desktop Entry]
Name=Ativar Controle 8BitDo
Comment=Converte 8BitDo 2C para Xbox Mode
Exec=gnome-terminal -- bash -c "sudo ~/8bitdo_fix.sh; exec bash"
Icon=input-gaming
Terminal=false
Type=Application
Categories=Game;</code></pre>
    </div>
    <h2>🎮 Como Jogar</h2>
    <ol>
        <li>Conecte o adaptador USB do controle.</li>
        <li>Abra o menu do sistema e procure por <b>"Ativar Controle 8BitDo"</b>.</li>
        <li>Digite sua senha no terminal que abrir.</li>
        <li>O controle agora aparecerá como <b>Microsoft Xbox 360 Controller</b> no Gamepad Tester e no xCloud.</li>
    </ol>
    <hr>
    <p align="center"><i>Desenvolvido para garantir a melhor experiência no Xbox Cloud Gaming via Linux.</i></p>
