## Descrição técnica tarefa 1
- O código do arquivo "main.tf" faz a configuração de uma infraestrutura AWS definindo o par de chaves encriptadas com o algoritmo RSA de 2048 bits, mas não tem instruções para armazenamento seguro da chave privada.

- Também cria uma VPC e uma subrede para tráfego seguro, já definindo seu gateway, tabela de roteamento e grupo de segurança. Entretanto, no grupo de segurança é definido que a entrada pode ser feita a partir de qualquer IP, o que não é o ideal, já que alguém pode acessar sem a devida autorização. 

- Também é criada uma instancia EC2 utilizando uma imagem do debian 12. A instância tem 20GB de espaço e executa um script ao iniciar para atualizar os pacotes, quando a instância é encerrada o disco é apagado. O disco não é criptografado, o que é uma vulnerabilidade.

- É gerado 2 output, um com a chave privada(como é sensível não é exibida no terminal) e o IP publico.

> Link para o main.tf alterado: [main.tf](main.tf)
## Descrição técnica tarefa 2(mudanças realizadas)
- SSH restringindo a um IP seguro
    - (linha 17 a 21): Criando a variável para o IP seguro
    - (linha 73): utilização da variável

- Criptografia ativada no Disco de armazenamento
    - (linha 120)

- instalando, iniciando e configurando o Nginx
    - (linha 76 a 82): Adicionando regra ao aws_security_group para ter acesso ao Nginx pela porta 80
    - (linha 128 a 130): Comandos adicionais necessários para instalar e iniciar o Nginx

## instruções de uso
Com o terraform devidamente instalado e executando a partir do diretório em que o main.tf então execute

```
    terraform init
```

Após isso execute 
```
    terraform apply
```
