---
layout: post
title:  "Porque utilizar SSG para criação de blogs"
date:   2017-06-13
categories: Blog
---

Decidimos criar um blog e o primeiro passo é fazer uma pesquisa sobre
qual a melhor tecnologia para este empreendimento.
Ao identificar as características de cada opção, percebemos que
nem sempre é mais indicado seguir o que a maioria está fazendo.
Neste post vou explicar porque é mais indicado criar um blog utilizando um
**Static Site Generator** (SSG) ao invés de um **Content Management System** (CMS).

Sistemas de Gerencimento de Conteúdo
------------------------------------

Geralmente os sistemas de gerenciamento de conteúdo (CMS) são sites dinâmicos.
Ou seja, são construídos com uma linguagem para WEB (como PHP, Java, Ruby, etc.),
utilizam um banco de dados (MySQL, Postgress, Oracle, etc.)
e funcionam sobre um servidor de aplicações (Apache, Nginx, etc.).

Provavelmente você já tenha ouvido falar de **Workpress**,
o CMS mais utilizado no mundo para criação de blogs.
Ele é construído em PHP com MySQL.

Para muitos tipos de aplicações este Stack talvez seja a melhor opção,
principalmente quando você **precisa** gerar HTML/CSS/JS dinamicamente,
ou responder a um evento em tempo real.
Mas para a criação de um blog nem sempre há essa necessidade.

![Wordpress](/assets/images/wordpress.png)

No passado era bastante justificável a utilização de CMSs para blogs,
um blog geralmente precisa de um controle de acesso para o gerenciamento do conteúdo,
um formulário de contatos, gestão de comentários, etc.
E para implementar isso era necessário ter as soluções no próprio sistema de gestão do blog.
Mas hoje em dia todas essas necessidades podem ser atendidas por sistemas terceiros.

Por exemplo, para gestão de comentários nós podemos utilizar o [Disqus](https://disqus.com/),
ou até mesmo o [Facebook](https://developers.facebook.com/).
Para formulário de contatos também existem vários serviços como [Formspree](https://formspree.io) ou
[Formbucket](https://www.formbucket.com/).
Para controle de acesso de gestão de conteúdo, podemos utilizar o próprio [Github](https://github.com/).

Além de podemos utilizar sistemas terceiros para essas partes dinâmicas do nosso blog.
CMSs como o Workdpress tem algumas desvantagens que já me deram algumas dores de cabeça no passado.

A principal desvantagem é que por ser o CMS mais utilizado no mundo,
o Wordpress sofre ataques harckers constantemente.
É frequente a descoberta de uma ou outra [brecha de segurança grave no Wordpress](https://www.google.com.br/search?q=falha+de+segurança+grave+no+wordpress).
Eu mesmo já tive blog invadido por causa de uma dessas brechas de segurança.

Também já perdi as contas de quantas vezes meu servidor MySQL já caiu quando o meu blog [{ Dicas de Programação }](http://dicasdeprogramacao.com.br/) sofreu ataques DDOS.

Uma outra desvantagem forte dos CMSs é que o histórico de alterações de conteúdo fica no banco de dados.
Eu sou totalmente contra essa característica dos CMS
por causa do fator "gestão de banco de dados" que isso implica.
É necessário ter um processo rígido de backup e também de um bom conhecimento
sobre a forma como o CMS faz esse gerenciamento de versões.

Todo programador curte os sistemas de gerenciamento de versões como GIT, SVN, etc.
Por que não utilizar esses sistemas para gerenciar o blog inteiro, principalmente o seu conteúdo?

Por fim aplicações dinâmicas trazem uma série de preocupações para manter o site no ar.
Cache, persistência, segurança, infra-estrutura web, etc.
Por isso, manter um blog com um CMS pode ficar caro ao longo do tempo, com o aumento das visitas.

Geradores de Sites Estaticos
----------------------------

Apresentados esses problemas, os _Geradores de Sites Estáticos_
vem se mostrando a melhor solução para blogs.

Os **Static Site Generators** (SSG) são processadores que unem conteúdo,
algumas configurações, tema e plugins para criar as páginas do site.
O resultado é uma pasta que contém os arquivos estáticos que compõem o site.
Depois do site gerado você pode hospedá-lo em qualquer servidor básico de conteúdo estático.

O próprio Github tem um projeto chamado [Github Pages](https://pages.github.com/)
que hospeda o site estático gratuitamente com alguns [limites de uso](https://help.github.com/articles/what-is-github-pages/#usage-limits).

![Static Site Generator](/assets/images/ssg.png)

Existem SSGs em diferentes linguagens como você pode conferir [neste link](https://www.staticgen.com/).

Eu uso e gosto bastante do [Pelican](https://blog.getpelican.com/), que é feito em Python.
Mas o mais famoso é o [Jekyll](https://jekyllrb.com/), feito em Ruby,
que inclusive nós estamos utilizando para gerar este blog.

Com os SSGs obtemos algumas vantagens em relação aos CMSs para blogs.

- Controle de versão para o conteúdo do blog;
- Escalabilidade para acesso em massa do blog (inclusive ataques DDOS);
- Proteção contra ataques (eles não tem o quê invadir);
- Escrever conteúdos para o blog como se estivesse programando
(Abre o código do blog na sua IDE favorita e divirta-se);
- É mais barato! Qualquer servidorzinho de site estático é mais barato
que uma hospedagem de site dinâmico.
- Estabilidade. Por exemplo eu armazeno meus blogs no S3 da Amazon (barato).
O dia que a Amazon cair você não poderá ver suas séries favoritas da Netflix.

Além disso, é possível utilizar ferramentas de integração contínua (como Travis-CI, Cicle-CI, Jenkins, etc),
para fazer o deploy do blog direto no seu servidor de site estático.

Eu, particularmente, armazeno os códigos-fonte dos meus blogs no meu [github](https://github.com/gustavofoa)
e uso o [Travis-CI](https://travis-ci.org/) para fazer deploy automaticamente deles no S3 da Amazon
a cada commit/push que eu faço no master do meu repositório remoto.

![Travis-CI](/assets/images/travis-ci-gustavo.png)

Concluindo ...
--------------

Muita gente tem preconceito de SSGs por exigir um pouco mais de conhecimento técnico
em comparação aos CMSs como Wordpress.
Temos que concordar, criar um blog com Wordpress é muito simples e
tem várias hospedagens que fornecem um serviço de instalação do Wordpress
com apenas 1 clique. O dono do blog não precisa se preocupar (por enquanto) com PHP, MySQL, Apache, etc.

Mas ao mesmo tempo que a barreira de entrada do Wordpress é muito pequena,
todo mundo que cria um blog, quer que ele cresça, e isso significa que
será necessário se preocupar com questões técnicas para mantê-lo no ar.

Além disso, configurar e personalizar temas e plugins deixa de tão trivial quanto instalar o Wordpress,
sendo necessário contratar programadores e designers para deixar o blog como o blogueiro quer.

Os SSGs antecipa essa parte para a criação do blog, mas depois que ele já está criado,
configurado, personalizado, não tem mais preocupação nenhuma. Só criar conteúdo!

Bora compartilhar conhecimento!

Algo a compartilhar sobre o assunto? Escreva nos comentários aqui em baixo ...
