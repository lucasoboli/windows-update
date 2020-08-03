# Instruções

## Erro 0x80070005
Siga as instruções na ordem apresentada abaixo, testando o *Windows Update* após cada passo completado.


### Passo 1

> Utilize a Ferramenta de Correção do *Windows Update*.

1. Baixe e execute o arquivo `WindowsUpdate.diagcab` encontrado no repositório ou em https://aka.ms/diag_wu.


### Passo 2

> Bloqueio do antivírus.

1. Desative ou desinstale programas antivírus caso haja algum instalado;
2. Reinicie o computador.


### Passo 3

> Redefina a conexão de rede.

1. Abra o *Prompt de Comando* como Administrador;
2. Utilize os comandos abaixo:

``` sh
$ ipconfig /release
$ ipconfig /renew
$ ipconfig /flushdns
$ netsh winsock reset
$ net localgroup administradores localservice /add
$ fsutil resource setautoreset true C:\
$ netsh int ip reset resetlog.txt
$ netsh winsock reset all
$ netsh int 6to4 reset all
$ netsh int ip reset all
$ netsh int ipv4 reset all
$ netsh int ipv6 reset all
$ netsh int httpstunnel reset all
$ netsh int isatap reset all
$ netsh int portproxy reset all
$ netsh int tcp reset all
$ netsh int teredo reset all
$ netsh int ip reset
$ netsh winsock reset
```

3. Reinicie o computador.


### Passo 4

> Redefina para inicialização automática os serviços relacionados à *Windows Store* e ao *Windows Update*.

1. Abra o *Prompt de Comando* como Administrador;
2. Utilize os comandos abaixo:

``` sh
$ sc config wuauserv start= auto
$ sc config bits start= auto
$ sc config Cryptsvc start= auto
$ sc config TrustedInstaller start= auto
```

3. Reinicie o computador.


### Passo 5

> Realize uma inicialização limpa.

1. Pressione as teclas `Windows + R`, digite `Msconfig` e clique em Ok;
2. Selecione a aba `Serviços`;
3. Habilite a opção `Ocultar todos os serviços Microsoft`;
4. Clique em `Desativar tudo`;
5. Clique em `Inicialização do Sistema` > `Opções Avançadas`;
6. Habilite a opção `Número de processadores` e escolha o maior valor possível;
7. Clique na aba `Inicialização de Programas` > `Gerenciador de Tarefas` > Inicializar`;
8. Desative os Programas;
9. Feche o Gerenciador de Tarefas e clique em Ok;
10. Reinicie o computador. 

**OBSERVAÇÃO:** Isto desabilitará todos os serviços e programas de terceiros. Se o problema for solucionado neste passo, recomenda-se a habilitação individual e seletiva dos programas e serviços que serão inicializados com o *Windows*. Caso o problema volte após a ativação de um serviço/programa em específico, ele estará diretamente relacionado à este serviço/programa.


### Passo 6

> Limpar os arquivos temporários.

 1. Pressione as teclas `Windows + R`, digite `%TEMP%` e clique em Ok;
 2. Apague permanentemente todos os arquivos contidos na pasta *TEMP*;
 3. Abra o menu Executar novamente pressionando `Windows + R`;
 4. Digite `Prefetch` e clique em Ok;
 5. Apague permanentemente todos os arquivos contidos na pasta *Prefetch*;
 6. Reinicie o computador.


### Passo 7

> *DLLs*

1. Baixe o arquivo `WindowsUpdate.bat` do repositório;
2. Execute-o como administrador e aguarde a inserção das *DLLs*;
3. Reinicie o computador.


### Passo 8

1. Abra o *Prompt de Comando* como Administrador;
2. Utilize o comando:
``` sh 
sfc \scannow
```

3. Finalizado o passo anterior, utilize o comando:
``` sh
DISM.exe/Online /Cleanup-image /Restorehealth
```

4. Espere a execução finalizar;
5. Reinicie o computador.