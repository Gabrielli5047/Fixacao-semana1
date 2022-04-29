# D-semana1
EXERCÍCIOS PRÁTICOS - Semana 1

Com base nas aulas dessa semana, iremos colocar em prática os conceitos teóricos vistos em aula

Crie uma rede pública(vpc) na Amazon com todos os recursos necessários para ter acesso a Internet.

Importante: deixar esta rede em datacenters diferentes

Depois crie um EC2 e faça a conexão via ssh na máquina criada.

1- Criando a vpc (criar redes virtuais):
  1.1- Buscamos em - https://us-east-1.console.aws.amazon.com/console/home?region=us-east-1# -> VPC - > vpc's
   1.2- create vpc -> name 
   1.3- vamos na tabela Calculadora de rede para IPV4 -> https://www.site24x7.com/pt/tools/ipv4-sub-rede-calculadora.html
     1.3.1- 10.24.0.0/24 - vou usar em IPv4 CIDR
     1.3.2- create vpc
     1.3.3- selecionei a vpc que criei -> actions -> Edit DNS hostnames -> Enable
   1.4- Apos criar a vpc, vamos criar as subnets (subredes)- create subnet  
     1.4.1- VPC ID -> escolho a minha vpc criada.
     1.4.2- Subnet settings -> 
        Subnet name - > ex: Subnet-name-1a
        Availability Zone -> n. virginia 1a
        IPv4 CIDR block -> valor do Subnet ID - 1- na calculadora de sub rede
        
        Subnet name - > ex: Subnet-name-1b
        Availability Zone -> n. virginia 1b
        IPv4 CIDR block -> valor do Subnet ID - 2- na calculadora de sub rede
        
        Subnet name - > ex: Subnet-name-1c
        Availability Zone -> n. virginia 1c
        IPv4 CIDR block -> valor do Subnet ID - 3- na calculadora de sub rede
      1.4.3- create subnet
    1.5- Para tornar nosso acesso publico vamos em -> internet gateway -> Internet gateway settings -> create
    1.6- temos que adicionar na nossa internet gateway uma vpc -> actions -> attach internet gateway -> seleciona nossa vpc -> attach...
    1.7- Vamos configurar agora o route tables
       1.7.1- Da um nome e seleciona a nossa vpc
       1.7.2- Precisamos de um acesso externos -> criaremos outra rota-> edit routes -> add routes
          1.7.2.1- 0.0.0.0/0 -> internet gateway -> save 
       1.7.3- vamos em subnet associations -> Explicit subnet associations (0) -> edit -> selecionamos as que queremos deixar publica
       1.7.4- save associations 
       
 2- Criarei agora a maquina - ec2
    2.1- instances - > launch instances 
       2.1.1- Selecionaremos -> Ubuntu Server 20.04 LTS (HVM), SSD Volume Type - ami-04505e74c0741db8d (64-bit x86) / ami-0b49a4a6e8e22fa16 (64-bit Arm)
       2.1.2- t2.micro -> free
       2.1.3- configure instance 
          2.1.3.1-  instance - 1
          2.1.3.2-  Network - seleciona minha vpc
          2.1.3.3-  Subnet - uma das 3 subnets ( publica)
          2.1.3.4-  Auto-assign Public IP - enable
       2.1.4- add storage -> add tags -> configure security -> gab-security -> review and launch -> launch-> seleciona minha key pair 
       2.1.5- launch instances -> The following instance launches have been initiated: i-... -> clica nesse link -> connect -> ssh client
       2.1.6- copia o ssh -> ssh -i ....amazonaws.com
  3- vamos no terminal - na pasta onde estao as nossas chaves-> e cola a ssh copiada no passso acima
      3.1 - substituimos o "gabrielli..."por id_rsa e damos enter -> yes
  4- maquina ta rodando.