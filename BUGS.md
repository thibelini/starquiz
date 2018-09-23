Problemas com a arquitetura:
- falta de padrão entre uso do @ngInject vs. Artefato.$inject: 
- component location criado não faz sentido fora do módulo Dashboard
- component location tem responsabilidades que não são dele (controle de cache por ex... ele deveria apenas renderizar o item e controlar o loading baseado em um attr do data/item)
- "spinner"/loader usado no component location foi implementado usando jQuery e é controlado fora do component usando seletores jQuery
- controle de width/screen dentro do DashboardController: poderia/deveria ser abstraido p/ algo geral da app, provavelmente no MainController
- lógica de "find by pks" dentro do DashboardController, ao invés de encapsulada em um service
- parser do response.data dentro do DashboardController: deveria ser abstraido no DashboardService
- confusão de responsabilidades entre o DashboardService, DashboardController e component location


Problemas com uso do AngularJs
- não há entendimento sobre os recursos disponíveis como @ngInject
- controle de estado do DOM do "spinner" usando jQuery/angular.$ desnecessariamente, com mais de uma interação com o DOM por método (poderia/deveria ser u m ng-if/ng-show com controle do estado em um booleano no item da lista)
- ng-app na tag html, poderia/deveria estar em um container dentro do body
- Lista de itens do dashboard sem ng-repeat, duplicando itens na mão no template do Dashboard
- Directive do component location é usada como element, sem replace:true, gerando um DOM inválido
- routes do Dashboard deveriam ser declaradas no modulo do Dashboard


Problemas com uso de javascript
- 'use strict'; em todos arquivos fora da IIFE
- console.log('Plus Ultra!'); na inicialização de um controller
- attrs keys do JSON de i18n message-en-US.json e message-pt-BR.json estão como texto normal, usando espaços etc
- uso do $interval sem controle de estado das requisições... deveria usar um timer com timeout, controlar o final de todas as requisições com $q.all e iniciar um novo timer para evitar disparar requisições sequenciais caso o servidor apresente alguma lentidão, embora o tempo seja de 10 minutos
- setando um array como cookie para controlar cache.

Problemas com CSS
- uso de tag-selectors de maneira global
- nomenclatura de classes sem um padrão consistente (.container vs. .dashboard-weather e .dashboard-weather-list)
- mixin p/ o attr color, ao invés de variáveis ou extensões, que só é usado em um único arquivo, em apenas uma declaração, embora tenham cores espalhadas em outros arquivos
- falta de padrão de unidades de medida relativas: uso de "%", "em", "vh" e "vw" em um mesmo contexto não faz o menor sentido
- query selector de screen width considerando unidades relativas em "em" esperando tratar uma resolução p/ tablets/mobile não faz sentido

Outros problemas:
- Confusão entre termos "universalização" vs "internacionalização" demonstra pouco contato com i18n e l10n
- versão desatualizada do AngularJs, embora o projeto seja novo.
- Arquivo "Makefile" foi criado sem target alguma e com lowercase, o que não é reconhecido pelo make
- Arquivo .yo-rc.json não é usado
- Arquivo .bowerrc com declarações default
- eslint extremamente permissivo
- $logProvider em modo debug sem parametrização p/ dev/prod

Problemas com testes
- Teste e2e não roda, pois importa um arquivo que não existe
- Teste com jasmine tem variáveis declaradas de forma global, um arquivo de mock que não é usado, pois o código está duplicado dentro do main.js
- Todos testes em um único arquivo, que se chama main.js, embora esteja relacionado com o módulo de dashboard