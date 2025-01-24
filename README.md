# Conexão SSH entre Dispositivos Móveis
Estudo de conexão SSH feita através de dois dispositivos Android, utilizando o aplicativo `Termux`.

[Assista ao vídeo de demonstração.](https://youtu.be/DxxPuTWq7zc)


## Configurações inicias
1. Instale o Termux nos dispositivos.

2. Permita que o Termux acesse os diretórios locais, através do comando:
    ```plaintext
    termux-setup-storage
    ```

3. No dispositivo host, defina uma senha de acesso ao terminal.
    ```plaintext
    passwd
    ```

4. Em ambos dispositivos, instale a biblioteca `openssh`.
    ```plaintext
    pkg install openssh
    ```

## Abrindo o servidor SSH
No dispositivo A, faça:

2. Leia o arquivo `sshd_config`, por meio do editor de texto nativo `nano`:
    ```plaintext
    nano /data/data/com.termux/files/usr/etc/ssh/sshd_config
    ```
    e verifique se a porta está configurada corretamente, bem como a autenticação por senha.
    ```plaintext
    #Port 8022
    ...
    #PasswordAuthentication yes
    ```
    Caso não esteja, configure corretamente e salve o arquivo.

3. Descubra seu nome de usuário do Termux. Normalmente, está no formato `u0_aXXX`.
    ```plaintext
    whoami
    ```
4. Descubra o `Endereço IP` do seu dispositivo na rede local.
    ```plaintext
    ifconfig
    ```
    É esperado que seja retornado `wlan0`, que é onde se encontra o seu IP:
    ```plaintext
    inet 192.168.X.XXX
    ```

5. Inicie o servidor SSH no dispositivo:
    ```plaintext
    sshd
    ```
    Você também pode conferir se o servidor foi aberto corretamente, executando o seguinte comando:
    ```plaintext
    ps aux | grep sshd
    ```
    Caso esteja ativo, você verá algo como `/data/data/com.termux/files/usr/bin/sshd`.

## Conectando-se ao servidor SSH
No dispositivo B, faça:
1. Conecte ao servidor SSH
    ```plaintext
    ssh <nome_de_usuárioA>@<ip_do_dispositivoA> -p 8022
    ```

2. Permita que crie uma impressão digital da chave pública.