To-do list

[X] - mudar foto
[x] - Mudar o idioma para ingles
[X] - Criar um campo de "about"
[X] - mudar a descrição
[X] - tirar logos de tech
[x] - Adiconar certificações
[x] - adicionar posts
    [X] - Pokedex 
    [-] - Iac alura
    [-] - Curso Python
    [] - Site-Deployment - TODO
    [X] - LinkedinInfra
    [-] - K8s--Studies
    [X] - LandingPageCV
    [-] - Estudos mudblazor
    [X] - TRATADOR
    [-] - Crudlilao
    [-] - WebPage
    [X] - PulumiAWS
    [X] - challenges-repo
    [-] - POO_PY
    [] - server_connection 
[x] - adicionar cursos
[x] - aonde fazer a hospedagem do site (aws)
[X] - como fazer o pull automatico com as mudanças
[X] - Comprar um dns (marcusaloise.com)
[X] - Criar regras de segurança para o site
[] - criar outro nome de dominio para o site -> https://webpagemarcus.marcusaloise.com/ -> webpage.marcusaloise.com
[] - Criar passo a passo para a hospedagem do site com dominio e tls e https
        Criar um bucket com o nome de subdominio (webpage.marcusaloise.com)
            Ativar acesso publico e criar regras de acesso.
            {
                "Version": "2012-10-17"
                "Statement": [
                    {
                        "Sid": "AllowPublicRead",
                        "Effect": "Allow",
                        "Principal": "*",
                        "Action": [
                            "s3:GetObject"
                        ],
                        "Resource": "arn/*"
                    }
                ]
            }

            Ativar o modo site host do bucket
        Ir no route 53 e criar um CNAME com o link gerado pelo s3 no modo site host
[] - criar texto para post


-------

Coeficiente de correlação



https://mercadolibre.eightfold.ai/careers?query=IT&location=Brazil&pid=11296366&domain=mercadolibre.com&sort_by=relevance