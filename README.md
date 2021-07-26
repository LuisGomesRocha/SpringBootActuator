# SpringBootActuator

Fonte: https://www.youtube.com/watch?v=LQlypTjmgZM
Fonte: https://emmanuelneri.com.br/2017/08/06/habilitando-monitoramento-no-spring-boot/

1.	Liveness and Readiness
O estado de vitalidade de um aplicativo informa se o estado interno é válido. Se o Liveness for interrompido, isso significa que o próprio aplicativo está em um estado de falha e não pode se recuperar dele. Nesse caso, o melhor curso de ação é reiniciar a instância do aplicativo. Por exemplo, um aplicativo que depende de um cache local deve falhar em seu estado Liveness se o cache local estiver corrompido e não puder ser reparado.
O estado de Readiness informa se o aplicativo está pronto para aceitar solicitações do cliente. Se o estado de prontidão não estiver pronto, não deve rotear o tráfego para esta instância. Se um aplicativo estiver muito ocupado processando uma fila de tarefas, ele poderá se declarar ocupado até que sua carga seja gerenciável novamente.

Para começar a utilizar o Actuator nos nossos projetos Spring Boot é bem simples, apenas adicionar a dependência no projeto e automaticamente os endpoints estarão disponíveis, isso devido o conceito de autoconfiguração do Spring Boot.

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
    <version>1.5.3.RELEASE</version>
</dependency>

Os endpoints disponíveis são :
•	/health: Retorna o status da aplicação e das ferramentas relacionadas;
•	/env: Retorna os dados do ambiente, exemplo informações da JVM, sistema operacional, dados de acesso, entre outros;
•	/dump: Gera e retorna o arquivo de dump da aplicação;
•	/metrics: Retorna métricas da aplicação como: quantidade de memória, número de Threads, número de classes, uptime, entre outros;
•	/heapdump: Gera e retorna o arquivo de heapdump da aplicação;
•	/loggers: Retorna os logs da aplicação, de acordo com as configurações;
•	/info: Retorna informações configuradas no application properties, exemplo: info.app.name e info.app.version;
•	/auditevents: Retorna os eventos gerados na aplicação, exemplo acesso negado ou acesso a algum endpoint;
•	/trace: Retorna toda rota dos últimos endpoints;
•	/mappings: Retorna informações dos endpoints disponibilizados na aplicação;
•	/configprops: Retorna informações sobre as configurações da aplicação;
•	/autoconfig: Retorna informações sobre as auto configurações;
•	/beans: Retorna informações sobre os beans da aplicação.

Por padrão, os endpoints são disponibilizados no path raiz da aplicação, com isso, podemos utilizar a propriedade management.context-path do application.properties para alterar o path desses endpoints e não misturar com os endpoints da aplicação.

application.properties
1	management.context-path=/manage

Após aplicar a propriedade os endpoints vão estar disponíveis no path /manage/health
Outro detalhe, que por segurança esses endpoints necessitam de autenticação, pois eles demonstram informações de toda aplicação e do ambiente que ela está instalada, assim, em ambiente de desenvolvimento podemos desabilitar essa autenticação com a propriedade management.security.enabled=false.
application.properties
	management.security.enabled=false

Porém, não podemos desabilitar essa funcionalidade de segurança em ambientes públicos como homologação e produção, assim, podemos adicionar a dependência do spring boot security e habilitar uma autenticação simples via “basic” para autenticarmos via browser.

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
    <version>1.5.3.RELEASE</version>
</dependency>

application.properties
	management.context-path=/manage
management.security.enabled=true
security.user.name=admin
security.user.password=admin
security.basic.enabled=true

Dessa forma, utilizando o projeto Actuator é possível monitorarmos nossas aplicações Spring Boot de forma prática, além disso, o Actuator prove informações da aplicação como: valores de properties, dados de autoconfiguração, logs e também possibilita ações, como gerar dump e heapdump.

