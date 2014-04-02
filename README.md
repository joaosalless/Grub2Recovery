Grub2Recovery
=============

Estas configurações foram criadas no intuito de desenvolver um sistema de Backup e Recovery 100% automatizado de uma instalação do Windows 7.

Utiliza-se o Clonezilla (versão debian) para backup e restauração de partições.
Utiliza-se variáveis como data e hora diretamente no grub.cfg para automatizar o nome dos backups.
Está funcionando perfeitamente para minhas necessidades: Foi testado apenas em um HD interno.

O HD testado tinha as seguintes partições:

    /dev/sda1 100M NTFS (Reservado pelo sistema)
    /dev/sda2 49G  NTFS (Windows)
    /dev/sda3 68G  ext3 (Recovery)
    /dev/sda4 42G  NTFS (Documentos) Todos os perfis de usuarios ficam nesta partição. Nenhum documento é perdido quando o Windows é restaurado.

Nesta instalação utilizei:
Clonezilla: http://colocrossing.dl.sourceforge.net/project/clonezilla/clonezilla_live_stable/2.2.2-32/clonezilla-live-2.2.2-32-i686-pae.zip
SystemRescueCD: http://ufpr.dl.sourceforge.net/project/systemrescuecd/sysresccd-x86/4.1.0/systemrescuecd-x86-4.1.0.iso

Para fazer uma instalação semelhante a esta, siga os passos supondo que a partição de Recovery será /dev/sda3:

####1 - Dê boot na máquina com um LiveCD que possua o grub na versão 2.0 (eu utilizei Ubuntu 13.10)
####2 - Use o Gparted caso precise redimensionar ou criar partições
####3 - Monte a partição e navegue pelo terminal até a raiz da partição e crie as pastas necessárias com os comandos:

    $ sudo mkdir -p /mnt/Recovery
    
    $ sudo mount /dev/sda3 /mnt/Recovery
    
    cd tmp
    
    $ sudo mkdir -p {tmp,Recovery/{isos,images/{OEM,backups}}}

    $ sudo chmod -R 777 Recovery tmp

####4 - Baixe os links citados acima (Clonezilla e SystemRescueCD) com os comandos:

    $ cd tmp

    $ wget http://colocrossing.dl.sourceforge.net/project/clonezilla/clonezilla_live_stable/2.2.2-32/clonezilla-live-2.2.2-32-i686-pae.zip

    $ unzip clonezilla-live-2.2.2-32-i686-pae.zip
    
    $ cp -rf live/* ../Recovery/

    $ wget http://ufpr.dl.sourceforge.net/project/systemrescuecd/sysresccd-x86/4.1.0/systemrescuecd-x86-4.1.0.iso
    
    $ cp systemrescuecd-x86-4.1.0.iso ../Recovery/isos

####5 - Instale o grub2 com o comando:

    $ sudo grub-install --boot-directory=/mnt/Recovery/Recovery

Copie este arquivo "grub.cfg" para /mnt/Recovery/Recovery/grub/grub.cfg com o comando:

    $ cd /mnt/Recovery/Recovery/grub/
    
    $ wget https://raw.githubusercontent.com/joaosalless/Grub2Recovery/master/grub.cfg

Edite o arquivo `/mnt/Recovery/Recovery/grub/grub.cfg`e ajuste o necessário como IP e Senha do root e vnc (ambas utilizadas no boot do SystemRescueCD)

#### 6 - Reinicie a máquina e use.

### Scrennshots

![enter image description here][1]

![enter image description here][2]

![enter image description here][3]

![enter image description here][4]

![enter image description here][5]


  [1]: https://raw.githubusercontent.com/joaosalless/Grub2Recovery/master/creenshots/WIN72.png
  [2]: https://raw.githubusercontent.com/joaosalless/Grub2Recovery/master/creenshots/WIN73.png
  [3]: https://raw.githubusercontent.com/joaosalless/Grub2Recovery/master/creenshots/WIN74.png
  [4]: https://raw.githubusercontent.com/joaosalless/Grub2Recovery/master/creenshots/WIN75.png
  [5]: https://raw.githubusercontent.com/joaosalless/Grub2Recovery/master/creenshots/WIN76.png