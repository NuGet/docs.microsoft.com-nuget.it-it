---
title: Utilizzo di pacchetti da feed autenticati
description: Utilizzo di pacchetti da feed autenticati in tutti gli scenari client NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: e76fefaf4d3c86aa15cf279090c0adb8ed779aab
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901512"
---
# <a name="consuming-packages-from-authenticated-feeds"></a>Utilizzo di pacchetti da feed autenticati

Oltre al feed [nuget.org,](https://api.nuget.org/v3/index.json)i client NuGet hanno la possibilità di interagire con feed di file e feed HTTP privati.


Per eseguire l'autenticazione con feed HTTP privati, i due approcci sono:

* Aggiungere le credenziali nel [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)
* Eseguire l'autenticazione usando uno dei numerosi modelli di estendibilità a seconda del client usato.

## <a name="nuget-clients-authentication-extensibility"></a>Estendibilità dell'autenticazione dei client NuGet

Per i vari client NuGet, il provider di feed privato è responsabile dell'autenticazione.
Tutti i client NuGet hanno metodi di estendibilità per supportare questa operazione. Si tratta di un'estensione Visual Studio o un plug-in in grado di comunicare con NuGet per recuperare le credenziali.

### <a name="visual-studio"></a>Visual Studio

In Visual Studio NuGet espone un'interfaccia che i provider di feed possono implementare e fornire ai clienti. Per altre informazioni, vedere la documentazione su come creare un provider di [Visual Studio credenziali.](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)

#### <a name="available-nuget-credential-providers-for-visual-studio"></a>Provider di credenziali NuGet disponibili per Visual Studio

È disponibile un provider di credenziali incorporato in Visual Studio per supportare Azure DevOps.


I provider di credenziali plug-in disponibili includono:

* [MyGet Provider di credenziali per Visual Studio](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a>nuget.exe

Quando `nuget.exe` sono necessarie le credenziali per l'autenticazione con un feed, queste vengono cercate nel modo seguente:

1. Cercare le credenziali nei `NuGet.config` file.
1. Usare i provider di credenziali del plug-in V2
1. Usare i provider di credenziali del plug-in V1
1. NuGet richiede quindi all'utente le credenziali nella riga di comando.

#### <a name="nugetexe-and-v2-credential-providers"></a>nuget.exe e provider di credenziali V2

Nella versione NuGet ha definito un nuovo meccanismo del plug-in di autenticazione, denominato successivamente provider di credenziali `4.8` V2.
Per l'installazione e l'individuazione di tali provider, vedere [Plug-in multipiattaforma NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="nugetexe-and-v1-credential-providers"></a>nuget.exe e provider di credenziali V1

Nella versione `3.3` NuGet ha introdotto la prima versione dei plug-in di autenticazione.
Per l'installazione e l'individuazione di tali provider, fare [ riferimentonuget.exe provider di credenziali](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)

#### <a name="available-credential-providers-for-nugetexe"></a>Provider di credenziali disponibili per nuget.exe

* [Azure DevOps provider di credenziali V2](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) o [Azure Artifacts Provider di credenziali](https://github.com/microsoft/artifacts-credprovider)

Con Visual Studio 2017 versione 15.9 e successive, il provider Azure DevOps credenziali è in bundle in Visual Studio.
Se `nuget.exe` usa MSBuild da quel set Visual Studio strumenti, il plug-in verrà individuato automaticamente.

### <a name="dotnetexe"></a>dotnet.exe

Quando `dotnet.exe` sono necessarie credenziali per l'autenticazione con un feed, le cerca nel modo seguente:

1. Cercare le credenziali nei `NuGet.config` file.
1. Usare i provider di credenziali del plug-in V2

Per impostazione predefinita, non è interattiva, quindi potrebbe essere necessario passare un flag per ottenere `dotnet.exe` lo strumento da bloccare per `--interactive` l'autenticazione.

#### <a name="dotnetexe-and-v2-credential-providers"></a>dotnet.exe e provider di credenziali V2

Nella versione `2.2.100` dell'SDK NuGet ha definito un meccanismo del plug-in di autenticazione che funziona in tutti i client.
Per l'installazione e l'individuazione di tali provider, vedere [Plug-in multipiattaforma NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).

#### <a name="available-credential-providers-for-dotnetexe"></a>Provider di credenziali disponibili per dotnet.exe

* [Azure Artifacts Provider di credenziali](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a>MSBuild.exe

Quando `MSBuild.exe` sono necessarie le credenziali per l'autenticazione con un feed, queste vengono cercate nel modo seguente:

1. Cercare le credenziali nei `NuGet.config` file
1. Usare i provider di credenziali del plug-in V2

Per impostazione predefinita, non è interattiva, quindi potrebbe essere necessario impostare la proprietà per ottenere `MSBuild.exe` lo strumento da bloccare per `/p:NuGetInteractive=true` l'autenticazione.

#### <a name="msbuildexe-and-v2-credential-providers"></a>provider di credenziali MSBuild.exe e V2

In Visual Studio 2019 Update 9, NuGet ha definito un meccanismo del plug-in di autenticazione che funziona in tutti i client.
Per l'installazione e l'individuazione di tali provider, vedere [Plug-in multipiattaforma NuGet.](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)

#### <a name="available-credential-providers-for-msbuildexe"></a>Provider di credenziali disponibili per MSBuild.exe

* [Azure Artifacts Provider di credenziali](https://github.com/microsoft/artifacts-credprovider)

Con Visual Studio 2017 Update 9 e versioni successive, il provider Azure DevOps credenziali è in bundle in Visual Studio. Non sono necessari altri passaggi.
