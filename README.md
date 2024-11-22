# foundry-aws-docker

# AWS Policies

### Observação: Existe um bug na V12 do foundry, apenas o release 12.329 funciona a integração com AWS

## IAM


Criar um usuário e anexar a politica abaixo
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:ListBucket",
                "s3:DeleteObject",
                "s3:PutObjectAcl"
            ],
            "Resource": [
                "arn:aws:s3:::<bucket name>",
                "arn:aws:s3:::<bucket name>/*"
            ]
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": "s3:ListAllMyBuckets",
            "Resource": "*"
        }
    ]
}
```

## Bucket

### Policie

Logo após criar o bucket, anexe a politica abaixo
```
{
    "Version": "2012-10-17",
    "Id": "Policy1732279046787",
    "Statement": [
        {
            "Sid": "Stmt1732279041364",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": [
                "arn:aws:s3:::<bucket name>",
                "arn:aws:s3:::<bucket name>/*"
            ]
        }
    ]
}
```
**Importante**: Ativar ACS em propriedade do objeto (Object Property) e deixar o bucket publico, por isso, não coloque dados sensiveis

### CORS
```
[
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "GET",
            "POST",
            "HEAD",
            "PUT"
        ],
        "AllowedOrigins": [
            "*"
        ],
        "ExposeHeaders": [],
        "MaxAgeSeconds": 3000
    }
]
```

## aws.json

No arquivo aws.json neste repositorio, colocar as configurações corretas, a access key você consegue indo no usuario que você criou, um pouco para baixo terá chaves de acesso e você vai clicar em criar chaves de acesso. Dentre todas as opções você vai selecionar **Serviço de terceiros** e baixar as chaves para sua maquina.

Exemplo:
```
{
    "region": "us-east-1",
    "buckets": ["meuprimeiros3-bucket"],
    "credentials": {
      "accessKeyId": "<acces key>",
      "secretAccessKey": "<secret access key>"
    }
}
```

Tudo pronto, sem dificuldades.