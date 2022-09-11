- [Oracle Linux 8.6](#oracle-linux-86)
  - [Instalação](#instalação)
    - [Pré-instalação](#pré-instalação)
    - [Criando a máquina virtual](#criando-a-máquina-virtual)
    - [Montando a ISO do Oracle Linux](#montando-a-iso-do-oracle-linux)
    - [Instalando Oracle Linux na máquina virtual](#instalando-oracle-linux-na-máquina-virtual)
    - [Pós-instalação](#pós-instalação)
      - [Atualizando os pacotes](#atualizando-os-pacotes)
      - [Criando usuários](#criando-usuários)

</br>

# Oracle Linux 8.6

## Instalação

### Pré-instalação

- faça o download da **Full ISO do Oracle Linux 8.6** [nesse link](https://yum.oracle.com/oracle-linux-isos.html)
- faça o download do software de virtualização **VirtualBox** [nesse link](https://www.virtualbox.org/wiki/Downloads) e o instale nas configurações padrões

### Criando a máquina virtual

- na janela inicial do VirtualBox, clique em `New` para criar uma nova máquina virtual
- escolha o nome e o local do disco que desejar
- no campo `Type` selecione `Linux` e no campo `Version` selecione `Oracle (64-bit)`
- em seguida clique `Next`/`Create` em todas as próximas telas para selecionar as configurações padrões (1024MB de RAM, 12GB Hard Drive, VDI Hard Disk, Dynamically Allocated, 12GB size)
- na tela principal do VirtualBox: selecione a máquina que foi criada, clique em `Settings`, na aba `Network`, na opção `Attached to` selecione `Bridge adapter`, deixe o campo `Name` como está (por exemplo `wlp3s0`) e clique em `Ok` para voltar para a tela inicial do VirtualBox

### Montando a ISO do Oracle Linux

- antes de dar boot na máquina virtual, precisamos montar a ISO do Oracle Linux na máquina virtual para que possamos usa-la como o disco bootável durante a instalação do OS
- selecione a máquina do Oracle Linux na tela inicial do VirtualBox, clique em `Settings` e depois em `Storage`
- clique em `Adds optical drive` na seção de `Controller: IDE`, selecione a image ISO do Oracle Linux, clique em `Choose` e depois em `Ok` para voltar para a tela inicial do VirtualBox

### Instalando Oracle Linux na máquina virtual

- na tela inicial do VirtualBox, selecione a Máquina do Oracle Linux e clique em `Start`
- a ISO é o único disco bootável e por isso a máquina entrará diretamente no menu de instalação
- selecione a segunda opção `Test this media & install Oracle Linux 8.6.0` e aguarde o menu GUI com opções avançada ser carregado
- em `Localization` selecione a linguagem (usaremos `English (United State)`), o layout do keyboard (para teclados brasileiros `Portuguese (Brazil)`) e o `Time & Date` adequados
- em `User Settings` adicione uma senha para o usuário root
- em `Software` deixaremos `Installation Source` como `Local media` e em `Software Selection` selecionaremos `Minimal install` e nenhum software adicional pois o nosso objetivo é o de criar um server básico sem interface gráfica 
- em `System` confirme `Installation Destination` como `Automatic partitioning selected`, deixe `KDUMP` como está (ativado), em `Network & Host` habilite network e deixe `Security Policy` como está (`No profile selected`)
- clique em `Begin installation` e após a instalação ser finalizada clique em `Reboot System`

### Pós-instalação

- após clicar em `Reboot System`, o sistema será inicializado
- no menu GRUB, sempre selecione a primeira opção para iniciar o Oracle Linux normalmente
- para logar, entre com o usuário `root` e a senha escolhida durante a instalação

#### Atualizando os pacotes

- após a instalação é de boa prática atualizar os pacotes do sistema
- use por exemplo `ping -c 3 google.com` para testar o acesso à internet
- se a conexão com a internet estiver ok, use `dnf upgrade -y` para atualizar todos os pacotes

#### Criando usuários

- não é recomendável utilizar o usuário root diretamente, a melhor alternativa é usar usuários com privilégios root
- use `adduser username` para criar usuário 'username'
- use `passwd username` para definer a senha do usuário 'username'
- para atribuir privilégios de root para um usuário, execute `visudo` e no arquivo que será aberto por esse comando, adicione `username ALL=(ALL) ALL`
