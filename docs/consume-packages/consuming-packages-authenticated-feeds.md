---
title: Utilizzo di pacchetti da feed autenticatiConsuming packages from authenticated feeds
description: Utilizzo di pacchetti da feed autenticati in tutti gli scenari client NuGetConsuming packages from authenticated feeds in all NuGet client scenarios
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231791"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>Utilizzo di pacchetti da feed autenticatiConsuming packages from authenticated feeds

Oltre ai nuget.org [feed pubblico,](https://api.nuget.org/v3/index.json)i client NuGet hanno la possibilità di interagire con feed di file e feed http privati.


Per eseguire l'autenticazione con feed http privati, i due approcci sono:

* Aggiungere le credenziali nel file [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)
* Eseguire l'autenticazione utilizzando uno dei numerosi modelli di estensibilità a seconda del client utilizzato.

## <a name="nuget-clients-authentication-extensibility"></a>Estendibilità dell'autenticazione dei client NuGetNuGet clients' authentication extensibility

Per i vari client NuGet, il provider di feed privato stesso è responsabile dell'autenticazione.
Tutti i client NuGet dispongono di metodi di estendibilità per supportare questa operazione. Si tratta di un'estensione di Visual Studio o di un plug-in in grado di comunicare con NuGet per recuperare le credenziali.

### <a name="visual-studio"></a>Visual Studio

In Visual Studio, NuGet espone un'interfaccia che i provider di feed possono implementare e fornire ai clienti. Per ulteriori informazioni, fare riferimento alla documentazione su [come creare un provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)di credenziali di Visual Studio .

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Provider di credenziali NuGet disponibili per Visual StudioAvailable NuGet credential providers for Visual Studio

È disponibile un provider di credenziali integrato in Visual Studio per supportare DevOps di Azure.There is a credential provider built into Visual Studio to support Azure DevOps.


I provider di credenziali plug-in disponibili includono:

* [Provider di credenziali MyGet per Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

Quando `nuget.exe` è necessario disporre delle credenziali per l'autenticazione con un feed, le cerca nel modo seguente:When needs credentials to authenticate with a feed, it looks for the following manner:

1. Cercare le credenziali `NuGet.config` nei file.
1. Usare i provider di credenziali del plug-in V2Use V2 plug-in credential providers
1. Usare i provider di credenziali del plug-in V1Use V1 plug-in credential providers
1. NuGet richiede quindi all'utente le credenziali nella riga di comando.

#### <a name="nugetexe-and-v2-credential-providers"></a>Provider di credenziali nuget.exe e V2

Nella `4.8` versione NuGet definito un nuovo meccanismo di plug-in di autenticazione, qui di seguito indicato come provider di credenziali V2.
Per l'installazione e la scoperta di tali provider, fare riferimento a [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="nugetexe-and-v1-credential-providers"></a>Provider di credenziali nuget.exe e V1

Nella `3.3` versione NuGet ha introdotto la prima versione dei plugin di autenticazione.
Per l'installazione e l'individuazione di tali provider fare riferimento ai provider di [credenziali nuget.exe](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)

#### <a name="available-credential-providers-for-nugetexe"></a>Provider di credenziali disponibili per nuget.exe

* Provider di credenziali V2 di Azure DevOps o provider di credenziali degli elementi di [AzureAzure](https://github.com/microsoft/artifacts-credprovider) [DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or Azure Artifacts Credential Provider

Con Visual Studio 2017 versione 15.9 e successive, il provider di credenziali DevOps di Azure viene incluso in Visual Studio.With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.
Se `nuget.exe` utilizza MSBuild da quello specifico set di strumenti di Visual Studio, il plug-in verrà individuato automaticamente.

### <a name="dotnetexe"></a>dotnet.exe

Quando `dotnet.exe` è necessario disporre delle credenziali per l'autenticazione con un feed, le cerca nel modo seguente:When needs credentials to authenticate with a feed, it looks for the following manner:

1. Cercare le credenziali `NuGet.config` nei file.
1. Usare i provider di credenziali del plug-in V2Use V2 plug-in credential providers

Per `dotnet.exe` impostazione predefinita non è interattivo, pertanto potrebbe essere necessario passare un `--interactive` flag per ottenere lo strumento da bloccare per l'autenticazione.

#### <a name="dotnetexe-and-v2-credential-providers"></a>provider di credenziali dotnet.exe e V2

Nella `2.2.100` versione dell'SDK, NuGet ha definito un meccanismo di plug-in di autenticazione che funziona in tutti i client.
Per l'installazione e la scoperta di tali provider, fare riferimento a [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-dotnetexe"></a>Provider di credenziali disponibili per dotnet.exe

* [Provider di credenziali degli elementi di AzureAzure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>FILE MSBuild.exe

Quando `MSBuild.exe` è necessario disporre delle credenziali per l'autenticazione con un feed, le cerca nel modo seguente:When needs credentials to authenticate with a feed, it looks for the following manner:

1. Cercare le credenziali `NuGet.config` nei file
1. Usare i provider di credenziali del plug-in V2Use V2 plug-in credential providers

Per `MSBuild.exe` impostazione predefinita non è interattivo, pertanto potrebbe essere necessario impostare la `/p:NuGetInteractive=true` proprietà per ottenere lo strumento da bloccare per l'autenticazione.

#### <a name="msbuildexe-and-v2-credential-providers"></a>Provider di credenziali MSBuild.exe e V2

In Visual Studio 2019 Update 9, NuGet ha definito un meccanismo di plug-in di autenticazione che funziona in tutti i client.
Per l'installazione e la scoperta di tali provider, fare riferimento a [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-msbuildexe"></a>Provider di credenziali disponibili per MSBuild.exe

* [Provider di credenziali degli elementi di AzureAzure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)

Con Visual Studio 2017 Update 9 e versioni successive, il provider di credenziali DevOps di Azure viene incluso in Visual Studio.With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio. Non sono necessari ulteriori passaggi.
