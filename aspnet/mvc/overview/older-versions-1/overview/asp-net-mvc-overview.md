---
uid: mvc/overview/older-versions-1/overview/asp-net-mvc-overview
title: visão geral ASP.NET MVC | Microsoft Docs
author: rick-anderson
description: Conheça as diferenças entre ASP.NET aplicativo MVC e aplicativos de Formulários da ASP.NET Web. Saiba como decidir quando construir um aplicativo MVC ASP.NET.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2dcb44a4-5cbf-4d62-b363-718104082d86
msc.legacyurl: /mvc/overview/older-versions-1/overview/asp-net-mvc-overview
msc.type: authoredcontent
ms.openlocfilehash: 84810f168faa2e79a65ff3fb75e3654828bdb58f
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81541007"
---
# <a name="aspnet-mvc-overview"></a>Visão geral do ASP.NET MVC

pela [Microsoft](https://github.com/microsoft)

> Conheça as diferenças entre ASP.NET aplicativo MVC e aplicativos de Formulários da ASP.NET Web. Saiba como decidir quando construir um aplicativo MVC ASP.NET.

O padrão arquitetônico Model-View-Controller (MVC) separa uma aplicação em três componentes principais: o modelo, a visualização e o controlador. A estrutura mvc ASP.NET fornece uma alternativa ao padrão ASP.NET Formulários web para criar aplicativos Web baseados em MVC. A estrutura ASP.NET MVC é uma estrutura de apresentação leve e altamente testável que (à semelhança dos aplicativos baseados em Web Forms) é integrada aos recursos ASP.NET existentes, como páginas mestras e autenticação baseada em associação. A estrutura MVC é definida no **namespace System.Web.Mvc** e é uma parte fundamental e suportada do **namespace system.Web.**   
  
O MVC é um padrão de design padrão que muitos desenvolvedores conhecem. Alguns tipos de aplicativos Web irão se beneficiar da estrutura MVC. Outros vão continuar usando o padrão de aplicativo ASP.NET tradicional que é baseado em Web Forms e postbacks. Outros tipos de aplicativos Web irão combinar as duas abordagens; uma abordagem não exclui a outra.   
  
A estrutura MVC inclui os seguintes componentes:

[![Invocando uma ação do controlador que espera um valor de parâmetro](asp-net-mvc-overview/_static/image1.jpg)](asp-net-mvc-overview/_static/image1.png)

**Figura 01**: Invocar uma ação do controlador que espera um valor de parâmetro[(Clique para exibir imagem em tamanho real)](asp-net-mvc-overview/_static/image2.png)

- **Modelos**. Os objetos de modelo são as partes do aplicativo que implementam a lógica para o domínio de dados do aplicativo. Muitas vezes, os objetos de modelo recuperam e armazenam o estado do modelo em um banco de dados. Por exemplo, um objeto Produto pode recuperar informações de um banco de dados, operá-lo e, em seguida, gravar informações atualizadas de volta para uma tabela Produtos no SQL Server.

Em aplicativos pequenos, o modelo, muitas vezes, é uma separação conceitual em vez de física. Por exemplo, se o aplicativo ler apenas um conjunto de dados e o enviar para a exibição, o aplicativo não terá uma camada de modelo físico e classes associadas. Nesse caso, o conjunto de dados assume o papel de um objeto modelo.

- **Pontos de vista**. As exibições são os componentes que exibem a interface do usuário do aplicativo (UI). Normalmente, esta IU é criada a partir dos dados do modelo. Um exemplo seria uma exibição de edição de uma tabela Produtos que exibe caixas de texto, listas de saque e caixas de seleção com base no estado atual de um objeto Produtos.

- **Controladores**. Os controladores são os componentes que lidam com a interação do usuário, trabalham com o modelo e, finalmente, selecionam uma exibição de renderização que mostra essa IU. Em um aplicativo MVC, a exibição mostra apenas informações; o controlador manipula e responde à entrada e à interação do usuário. Por exemplo, o controlador lida com valores de seqüência de consultas e passa esses valores para o modelo, que por sua vez consulta o banco de dados usando os valores.

O padrão MVC ajuda a criar aplicativos que separam os diferentes aspectos do aplicativo (lógica de entrada, lógica de negócio e lógica da IU), enquanto fornece um acoplamento flexível entre esses elementos. O padrão especifica onde cada tipo de lógica deve ficar localizado no aplicativo. A lógica da interface do usuário pertence à exibição. A lógica de entrada pertence ao controlador. A lógica de negócios pertence ao modelo. Essa separação ajuda a administrar a complexidade quando você cria um aplicativo, porque ela permite que você se concentre em um aspecto da implementação por vez. Por exemplo, você pode se concentrar na exibição sem depender da lógica de negócios.   
  
Além de administrar a complexidade, o padrão MVC torna o teste de aplicativos mais fácil do que o teste de um aplicativo Web ASP.NET baseado em Web Forms. Por exemplo, num aplicativo Web ASP.NET baseado em Web Forms, uma única classe é usada para exibir a saída e para responder à entrada do usuário. Escrever testes automatizados para aplicativos ASP.NET baseados em Web Forms pode ser complexo, pois para testar uma página individual, você deve criar uma instância da classe da página, de todos os seus controles filhos e das classes dependentes adicionais no aplicativo. Uma vez que são criadas instâncias de tantas classes para executar a página, pode ser complicado escrever testes que se foquem exclusivamente em partes individuais do aplicativo. Os testes para aplicativos ASP.NET baseados em Web Forms podem, por isto, ser mais difíceis de implementar do que testes em um aplicativo MVC. Além disso, os testes em aplicativos ASP.NET baseados em Web Forms exigem um servidor Web. A estrutura MVC separa os componentes e usa interfaces intensamente, o que torna possível testar componentes individuais isoladamente do resto da estrutura.   
  
O acoplamento flexível entre os três componentes principais de um aplicativo MVC também promove o desenvolvimento paralelo. Por exemplo, um desenvolvedor pode trabalhar na visão, um segundo desenvolvedor pode trabalhar na lógica do controlador, e um terceiro desenvolvedor pode se concentrar na lógica de negócios no modelo.

## <a name="deciding-when-to-create-an-mvc-application"></a>Decidindo quando criar um aplicativo MVC

Você deve considerar cuidadosamente se deve implementar um aplicativo Web usando a estrutura ASP.NET MVC ou o modelo de Web Forms do ASP.NET. A estrutura MVC não substitui o modelo de Web Forms; você pode usar ambas as estruturas para aplicativos Web. (Se você tem aplicativos existentes baseados em Web Forms, eles continuarão a funcionar exatamente como funcionavam antes).   
  
Antes de você decidir usar a estrutura MVC ou o modelo de Web Forms para um determinado site, pondere as vantagens de cada abordagem.

### <a name="advantages-of-an-mvc-based-web-application"></a>Vantagens de um aplicativo Web baseado em MVC

A estrutura ASP.NET MVC oferece as seguintes vantagens:

- Ela torna mais fácil gerenciar a complexidade ao dividir o aplicativo em modelo, exibição e controlador.
- Ela não utiliza o estado de exibição nem formulários baseados no servidor. Isto torna a estrutura MVC ideal para desenvolvedores que desejam controle completo sobre o comportamento do aplicativo.
- Ela usa um padrão Front Controller que processa as solicitações do aplicativo Web através de um único controlador. Isto permite desenvolver um aplicativo que suporta uma poderosa infraestrutura de roteamento. Para obter mais informações, consulte [O Controlador frontal](https://go.microsoft.com/fwlink/?LinkId=106357 "Controlador frontal") no site do MSDN.
- Ela fornece um melhor suporte para desenvolvimento controlado por testes (TDD – test-driven development).
- Funciona bem para aplicações web que são suportadas por grandes equipes de desenvolvedores e web designers que precisam de um alto grau de controle sobre o comportamento do aplicativo.

### <a name="advantages-of-a-web-forms-based-web-application"></a>Vantagens de um aplicativo Web baseado em Web Forms

A estrutura baseada em Web Forms oferece as seguintes vantagens:

- Ela suporta um modelo de evento que preserva o estado sobre HTTP, o que beneficia o desenvolvimento de aplicativos Web de linha de negócios. O aplicativo baseado em Web Forms fornece dezenas de eventos que são suportados em centenas de controles de servidor.
- Ela usa um padrão Page Controller que adiciona funcionalidade em páginas individuais. Para obter mais informações, consulte [O Controlador de Página](https://go.microsoft.com/fwlink/?LinkId=106359 "Controlador de página") no site do MSDN.
- Ele usa formulários de exibição de estado ou servidor, o que pode facilitar o gerenciamento de informações de estado.
- Ela funciona bem com pequenas equipes de desenvolvedores e Web designers que desejem tirar proveito do grande número de componentes disponíveis para um rápido desenvolvimento do aplicativo.
- Em geral, é menos complexo para o desenvolvimento de aplicativos, porque os componentes (a classe **Page,** controles e assim por diante) são fortemente integrados e geralmente requerem menos código do que o modelo MVC.

## <a name="features-of-the-aspnet-mvc-framework"></a>Recursos da estrutura ASP.NET MVC

A estrutura ASP.NET MVC fornece os seguintes recursos:

- Separação de tarefas de aplicativos (lógica de entrada, lógica de negócios e lógica de interface do usuário), testability e tDD (test-driven development, desenvolvimento orientado por teste) por padrão. Todos os contratos núcleo na estrutura MVC são baseados na interface e podem ser testados usando objetos fictícios, que são objetos simulados que imitam o comportamento dos objetos reais no aplicativo. Você pode testar a unidade do aplicativo sem ter que executar os controladores em um processo ASP.NET, o que acelera e flexibiliza o teste da unidade. Você pode usar qualquer estrutura de teste da unidade que seja compatível com o .NET Framework.
- Uma estrutura extensível e conectável. Os componentes da estrutura ASP.NET MVC são desenvolvidos para serem facilmente substituídos ou personalizados. É possível conectar o seu próprio mecanismo de exibição, política de roteamento de URL, serialização de parâmetro ação-método e outros componentes. A estrutura ASP.NET MVC também suporta o uso dos modelos de contêiner de DI (Dependency Injection – Injeção de Dependência) e IOC (Inversion of Control – Inversão de Controle). O DI permite que você injete objetos em uma classe, em vez de depender da classe para criar o objeto em si. A IOC especifica que se um objeto requer outro objeto, os primeiros objetos devem obter o segundo objeto de uma fonte exterior como um arquivo de configuração. Isto facilita os testes.
- Um poderoso componente de mapeamento de URL que permite construir aplicativos que tenham URLs compreensíveis e pesquisáveis. As URLs não precisam incluir extensões de nome de arquivo e são desenvolvidas para suportar padrões de denominação de URLs que funcionam bem para SEO (Search Engine Optimization – Otimização do Mecanismo de Pesquisa) e endereçamento REST (Representational State Transfer – Transferência de Estado Representacional).
- Suporte ao uso de marcação em arquivos de marcação de páginas ASP.NET (arquivos .aspx), de controle de usuário (arquivos .ascx) e de página mestra (arquivos .master) existentes como modelos de exibição. Você pode usar os recursos de ASP.NET existentes com a estrutura ASP.NET MVC,&lt;como&gt;páginas-mestre aninhadas, expressões em linha (%= %), controles declarativos de servidor, modelos, vinculação de dados, localização e assim por diante.
- Suporte para recursos ASP.NET existentes. A estrutura ASP.NET MVC permite a utilização de recursos como autenticação de formulários e autenticação do Windows, autorização de URLs, associação e funções, caching de saída e dados, gerenciamento de estado de sessão e perfil, monitoramento de integridade, sistema de configuração e arquitetura de provedor.
