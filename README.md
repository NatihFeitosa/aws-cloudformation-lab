> **AVISO:** O conteúdo deste documento foi organizado e estruturado com o auxílio de uma Inteligência Artificial. No entanto, todo o conhecimento, insights e anotações aqui presentes são de autoria própria, refletindo minha compreensão e aprendizado durante as aulas do módulo.

# Estudos sobre Infraestrutura como Código com AWS CloudFormation

### 1. Objetivo

Este documento serve como um repositório de anotações e insights adquiridos durante o estudo sobre AWS CloudFormation, consolidando o aprendizado sobre a automação e o provisionamento de recursos na nuvem AWS.

### 2. O que é AWS CloudFormation?

AWS CloudFormation é um serviço que permite modelar, provisionar e gerenciar recursos da AWS e de terceiros de forma automatizada. Ele funciona como uma ferramenta de **Infraestrutura como Código (IaC)**, onde a infraestrutura é descrita em arquivos de texto (templates) que podem ser versionados e reutilizados. O serviço em si é gratuito, e o pagamento é feito apenas pelas "stacks" (conjunto de recursos) que são efetivamente criadas.

### 3. Conceitos-Chave e Sintaxe

Os templates do CloudFormation são escritos em formato JSON ou YAML. Neles, descrevemos os recursos que desejamos criar. Por exemplo, para definir um bucket S3, a sintaxe seria algo como:

-   `AWS::S3::Bucket`: Define o tipo de recurso, neste caso, um bucket S3.
    -   `DeletionPolicy`: Define o que acontece com o bucket se a stack for deletada (por exemplo, `Retain` para manter os dados).
    -   `AccessControl`: Define as permissões de acesso ao bucket (ex: `PublicRead`).
    -   `LifecycleConfiguration`: Permite criar políticas de ciclo de vida para os objetos, como movê-los para uma classe de armazenamento mais barata após um certo tempo.

### 4. Principais Funcionalidades

-   **Templates Reutilizáveis:** É possível criar templates próprios ou utilizar modelos prontos. Esses templates podem ser armazenados em um repositório Git, permitindo o versionamento da infraestrutura.
-   **Provisionamento Simplificado:** O CloudFormation pré-configura todos os dados dos recursos descritos no template, permitindo que uma infraestrutura complexa seja criada ou replicada "de uma vez só", com poucos cliques.
-   **Gerenciamento Centralizado:** A configuração e o gerenciamento das stacks e templates são feitos diretamente pela interface da AWS.

### 5. Caso de Uso: Criando um Firewall e um Servidor Web (Apache)

Em uma das anotações, foi mencionado "Para criar stacks de firewall, sobe o Apache". Vamos detalhar o que isso significa:

* **O que é o Apache?** Apache HTTP Server é um dos softwares de servidor web mais populares do mundo. É ele quem "serve" as páginas de um site para os visitantes que acessam pelo navegador. "Subir o Apache" significa instalar e iniciar esse software em um servidor.

* **Como o CloudFormation faz isso?** O CloudFormation orquestra todo o processo. Em um único template, ele pode:
    1.  **Criar o Firewall:** Provisionar um *Security Group*, que funciona como um firewall virtual, definindo regras como "liberar o acesso na porta 80" (HTTP, para sites).
    2.  **Criar o Servidor:** Provisionar uma instância EC2 (um servidor virtual).
    3.  **Instalar e "Subir" o Apache:** Através de um script de inicialização (*User Data*) dentro da configuração da instância EC2, o CloudFormation instrui o servidor a, assim que for criado, instalar e iniciar o Apache automaticamente.

Dessa forma, com um único comando, o CloudFormation cria a regra de firewall, o servidor e já deixa o site no ar.

### 6. Insight Pessoal: CloudFormation vs. Imagem EC2 (AMI)

A melhor forma de resumir o CloudFormation é como um **criador de "plantas baixas" (templates) para recursos AWS**. A interface permite que, a partir de um arquivo JSON ou YAML, um ou vários recursos sejam criados de forma padronizada e repetível.

A analogia com o conceito de **Imagem do EC2 (AMI)** é excelente:
* Uma **AMI** é um "molde" de um servidor (com sistema operacional e softwares instalados).
* Um **template do CloudFormation** é um "molde" da infraestrutura inteira (servidores, bancos de dados, regras de rede, buckets S3, etc.), podendo ser usado para recriar o ambiente completo em praticamente todos os serviços da AWS.
