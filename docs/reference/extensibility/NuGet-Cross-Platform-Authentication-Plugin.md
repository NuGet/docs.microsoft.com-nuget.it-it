---
title: Plug-in di autenticazione multipiattaforma NuGet
description: Plug-in di autenticazione multipiattaforma NuGet per NuGet. exe, dotnet. exe, MSBuild. exe e Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: a716737343ea826d28da6de46c32ca73aef590bd
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317274"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>Plug-in di autenticazione multipiattaforma NuGet

Nella versione 4.8 + tutti i client NuGet (NuGet. exe, Visual Studio, dotnet. exe e MSBuild. exe) possono usare un plug-in di autenticazione basato sul modello di plug-in [NuGet multipiattaforma](NuGet-Cross-Platform-Plugins.md) .

## <a name="authentication-in-dotnetexe"></a>Autenticazione in dotnet. exe

Visual Studio e NuGet. exe sono interattivi per impostazione predefinita. NuGet. exe contiene un'opzione per renderla [non interattiva](../nuget-exe-CLI-Reference.md).
Inoltre, i plug-in NuGet. exe e Visual Studio richiedono l'input dell'utente.
In dotnet. exe non ci sono richieste e il valore predefinito è non interattivo.

Il meccanismo di autenticazione in dotnet. exe è il flusso del dispositivo. Quando l'operazione di ripristino o aggiunta del pacchetto viene eseguita in modo interattivo, l'operazione viene bloccata e le istruzioni per l'utente come completare le autenticazioni verranno fornite nella riga di comando.
Quando l'utente completa l'autenticazione, l'operazione continuerà.

Per rendere l'operazione interattiva, è necessario passare `--interactive`.
Attualmente solo i comandi `dotnet restore` espliciti e `dotnet add package` supportano un commute interattivo.
Non è disponibile alcun commute `dotnet build` interattivo `dotnet publish`in e.

## <a name="authentication-in-msbuild"></a>Autenticazione in MSBuild

Analogamente a dotnet. exe, MSBuild. exe è per impostazione predefinita non interattiva il meccanismo di autenticazione MSBuild. exe è il flusso del dispositivo.
Per consentire il ripristino per sospendere e attendere l'autenticazione, chiamare Restore with `msbuild -t:restore -p:NuGetInteractive="true"`.

## <a name="creating-a-cross-platform-authentication-plugin"></a>Creazione di un plug-in di autenticazione multipiattaforma

È possibile trovare un'implementazione di esempio nel plug-in [Microsoft Credential provider](https://github.com/Microsoft/artifacts-credprovider).

È molto importante che i plug-in siano conformi ai requisiti di sicurezza definiti dagli strumenti client NuGet.
La versione minima richiesta per un plug-in di autenticazione è *2.0.0*.
NuGet eseguirà l'handshake con il plug-in e la query per le attestazioni dell'operazione supportate.
Per ulteriori informazioni sui messaggi specifici, vedere i [messaggi del protocollo](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) del plug-in NuGet multipiattaforma.

NuGet imposta il livello di registrazione e fornisce informazioni sul proxy al plug-in quando applicabile.
La registrazione alla console NuGet è accettabile solo dopo che NuGet ha impostato il livello di registrazione sul plug-in.

- Comportamento di autenticazione del plug-in .NET Framework

In .NET Framework, i plug-in possono richiedere l'input di un utente, sotto forma di finestra di dialogo.

- Comportamento di autenticazione del plug-in .NET Core

In .NET Core non è possibile visualizzare una finestra di dialogo. I plug-in devono usare il flusso del dispositivo per l'autenticazione.
Il plug-in può inviare messaggi di log a NuGet con le istruzioni per l'utente.
Si noti che la registrazione è disponibile dopo che il livello di registrazione è stato impostato sul plug-in.
NuGet non accetta alcun input interattivo dalla riga di comando.

Quando il client chiama il plug-in con ottenere le credenziali di autenticazione, i plug-in devono essere conformi all'opzione di interattività e rispettare l'opzione della finestra di dialogo. 

La tabella seguente riepiloga il comportamento del plug-in per tutte le combinazioni.

| IsNonInteractive | CanShowDialog | Comportamento del plug-in |
| ---------------- | ------------- | --------------- |
| true | true | L'opzione IsNonInteractive ha la precedenza sull'opzione della finestra di dialogo. Il plug-in non è autorizzato a pop una finestra di dialogo. Questa combinazione è valida solo per .NET Framework plug-in |
| true | false | L'opzione IsNonInteractive ha la precedenza sull'opzione della finestra di dialogo. Il plug-in non può essere bloccato. Questa combinazione è valida solo per i plug-in .NET Core |
| false | true | Il plug-in dovrebbe visualizzare una finestra di dialogo. Questa combinazione è valida solo per .NET Framework plug-in |
| false | false | Il plug-in non deve visualizzare una finestra di dialogo. Il plug-in deve usare il flusso del dispositivo per l'autenticazione registrando un messaggio di istruzione tramite il logger. Questa combinazione è valida solo per i plug-in .NET Core |

Prima di scrivere un plug-in, fare riferimento alle seguenti specifiche.

- [Plug-in di download del pacchetto NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [Plug-in autenticazione NuGet Cross Plat](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
