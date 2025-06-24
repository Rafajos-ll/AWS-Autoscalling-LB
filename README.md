# AWS-Autoscalling-LB  

- Participantes do Projeto:

.Rafael Giocondo Schmidt<br>
.Algacyr Silva de Melo Junior

- Criaremos um projeto utilizando o auto scalling group e suas politicas para simular a geração de carga e aumentar ou diminuir as instancias.

## 1.Primeiro criaremos a vpc:

- criaremos ela no modo criar vpc e muito mais onde se cria tudo automaticamente:

![Texto alternativo](/Prints-Project-2/vpc-00.png)

![Texto alternativo](/Prints-Project-2/vpc-01.png)

![Texto alternativo](/Prints-Project-2/vpc-02.png)

## 2.Criacao da template:

- com nossa vpc criada, lancaremos a nossa template agora para integra-la no auto scalling group:

![Texto alternativo](/Prints-Project-2/templates-00.png)

![Texto alternativo](/Prints-Project-2/template-01.png)

![Texto alternativo](/Prints-Project-2/template-02.png)

![Texto alternativo](/Prints-Project-2/templates-03.png)

. e tambem o user data usado para criar ela
 
```
#!/bin/bash
yum update -y
yum install -y httpd
echo "Hello World" > /var/www/html/index.html
 
cat <<EOL > /var/www/html/teste
echo "Content-type: text/plain"
echo ""
echo "Requisição recebida em $(hostname)"
sleep 5
EOL
 
chmod +x /var/www/html/teste
systemctl start httpd
systemctl enable httpd
```


## 3.Criacao do Load Balancer:

- Criaremos o load balancer para acessar o site pelo dns e verificar as requests:

![Texto alternativo](/Prints-Project-2/elb-00.png)

![Texto alternativo](/Prints-Project-2/elb-01.png)

![Texto alternativo](/Prints-Project-2/elb-02.png)

![Texto alternativo](/Prints-Project-2/elb-03.png)

![Texto alternativo](/Prints-Project-2/elb-04.png)

## 4.Criacao do Auto Scalling Group:

- agora intregaremos o auto scalling group permitindo assim que as politicas sejam aplicadas:

![Texto alternativo](/Prints-Project-2/as-00.png)

![Texto alternativo](/Prints-Project-2/as-01.png)

![Texto alternativo](/Prints-Project-2/as-02.png)

![Texto alternativo](/Prints-Project-2/as-03.png)

![Texto alternativo](/Prints-Project-2/as-04.png)

![Texto alternativo](/Prints-Project-2/as-05.png)

![Texto alternativo](/Prints-Project-2/as-06.png)

![Texto alternativo](/Prints-Project-2/as-07.png)

- Configuraremos com as seguintes politicas:

![Texto alternativo](/Prints-Project-2/as-policies.png)

## 5.Configurando o Cloudwatch:

- Agora no cloudwatch configuraremos os alarems para efetivar as politicas que foram feitas e assim se necessario diminuir ou aumentar a carga:

![Texto alternativo](/Prints-Project-2/cw-00.png)

![Texto alternativo](/Prints-Project-2/cw-01.png)

![Texto alternativo](/Prints-Project-2/cw-02.png)

![Texto alternativo](/Prints-Project-2/cw-03.png)

## 6 Resultado do projeto finalizado:

- Com todos os nossos serviços configurados o resultado deve ser esse:

![Texto alternativo](/Prints-Project-2/as-activity-00.png)

![Texto alternativo](/Prints-Project-2/as-activity-01.png)

- com as instancias sendo ciradas e terminadas de acordo com a demanda

![Texto alternativo](/Prints-Project-2/ec2-instances-max-capacity.png)

