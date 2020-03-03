---
title: Utilizzo di pacchetti da feed autenticati
description: Utilizzo di pacchetti da feed autenticati in tutti gli scenari client NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231791"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>Utilizzo di pacchetti da feed autenticati

Oltre al [feed pubblico](https://api.nuget.org/v3/index.json)di NuGet.org, i client NuGet sono in grado di interagire con i feed di file e i feed http privati.


Per eseguire l'autenticazione con feed http privati, i 2 approcci sono:

* Aggiungere le credenziali in [NuGet. config](../reference/nuget-config-file.md#packagesourcecredentials)
* Eseguire l'autenticazione usando uno dei numerosi modelli di estendibilità a seconda del client usato.

## <a name="nuget-clients-authentication-extensibility"></a>Estendibilità dell'autenticazione dei client NuGet

Per i vari client NuGet, il provider di feed privato è responsabile dell'autenticazione.
Tutti i client NuGet hanno metodi di estendibilità per supportare questa operazione. Si tratta di un'estensione di Visual Studio o un plug-in in grado di comunicare con NuGet per recuperare le credenziali.

### <a name="visual-studio"></a>Visual Studio

In Visual Studio, NuGet espone un'interfaccia che i provider di feed possono implementare e fornire ai propri clienti. Per altri dettagli, vedere la documentazione su [come creare un provider di credenziali di Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Provider di credenziali NuGet disponibili per Visual Studio

Per supportare Azure DevOps è disponibile un provider di credenziali incorporato in Visual Studio.


I provider di credenziali plug-in disponibili includono:

* [Provider di credenziali MyGet per Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

Quando `nuget.exe` necessita di credenziali per l'autenticazione con un feed, la ricerca viene eseguita nel modo seguente:

1. Cercare le credenziali nei file di `NuGet.config`.
1. Usare i provider di credenziali plug-in V2
1. Usare i provider di credenziali plug-in V1
1. NuGet chiede quindi all'utente le credenziali nella riga di comando.

#### <a name="nugetexe-and-v2-credential-providers"></a>provider di credenziali NuGet. exe e V2

Nella versione `4.8` NuGet definisce un nuovo meccanismo di plug-in di autenticazione, in seguito denominato provider di credenziali V2.
Per l'installazione e l'individuazione di tali provider, vedere [plug-in NuGet multipiattaforma](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="nugetexe-and-v1-credential-providers"></a>provider di credenziali NuGet. exe e V1

Nella versione `3.3` in NuGet è stata introdotta la prima versione di plug-in di autenticazione.
Per l'installazione e l'individuazione di questi provider, vedere [provider di credenziali NuGet. exe](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)

#### <a name="available-credential-providers-for-nugetexe"></a>Provider di credenziali disponibili per NuGet. exe

* Provider di [credenziali di Azure DevOps V2](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) o [provider di credenziali Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

Con Visual Studio 2017 versione 15,9 e successive, il provider di credenziali di Azure DevOps è incluso in Visual Studio.
Se `nuget.exe` USA MSBuild da quel set di strumenti di Visual Studio specifico, il plug-in verrà individuato automaticamente.

### <a name="dotnetexe"></a>dotnet.exe

Quando `dotnet.exe` necessita di credenziali per l'autenticazione con un feed, la ricerca viene eseguita nel modo seguente:

1. Cercare le credenziali nei file di `NuGet.config`.
1. Usare i provider di credenziali plug-in V2

Per impostazione predefinita `dotnet.exe` non è interattivo, quindi potrebbe essere necessario passare un flag `--interactive` per ottenere lo strumento da bloccare per l'autenticazione.

#### <a name="dotnetexe-and-v2-credential-providers"></a>provider di credenziali dotnet. exe e V2

Nella versione `2.2.100` dell'SDK, NuGet definisce un meccanismo di plug-in di autenticazione che funziona in tutti i client.
Per l'installazione e l'individuazione di tali provider, vedere [plug-in NuGet multipiattaforma](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-dotnetexe"></a>Provider di credenziali disponibili per dotnet. exe

* [Provider di credenziali Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild. exe

Quando `MSBuild.exe` necessita di credenziali per l'autenticazione con un feed, la ricerca viene eseguita nel modo seguente:

1. Cerca le credenziali nei file di `NuGet.config`
1. Usare i provider di credenziali plug-in V2

Per impostazione predefinita `MSBuild.exe` non è interattivo, quindi potrebbe essere necessario impostare la proprietà `/p:NuGetInteractive=true` per fare in modo che lo strumento si blocchi per l'autenticazione.

#### <a name="msbuildexe-and-v2-credential-providers"></a>Provider di credenziali MSBuild. exe e V2

In Visual Studio 2019 Update 9, NuGet definisce un meccanismo di plug-in di autenticazione che funziona in tutti i client.
Per l'installazione e l'individuazione di tali provider, vedere [plug-in NuGet multipiattaforma](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-msbuildexe"></a>Provider di credenziali disponibili per MSBuild. exe

* [Provider di credenziali Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)

Con Visual Studio 2017 Update 9 e versioni successive, il provider di credenziali di Azure DevOps è incluso in Visual Studio. Non sono necessari passaggi aggiuntivi.
