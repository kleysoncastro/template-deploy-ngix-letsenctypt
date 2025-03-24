## Para configurar Router53 para validar cetificado Usando DNS 

!!! compose `swag-nginx.yaml`

### Passos para Resolver o Erro AccessDenied:

1. Ajustar as Permissões do IAM

Você precisa garantir que o usuário allca-api-notifyer tenha as permissões necessárias para interagir com o Route 53. Para isso, siga estas etapas:

Acesse o console da AWS e vá para a seção IAM (Identity and Access Management).

Encontre o usuário allca-api-notifyer em "Users".

Adicione permissões para acessar o Route 53. A maneira mais fácil de fazer isso é atribuindo uma política gerenciada chamada AmazonRoute53FullAccess, que dá permissões totais para o serviço Route 53.

Clique no nome do usuário allca-api-notifyer.
Vá para a aba Permissions.
Clique em Add permissions.
Selecione Attach policies directly.
Pesquise por AmazonRoute53FullAccess e marque a caixa ao lado.
Clique em Next e depois em Add permissions.

### No `/config/dns-conf/router53.ini`

```ini
dns_route53_access_key = YOUR_AWS_ACCESS_KEY
dns_route53_secret_key = YOUR_AWS_SECRET_KEY
```

### No docker compose nginx.yaml

```yaml
- URL=deploy.allca.eng.br
- SUBDOMAINS=wildcard
```

- URL = dominio base
- SUBDOMAINS= lista de subdominios ex: `SUBDOMAIS=api,app,deploy,test`

## Configurações Nginx

No diretporio `config/nginx/site-confs` esta o `.conf`

No diretorio `config/nginx/site-confs/default.conf` deve ser substuido pelo `./nginx/default.conf` para que outras `*.conf` possam ser aplicadas

Também no diretório `./nginx` tem outros arquivos de exemplos
