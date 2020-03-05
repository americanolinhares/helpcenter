---
id: criando-bot-arquitetura-router-empresa
title: Criando um bot router com subbots para uma empresa fictícia
sidebar_label: Criando um bot router com subbots para uma empresa fictícia
---

Para exemplificar como criar uma arquitetura de bot router e subbots no BLiP, implementaremos um exemplo desta arquitetura para uma empresa fictícia, utilizaremos o maximo de funcionalidades do BLiP para compor este bot. Neste exemplo, nossa empresa fictícia se chamará **Company**.

## Descrição da empresa

A **Company** é uma empresa do ramo de serviços de internet, assim sendo é possivel contratar e gerenciar seu plano para sua moradia. A empresa necessita que através do bot, seus clientes possam:

* Pesquisar valores dos planos de internet disponiveis;
* Contratar planos de internet;
* Cancelar planos de internet;
* Mudar o plano de internet contratado;
* Obter fatura mensal;
* Conversar com o atendente.

## Desenvolvendo o bot

A primera tarefa será a criação da sua organização, neste exemplo, como já apresentado a organização é **`Company`**.

![Criando sua organização](/img/router/criando-bot-arquitetura-router-empresa-1.png)
<br>

Em suma, a arquitetura deste bot foi modelado com um router e três subbots, o desenvolvimento de cada um destes componentes será apresentado invidualmente logo abaixo.

### Router
Vamos começar criando o router de nome `Company Router`:

![Criando router](/img/router/criando-bot-arquitetura-router-empresa-2.png)

Após este processo é necesssario [configurar os serviços no bot router](criando-bot-com-3-subbots#passo-5-configurando-os-servicos-no-bot-router), conectando os subbots criados com router. Como vamos utilizar [o contexto do router ativado](recuperando-infomacoes-contatos-subbots#contexto-do-roteador-ativado) em todos os subbots, todas informações do subbots serão centralizadas no router. 

Alguns dos nossos bots irão utilizar Inteligencia Artificial, configure um provedor:

* [Como configurar o DialogFlow como um provedor de Inteligência Artificial](../ai/nlp/como-configurar-dialogflow)
* [Como configurar o Watson Assistant como um provedor de Inteligência Artificial](../ai/nlp/como-configurar-watson)
* [Como configurar LUIS como um provedor de Inteligência Artificial](../ai/nlp/como-configurar-luis)

Para cada funcionalidade disponivel aos clientes, teremos uma intenção, logo são: 

* Adquirir Plano: Pesquisar valores dos planos de internet disponiveis, contratar planos de internet;
* Cancelar: Cancelar planos de internet.
* Fatura:  Obter fatura mensal.
* Mudar plano: Mudar o plano de internet contratado.
* Atendente: Conversar com o atendente.

Você pode importar as intenções no arquivo abaixo, [sabia como](../nlp/como-exportar-base-conhecimento).

* [intencoes.json]()

Não apenas, utilizaremos o atendimento humano em alguns subbots, dessa forma realize todas as configurações:

* [Como ativar o BLiP Desk como um canal de atendimento](../helpdesk/blipdesk/como-ativar-blip-desk-canal)
* [Como realizar um atendimento através do BLiP Desk](../blipdesk/como-realizar-um-atendimento-atraves-do-blip-desk)
* [Gerenciando equipes de atendimento no BLiP Desk](../helpdesk/blipdesk/gerenciamento-equipes)



### Subbots
Antes de mais nada, é necessario que [o contexto do router esteja ativado para todos os subbots abaixo](recuperando-infomacoes-contatos-subbots#contexto-do-roteador-ativado) para que as informações sejam centralizadas no bot.

#### Subbot Principal 

Este bot será responsavel por direcionar todos os usuarios para os respectivos subbots resposavel pelo ação desejada, para isso, utilizaremos a inteligencia artifial já definida no router. Veja abaixo uma apresentação desde fluxo.

// Imagem

Em resumo, como é possivel visualizar, uma vez que o usuaario apresentar qual ação ele deseja, a entrada do usuario será processada pelo provedor de IA configurado no router e por fim, o usuario será redirecionado ao subbot responsavel. É importante ressaltar que todo o fluxo de dados está rastreavel com utilização de [registro de eventos](../builder/acao-registro-evento) que futuramente pode ser utilizado no desenvolvimento de relátorios.

Você pode importar o fluxo do arquivo abaixo, [sabia como](../builder/importando-o-fluxo-de-um-bot-no-builder).
* [subbotprincipal.json]()

#### Subbot de Contratação do Serviço

Esse subbot é responsavel por:

* Pesquisar valores dos planos de internet disponiveis;
* Contratar planos de internet.

Com esse proprosito, um fluxo bem direto foi desenvolvido seguindo os seguintes passos.

1. Seleção do Plano de Interesse: Requisita para que o usuario selecione o plano de interesse.
2. Requisitando CPF: Requisita CPF do usuario para fechamendo do contrato.
3. Requisitando Email: Requisita CPF do usuario para fechamendo do contrato e envio do email com documento do contrato.
4. Finalização: Envia o email com documento do contrato.

// imagem

Você pode importar o fluxo do arquivo abaixo, [sabia como](../builder/importando-o-fluxo-de-um-bot-no-builder).
* [subbotcontratação.json]()

#### Subbot de Atendimento

Esse subbot é responsavel por:

* Cancelar planos de internet;
* Mudar o plano de internet contratado;
* Obter fatura mensal;
* Conversar com o atendente.


Para cada uma das funções deste bot, o atendente deve atender conforme protocolo empresarial. Como o contexto está ativado, todas informações do contato estão centralizas no router.


Você pode importar o fluxo do arquivo abaixo, [sabia como](../builder/importando-o-fluxo-de-um-bot-no-builder).
* [subbotatendimento.json]()