# EVE-NG
Repositório dedicado para oficina de introdução ao EVE-NG ministrada para alunos do IFPB-CG com o apoio do ramo estudantil do IEEE do IFPB.

Para esse tutorial recomendo o uso do VMware Workstation Player, mas você também pode utilizar o VirtualBox.

Passos a seguir:
O primeiro passo a ser seguido é baixar a ISO do EVE-NG no site oficial
[https://www.eve-ng.net/index.php/download/](url).

Após o download, você precisa executar a VM como faria com outra VM, mas para essa, tem alguns requisitos que precisam ser atendidos para funcionar devidamente, principalmente se estiver utilizado o VirtualBox:
- Você deve mudar a interface de rede e colocar no modo bridge, assim, a sua VM vai receber IP da sua rede LAN e conseguir se comunicar com qualquer dispositivo que esteja na sua rede;
- De acordo com os seus recursos você deve colocar no mínimo 2 núcleos de CPU;
- Alocar pelo menos 25 GB de armazenamento, principalemnte se estiver utilizado o VirtualBox, pois em alguns testes que fiz menos que isso vai dar erro na inicialização;
- No mínimo 4 GB de memória RAM;
- É mandatório ativar a opção de aninhamento e virtualização intel VT-x/AMD-V tanto na sua BIOS quanto no hypervisor que esteja utilizando.

VMware
- Se tiver utilizando o VMware é só iniciar a máquina virtual e esperar a instalação so EVE-NG as únicas intervenções que você vai fazer é colocar o idioma e idioma do teclado e selecionar a opção continuar que vem logo depois.

VirtualBox
Se estiver utilizando o VirtualBox você vai fazer a mesma interação descrita no VMware, porém, ao terminar a primeira instalação você deve seguir os seguintes passos:
-   Ao iniciar o boot de inicialização, você deve desligar a VM;
-   Vá em configurações -> armazenamento e em 'controladora: IDE' remova a conexão;
-   Inicie a VM novamente e espere a inicialização.

Ao iniciar vai aparecer as informações necessárias para acessar o GUI do EVE-NG, que seria o IP. Coloque o IP no navegador e as informações padrões de login no GUI são:

Login: `admin` 
Senha: `eve`

E as infomaçõess de login ssh são: 

  login: `root`
  senha: `eve`


# Adição de dispositivos

Para adicionar dispositivos no EVE-NG você vai precisar seguir alguns passos que são descritos abaixo:

- Baixe o dispositivo que deseja simular utilizado a seguinte biblioteca [https://drive.labhub.eu.org/0:/addons/](url).
Alguns dispositivos podem não fucionar, então sempre verifique a disponibilidade do dispositivo na tabela de dispositivos oficiais do EVE-NG [https://www.eve-ng.net/index.php/documentation/qemu-image-namings/](url).
- Após fazer o download você vai utilizar o WinSCP ou linha de comando para enviar o arquivo baixado para a pasta de dispositivos. As pastas precisam está nomeadas de acordo com o que especificado na página do EVE-NG, assim como o nome do arquivo precisa ter o nome e a extensão correta.
- O caminho para a pasta de dispositivo é: `/opt/unetlab/addons/qemu`.
- Crie uma pasta com o nome do dispositivo e adicione o arquivo dentro dessa pasta. Por exemplo: `/opt/unetlab/addons/qemu/mikrotik.6.39/`
- Dica: Ao criar a pasta com o nome do dispositivo coloque o mesmo nome que está na biblioteca de dispositivos. Isso pode evitar algum tipo de erro na hora de criar a pasta do dispositivo.
- Quando mover o arquivo pra pasta do dispositivo você obrigatoriamente deve fazer o seguinte comando para aplicar as permissões e o dispositivo aparecer no EVE-NG: `/opt/unetlab/wrappers/unl_wrapper -a fixpermissions`.
- Procure o dispositivo adicionado no EVE-NG, monte suas topologias e se divirta!



# Adicionar sua própria VM ao EVE-NG

Caso você tenha uma VM que executa algum tipo de serviço e queira testar ela em algum cenário específico que não tem como você testar em ambiente real, voce pode adicionar essa VM pronta ao EVE-NG e montar sua topologia de teste.
- Primeiro você vai colocar o disco, ou OVA da sua máquina virtual na pasta de dispositivos no EVE-NG.
- Caso seja uma .OVA use o comando `tar xvf nome_da_vm.ova` para extrair os arquivos e o único que você vai precisar é o .vmdk;
- Após ter o .vmdk use o comando `qemu-img convert -f vmdk -O qcow2 nome_da_vm.vmdk virtioa.qcow2` para converter o disco para o padrão suportado pelo EVE-NG;
- Aplique as permissões e você poderá usar a sua VM dentro do EVE-NG.
