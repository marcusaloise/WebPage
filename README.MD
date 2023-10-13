# LandingPage|CI/CD|Github Actions

## Sobre:

Um currículo online em formato de página web para apresentar projetos principais e certificados de cursos ou exames.

## Como foi feito:
O site em si foi construído usando apenas HTML/CSS e possui algumas funcionalidades em JavaScript. No entanto, o principal foco do projeto foi a implementação de uma esteira de CI/CD.

Essa esteira é construída usando o GitHub Actions, e o que acontece nela?

Basicamente, sempre que ocorre um commit na branch main, o GitHub identifica o push e realiza uma sincronização dos arquivos enviados com os arquivos armazenados em um bucket S3 da AWS. Em seguida, ele compara se houve alguma alteração. Se houver alguma alteração, ele substituirá o arquivo antigo pelo mais recente. Isso elimina a necessidade de realizar manualmente o upload do arquivo mais recente para o bucket.

## Como funciona o CI/CD:

Existe um arquivo yml dentro de diretorio .github/workflows/main.yml que segue a seguinte configuração.

``````yaml
name: Upload Website

on:
  push:
    branches:
    - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@v1

    - name: Configure AWS Credentials
      uses: aws-actions/configure-aws-credentials@v1
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: us-east-1

    - name: Deploy static site to S3 bucket
      run: aws s3 sync ./ s3://webpage.marcusaloise.com --exclude '.git*/*'

``````

## Como utilizar:

Podemos observar no modelo acima que existem informações críticas no arquivo YAML, como o aws-access-key-id e aws-secret-access-key. Para evitar a exposição pública desses dados, o GitHub permite configurá-los como variáveis armazenadas internamente, semelhante às chaves SSH usadas para commits e pushes. Para utilizar essa abordagem, é necessário que o Git reconheça o arquivo YAML. Portanto, precisamos criar uma pasta chamada .github/workflows e, dentro dela, colocar o arquivo YAML.


Se você deseja aplicar a mesma ideia para fazer o deploy de um site estático em um S3, como eu fiz, siga os seguintes passos:

- Crie o seu bucket S3 e ative a opção "Hospedagem de site estático", e faça o apontamento para o seu index.html

- Em seguida, crie uma distribuição no CloudFront com um certificado associado ao seu domínio.

- Posteriormente, faça a associação da sua distribuição ao seu domínio nas configurações do Route 53. Isso pode ser feito por meio da função CNAME.

- Algo muito importante de ser falado e que o seu s3 precisa ter o mesmo nome de seu site como no exemplo:

        s3 = webpage.marcusaloise.com
        site = webpage.marcusaloise.com

`não sei bem o motivo dessa regra mas quando eu tentei fazer com nomes diferentes me causava erro ao realizar o apontamento para o bucket e o dominio.`