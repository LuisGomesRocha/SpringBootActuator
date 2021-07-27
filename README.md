# SpringBootActuator

<h4 align="center"> 
	🚧  Orange Talents  🚀 Em construção...  🚧
</h4>

<p align="center">🚀 Formulário de Auto percepção: Health Check, Readiness & Liveness Check e Spring Boot Actuator 🚀 </p>



<h1 align="center">
    <a href="https://www.youtube.com/watch?v=LQlypTjmgZM">🔗Spring Boot Tutorial - Spring Boot Actuator</a>
</h1>

<h1 align="center">
    <a href="https://emmanuelneri.com.br/2017/08/06/habilitando-monitoramento-no-spring-boot/">🔗Habilitando monitoramento no Spring boot</a>
</h1>



### Liveness and Readiness

<p align="justify"> :robot: O estado de vitalidade de um aplicativo informa se o estado interno é válido. Se o Liveness for interrompido, isso significa que o próprio aplicativo está em um estado de falha e não pode se recuperar dele. Nesse caso, o melhor curso de ação é reiniciar a instância do aplicativo. Por exemplo, um aplicativo que depende de um cache local deve falhar em seu estado Liveness se o cache local estiver corrompido e não puder ser reparado.
O estado de Readiness informa se o aplicativo está pronto para aceitar solicitações do cliente. Se o estado de prontidão não estiver pronto, não deve rotear o tráfego para esta instância. Se um aplicativo estiver muito ocupado processando uma fila de tarefas, ele poderá se declarar ocupado até que sua carga seja gerenciável novamente.:robot: </p>


### Actuator

<p align="justify"> :robot: Para começar a utilizar o Actuator nos nossos projetos Spring Boot é bem simples, apenas adicionar a dependência no projeto e automaticamente os endpoints estarão disponíveis, isso devido o conceito de autoconfiguração do Spring Boot.:robot: </p>

```

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
    <version>1.5.3.RELEASE</version>
</dependency>

```

### Os endpoints disponíveis são :

- [x] /health: Retorna o status da aplicação e das ferramentas relacionadas;
- [x] /env: Retorna os dados do ambiente, exemplo informações da JVM, sistema operacional, dados de acesso, entre outros;
- [x] /dump: Gera e retorna o arquivo de dump da aplicação;
- [x] /metrics: Retorna métricas da aplicação como: quantidade de memória, número de Threads, número de classes, uptime, entre outros;
- [x] /heapdump: Gera e retorna o arquivo de heapdump da aplicação;
- [x] /loggers: Retorna os logs da aplicação, de acordo com as configurações;
- [x] /info: Retorna informações configuradas no application properties, exemplo: info.app.name e info.app.version;
- [x] /auditevents: Retorna os eventos gerados na aplicação, exemplo acesso negado ou acesso a algum endpoint;
- [x] /trace: Retorna toda rota dos últimos endpoints;
- [x] /mappings: Retorna informações dos endpoints disponibilizados na aplicação;
- [x] /configprops: Retorna informações sobre as configurações da aplicação;
- [x] /autoconfig: Retorna informações sobre as auto configurações;
- [x] /beans: Retorna informações sobre os beans da aplicação.

<p align="justify"> :robot: Por padrão, os endpoints são disponibilizados no path raiz da aplicação, com isso, podemos utilizar a propriedade management.context-path do application.properties para alterar o path desses endpoints e não misturar com os endpoints da aplicação. :robot: </p>

```
application.properties
management.context-path=/manage

```


<p align="justify"> :robot: Após aplicar a propriedade os endpoints vão estar disponíveis no path /manage/health
Outro detalhe, que por segurança esses endpoints necessitam de autenticação, pois eles demonstram informações de toda aplicação e do ambiente que ela está instalada, assim, em ambiente de desenvolvimento podemos desabilitar essa autenticação com a propriedade management.security.enabled=false. :robot: </p>


```
application.properties
management.security.enabled=false
```

<p align="justify"> :robot: Porém, não podemos desabilitar essa funcionalidade de segurança em ambientes públicos como homologação e produção, assim, podemos adicionar a dependência do spring boot security e habilitar uma autenticação simples via “basic” para autenticarmos via browser. :robot: </p>


```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
    <version>1.5.3.RELEASE</version>
</dependency>

```

### application.properties

```
management.context-path=/manage
management.security.enabled=true
security.user.name=admin
security.user.password=admin
security.basic.enabled=true

```

<p align="justify"> :robot: Dessa forma, utilizando o projeto Actuator é possível monitorarmos nossas aplicações Spring Boot de forma prática, além disso, o Actuator prove informações da aplicação como: valores de properties, dados de autoconfiguração, logs e também possibilita ações, como gerar dump e heapdump. :robot: </p>



