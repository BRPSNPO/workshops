# Worskshop sobre CORE Services AWS

Olá, este é um workshop individualizado, desenvolvido para explorar os Serviços Principais da AWS.

Neste workshop, você hospedará um site estático e criará uma arquitetura de aplicativos de duas camadas, cobrindo os principais serviços e as práticas recomendadas para computação, rede, armazenamento e bancos de dados.

Veja o diagrama abaixo para uma descrição da arquitetura completa.

## Conta da AWS necessária
Para concluir esses workshops, você precisará de uma conta ativa da AWS válida com permissões de administrador. 

Você deve concluir os seguintes módulos na região Leste dos EUA (Virgínia do Norte) em ordem antes de prosseguir para a próxima.

Iremos utilizar a plataforma: [Event Engine](https://dashboard.eventengine.run/login) para isto. O arquiteto que está ministrando o Workshop deve lhe passar algum HASH.

# Introdução ao Gerenciamento com IAM

O AAM Identity and Access Management (IAM) permite gerenciar o acesso aos serviços e recursos da AWS com segurança. Usando o IAM, você pode criar e gerenciar usuários e grupos da AWS e usar permissões para permitir e negar o acesso aos recursos da AWS.

1. Crie um grupo IAM
Um grupo IAM é uma coleção de usuários. Os grupos geralmente são baseados na função ou função do trabalho. Eles permitem que você gerencie permissões aplicando políticas a cada grupo, e não a usuários individuais.

1.1 Abra o console do IAM em https://console.aws.amazon.com/iam/.

1.2 No painel de navegação, clique em Grupos e, em seguida, clique em Criar Novo Grupo.

1.3 Na caixa Nome do grupo, digite Administradores como o nome do grupo e clique em Próxima etapa.

1.4 Na lista de políticas, marque a caixa de seleção da política AdministratorAccess que você deseja aplicar a todos os membros do grupo. Depois clique em Next Step.

1.5 Clique em Criar grupo.

2. Crie um usuário do IAM
Um usuário está associado a credenciais permanentes e possui permissões baseadas em políticas anexadas diretamente ao usuário ou políticas anexadas a um grupo ao qual o usuário pertence.

2.1 Abra o console do IAM em https://console.aws.amazon.com/iam/.

2.2 No painel de navegação, escolha Usuários e, em seguida, escolha Adicionar usuário.

2.3 Na caixa Nome do usuário, digite Administrador como o nome do usuário. Para Tipo de acesso, marque a caixa de seleção Acesso ao Console de Gerenciamento da AWS e clique em Avançar: Permissões.

2.4 Na página Definir permissões, marque a caixa de seleção para o grupo Administradores e clique em Avançar: Tags.

2.5 Na página Adicionar Tags, escolha Avançar: Revisar.

2.6 Na página Revisão, você verá todas as opções que você fez até esse momento. Quando estiver pronto para prosseguir, escolha Criar usuário.

2.7 Para salvar as credenciais, escolha Baixar .csv e salve o arquivo em um local seguro e clique em Fechar.

# Publicar um site estático com o Amazon S3 e Amazon Cloud Front

O Amazon Simple Storage Service é um armazenamento para a Internet. Ele foi projetado para facilitar a computação em escala da web para os desenvolvedores e você também pode hospedar um site estático em um bucket do Amazon S3.

1. Crie um bucket do Amazon S3
1.1 Abra o console do Amazon S3 em https://console.aws.amazon.com/s3/.

1.2 Escolha Criar bucket.

1.3 No campo Nome do bloco, digite um nome exclusivo compatível com DNS para o seu novo bloco, por exemplo, <seu nome-> site.

O nome deve ser exclusivo em todos os nomes de bucket existentes no Amazon S3.
Depois de criar o bucket, você não poderá alterar o nome; portanto, escolha sabiamente.
Escolha um nome de intervalo que reflita os objetos no intervalo, porque o nome do intervalo é visível no URL que aponta para os objetos que você colocará no intervalo.
1.4 Para Região, escolha Leste dos EUA (Virgínia do Norte) como a região em que você deseja que o intervalo resida.

1.5 Para configurações de bucket para bloquear o acesso público, desmarque a opção Bloquear todo o acesso público.

1.6 Valide as configurações, marque Eu reconheço ... e escolha Criar bucket.

1.3 No campo Nome do bloco, digite um nome exclusivo compatível com DNS para o seu novo bloco, por exemplo, <seu nome-> site.

O nome deve ser exclusivo em todos os nomes de bucket existentes no Amazon S3.
Depois de criar o bucket, você não poderá alterar o nome; portanto, escolha sabiamente.
Escolha um nome de intervalo que reflita os objetos no intervalo, porque o nome do intervalo é visível no URL que aponta para os objetos que você colocará no intervalo.

1.4 Para Região, escolha Leste dos EUA (Virgínia do Norte) como a região em que você deseja que o intervalo resida.

1.5 Valide as configurações, marque Eu reconheço ... e escolha Criar bucket.

# Crie uma instância do Cloud9 para fazer upload do seu site estático

O AWS Cloud9 é um ambiente de desenvolvimento integrado (IDE) baseado na nuvem que permite escrever, executar e depurar seu código com apenas um navegador. 
Ele combina os recursos avançados de edição de código de um IDE, como conclusão de código, dicas e depuração passo a passo, com acesso a um servidor Linux completo para execução e armazenamento de código.

2.1 Abra o console do AWS Cloud9 em https://console.aws.amazon.com/cloud9/.

2.2 Clique em Criar ambiente.

2.3 Para o tipo de nome MyDevelopmentInstance e escolha próxima etapa.

2.4 Para as configurações de ambiente, use os valores padrão e escolha a próxima etapa.

2.5 Clique em Criar ambiente.

2.6 Aguarde alguns segundos até que seu ambiente de desenvolvimento esteja pronto, você verá a seguinte tela.

2.7 Dentro do terminal bash, execute os seguintes comandos:

Faça o download do site estático no github.

`git clone https://github.com/aurbac/static-website.git`

Faça o upload do site estático, altere o <seudominio> -website com o nome do seu bucket.

site estático do `aws s3 cp / s3: // <seudominio> -website / --recursive --exclude ".git / *"`

2.8 Abra o console do Amazon S3 em https://console.aws.amazon.com/s3/, abra seu bucket do Amazon S3 e você verá os arquivos carregados.

# Configure o bucket S3 para hospedagem de site estático

3.1 Dentro do seu bucket do Amazon S3, escolha Propriedades.
3.2 Escolha hospedagem estática de sites.
3.3 Escolha Usar este intervalo para hospedar um site e, para o tipo de documento Index index.html, copie o Terminal e clique em Salvar.

# Configure CloudFront para servir o conteúdo de forma segura

1. Vá no serviço CloudFront e clique em Criar destribuição.

1.1 Em Origin Domain Name selecione o bucket S3.

1.1 Em restrict bucket access escolha a opção YES e selecione a opção Create a New Iedntity.

1.2 Selecione a opção: Yes, Update Bucket Policy

1.3 O restante dos parametros podem ser deixados iguais.

1.4 Clique em Create distribution.


















