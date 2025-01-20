# Conexão SSH entre Dispositivos Móveis
Conexão SSH feito através de senha de autenticação. Para mais segurança, meio de chaves de acesso.

## Configurações inicias
1. Instale o Termux no seu dispositivo

2. Permita que o Termux acesse o seu diretório local, através do comando
```plaintext
termux-setup-storage
```

3. Defina uma senha de acesso ao terminal
```plaintext
passwd
```

4. Instale a biblioteca `openssh`
```plaintext
pkg install openssh
```

## Abrindo o servidor SSH
No dispositivo A, faça:

1. Instale a biblioteca `openssh`
```plaintext
pkg install openssh
```

2. Leia o arquivo `sshd_config`, por meio do editor de texto `nano`:
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

## Conectando no servidor SSH
No dispositivo B, faça:
1. Conecte ao servidor SSH
```plaintext
ssh <nome_de_usuário>@<ip_do_dispositivoA> -p 8022
```

2. Permita que crie uma impressão digital da chave pública

3. Insira a senha definida
