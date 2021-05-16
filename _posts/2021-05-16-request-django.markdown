---
layout: post
title:  🇧🇷 "def get_self_request def_create_self_request. Mas, afinal, o que é request?"
date:   2021-05-16 14:04:26 -0300
categories: jekyll update
---

Uma parte essencial da funcionamento da internet como a temos em nosso cotidiano diz respeito à requests. Nesse artigo vamos discorrer sobre requests, sua importância, em que parte do fluxo de comunicação entre sistemas ela se encaixa, e finalmente, como ela existe no contexto do Django.


First things first: Request é traduzido para português como requisição, e requisições não são nada mais nada menos do que pedidos. Como nos lembra a gramática, quem pede, pede alguma coisa. No caso de sistemas de web, pede-se recursos. Recursos podem ser imagens do seu IG, vídeos do YT, ou uma página de texto da Wikipedia. Esses recursos retornarão em forma de Responses.


Como toda comunicação de qualidade, é necessário que haja uma linguagem comum entre o emissor da mensagem e o destinatário. A essa linguagem comum damos o nome de protocolo. Em sistemas web, o protocolo de comunicação é o HTTP, responsável pelo tratamento de pedidos e respostas entre cliente e servidor na World Wide Web.


Cliente é todo sistema que requisita um recurso e servidor é o sistema que serve o recurso. Por exemplo, o seu browser (Chrome, Firefox, Safari, …) é um cliente. O Google, por exemplo, tem seus servidores que fornecem as respostas com os recursos requisitados.


![image](../../../../../../images/primeiro_post/cliente_servidor.jpeg){:class="img-responsive", description="http://www.ead.ufrpe.br/acervo-digital-eadtec/node/685"}


Sendo que existem tantos sites, servidores, usuários de computadores (smartphones, laptops, desktops,…), como a requisição por www.google.com do seu browser chega ao Google?

O link www.google.com é uma URL, Uniform Resource Locator, que no bom e velho português é um Localizador Uniforme de Recursos, um nome bem descritivo. E como funciona? Muito semelhante ao sistema de correios.

Supondo seu endereço escrito com o padrão americano: **123** (domínio: número da residência), **Times Square St.**(domínio: rua), **Nova York** (domínio: cidade), **Nova York** (domínio: estado).

O endereço _www.google.com_. é então descrito em detalhes:
Cada parte entre os pontos é um domínio.


- _._ : o ponto não aparece para nós, mas ele existe e significa o DNS raiz;
- _com_ : é um dos nomes de domínios de nível mais alto na hierarquia de nomes. Outros são .org, .edu, .net, .gov, …;
- _google_ : é um nome de domínio. A identificação primária do serviço que você deseja na internet;
- _www_ : é um subdomínio de domínio, como mail, wiki;


![image](../../../../../../images/primeiro_post/resolucao_de_nomes.jpeg){:class="img-responsive"}


É notável que estamos falando em nomes o tempo todo. No entanto, os computadores não se comunicam dessa forma, esses são nomes mais amigáveis para nós humanos lermos, apenas. A realidade é que para os sistemas computacionais o endereço www.google.com é 172.217.30.78.


Para traduzir um nome em um endereço de números, a internet usa servidores de DNS — Domain Name System. O sistema de nomes de domínios traduz os nomes de domínio para endereços de computadores, os IPs. Talvez você já tenha visto números do tipo _192.168.0.1_ ou _127.0.0.1_. Esses são exemplos de endereços IPs — Internet Protocol.


A resolução de nomes funciona assim: Quando o browser faz uma requisição, ele pergunta ao servidor de nomes (servidor de DNS) mais próximo pelo IP do domínio que ele quer. O servidor de DNS guarda uma tabela com tudo que já procuraram e que ele soube resolver, mas ela pode ficar desatualizada ou ele não ter resolvido esse nome antes, quando isso ocorre, ele manda o request para o próximo servidor de DNS, e assim continua a busca pelo IP do domínio que se quer.

![image](../../../../../../images/primeiro_post/dns.png){:class="img-responsive"}

**Até aqui vimos como funciona o request na arquitetura Cliente-Servidor, vimos também que tem que haver um protocolo para que todos se comuniquem efetivamente, que os nomes dos sites são traduzidos para endereços de IPs e como eles são encontrados.**

Falta ainda saber como é esse protocolo de comunicação que rege a conversa entre os clientes e servidores, o HTTP.

Quando vamos pedir algo costumamos usar verbos que representam ações, assim também o HTTP funciona. Por exemplo, quando o browser quer algum recurso ele usa o **GET**, já quando ele quer enviar um recurso ele usa o **POST**, quando ele quer apagar um recurso ele usa o **DELETE** — há ainda o **PUT**, **HEAD**, **CONNECT**, **OPTIONS**, **TRACE** (https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Methods).

Juntando tudo, quando se busca por www.google.com no browser, o recurso é a URL (www.google.com), a ação que o cliente quer fazer é **GET**, e o protocolo eh _HTTP 2_. Então o request fica assim:

![image](../../../../../../images/primeiro_post/request.png){:class="img-responsive"}

Para cuidar de uma requisição existe um software chamado web server, ele espera o cliente enviar sua conexão e logo após o request. Antes de criar a conexão entre cliente e servidor, primeiro se estabelece uma conexão TCP, que utiliza um par “IP+porta” chamado de socket, que é o que identifica seu PC como único na rede. É necessário um par de sockets para identificar dois extremos (endpoints) na rede. Para um cliente é necessário apenas um socket e estabelecer a conexão, mas para um server há um processo mais longo, que é ilustrado no seguinte esquema:

![image](../../../../../../images/primeiro_post/listen_server.png){:class="img-responsive"}


E finalmente chegamos ao Django! Como parte de suas funcionalidades , ele processa os requests e envia respostas. Para que ele funcione, é necessário que haja o web server para fazer as conexões. No entanto, no mundo Python, linguagem que o Django utiliza, há um formato específico e diferente para a requisição, o que faz necessário que haja uma uniformidade de comunicação entre o web server e o mundo python. A esse formato dá-se o nome de WSGI (Web Server Gateway Interface), que se pronuncia “wiz-gee”.

![image](../../../../../../images/primeiro_post/middleware.png){:class="img-responsive"}

Como programadora ou programador Django, você quer receber esses requests e devolver recursos/responses. Isso é feito através da configuração de urls que levarão às views, onde está a lógica de processamento dos dados — elas podem buscar no banco de dados por registros — e na volta as views formam as responses e fazem o caminho inverso até chegar ao browser (setas pontilhadas).

![image](../../../../../../images/primeiro_post/dns_until_pc.png){:class="img-responsive"}

Espero que tenha ajudado a responder à pergunta do título!


Leituras adicionais:


- [https://docs.djangoproject.com/en/3.0/ref/request-response/] - Django Request Response doc;

- [https://ruslanspivak.com/lsbaws-part1/] - Server;

- [https://www.mattlayman.com/understand-django/browser-to-django/] - Bbrowser to Django;

- [https://medium.com/@ksarthak4ever/django-request-response-cycle-2626e9e8606e] - Django request response cycle.