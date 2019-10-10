# Criando Kafka-Producer e Kafka-Consumer com SSL e Kerberos

# Antes de Começar:

## 1 - Listar o conteúdo do user_name.keytab

- klist -kt user_name.keytab

- Exemplo: 
``` sh
[root@hostname]# klist -kt user_name.keytab
Keytab name: FILE:user_name.keytab
KVNO Timestamp           Principal
---- ------------------- ------------------------------------------------------
   1 02/19/2019 10:51:21 principal_user_name@DOMAIN

[root@hostname]#

```
## 2 - Criar um ticket com  o user_name.keytab

- kinit -kt user_name.keytab pricipal_user_name@DOMAIN

- Exemplo:
``` sh
[root@hostname]# kinit -kt user_name.keytab pricipal_user_name@DOMAIN

[root@hostname]# klist
Ticket cache: FILE:/tmp/krb5cc_0
Default principal: pricipal_user_name@DOMAIN

Valid starting       Expires              Service principal
10/10/2019 16:45:38  10/11/2019 02:45:38  krbtgt/BR.DOMAIN@BR.DOMAIN.LOCAL
        renew until 10/11/2019 16:45:38
[root@hostname]#
```
## 3 - Fazer o export da variável KAFKA_OPTS

export KAFKA_OPTS="-Djava.security.auth.login.config=/PATH/jaas.conf"

- Exemplo:
``` sh
[root@hostname]# export KAFKA_OPTS="-Djava.security.auth.login.config=/PATH/jaas.conf"

[root@hostname]# echo $KAFKA_OPTS
-Djava.security.auth.login.config=/PATH/jaas.conf
[root@hostname]#

```

## 4 - Criando Kafka-Producer

- Producer: kafka-console-producer --broker-list hostname_of_kafka_broker01:9093,hostname_of_kafka_broker02:9093,hostname_of_kafka_broker03:9093 --topic name_of_topic --producer.config producer.properties

- Exemplo:
``` sh
[root@hostname]# kafka-console-producer --broker-list hostname_of_kafka_broker01:9093,hostname_of_kafka_broker02:9093,hostname_of_kafka_broker03:9093 --topic name_of_topic --producer.config producer.properties
[root@hostname]#
>_

```
## 5 - Criando Kafka-Consumer
- Exemplo:
``` sh
[root@hostname]# kafka-console-consumer --bootstrap-server hostname_of_kafka_broker:9093 --topic name_of_topic --consumer.config consumer.properties
[root@hostname]#
> _
```
## Obs: Antes de criar o producer e o consumer, crie os arquivos de configuração: jaas.conf, producer.properties, consumer.properties;

## Pré-requisitos: O tópico precisa existir, ter as permissões de Tópico:ALL e Consumergroup: READ e DESCRIBE.
