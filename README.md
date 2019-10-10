# docs-serasa

# Antes de Começar:

## 1 - Listar o conteúdo do user_name.keytab

- klist -kt user_name.keytab
- Ex: 

## 2 - Criar um ticket com  o user_name.keytab

- kinit -kt user_name.keytab pricipal_user_name@DOMAIN

## 3 - Fazer o export da variável KAFKA_OPTS

export KAFKA_OPTS="-Djava.security.auth.login.config=/PATH/jaas.conf"


## 4 - Criando Kafka-Producer



## 5 - Criando Kafka-Consumer
