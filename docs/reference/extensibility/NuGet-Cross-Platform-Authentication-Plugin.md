---
title: NuGet cross platform plug-in di autenticazione
description: NuGet cross platform autenticazione i plug-in per NuGet.exe, dotnet.exe, msbuild.exe e Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: b76fab1028ec9a4172d2390083fbf9adb4290a6c
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453507"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet cross platform plug-in di autenticazione

Nella versione 4.8, NuGet tutti i client (NuGet.exe, Visual Studio, dotnet.exe e MSBuild.exe) possono usare un plug-in di autenticazione costruita basandosi sul [NuGet cross-platform plugins](NuGet-Cross-Platform-Plugins.md) modello.

## <a name="authentication-in-dotnetexe"></a>Autenticazione in dotnet.exe

Visual Studio e NuGet.exe sono per impostazione predefinita interattiva. NuGet.exe contiene un'opzione per renderla [non interattivo](../../tools/nuget-exe-CLI-Reference.md).
I plug-in Visual Studio e NuGet.exe inoltre richiesto l'input dell'utente.
Dotnet.exe non include alcuna richiesta di conferma e il valore predefinito è non interattivo.

Il meccanismo di autenticazione in dotnet.exe è flusso del dispositivo. Quando il ripristino o aggiungere l'operazione di pacchetti viene eseguita in modo interattivo, l'operazione si blocca e istruzioni per l'utente come a completa le autenticazioni verranno fornite nella riga di comando.
L'operazione continuerà quando l'utente ha completato l'autenticazione.

Per effettuare l'operazione interattiva, uno deve passare `--interactive`.
Attualmente solo l'impostazione esplicita `dotnet restore` e `dotnet add package` comandi supportano un'opzione interattiva.
Non include alcun commutatore interattivi `dotnet build` e `dotnet publish`.

## <a name="authentication-in-msbuild"></a>Autenticazione in MSBuild

Analogamente a dotnet.exe, MSBuild.exe è per impostazione predefinita non che è il meccanismo di autenticazione MSBuild.exe interattiva flusso del dispositivo.
Per consentire il ripristino sospendere e in attesa per l'autenticazione, chiamare il ripristino con `msbuild -t:restore -p:NuGetInteractive="true"`.

## <a name="creating-a-cross-platform-authentication-plugin"></a>Creazione di un plug-in di autenticazione cross-platform

Un'implementazione di esempio sono disponibili nel [plug-in Provider di credenziali Microsoft](https://github.com/Microsoft/artifacts-credprovider).

È molto importante che i plug-in sia conforme ai requisiti di sicurezza stabiliti dagli strumenti client NuGet.
È necessario almeno versione per un plug-in sia un plug-in di autenticazione *2.0.0*.
NuGet esegue l'handshake con il plug-in e query per le attestazioni di operazione supportata.
Fare riferimento a NuGet cross-platform plugin [i messaggi di protocollo](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) per altri dettagli sui messaggi specifici.

NuGet verrà impostato il livello di registrazione e fornire informazioni sul proxy per il plug-in quando applicabile.
La registrazione di NuGet console è accettabile solo dopo che NuGet ha impostato il livello di registrazione per il plug-in.

- Comportamento di autenticazione plug-in .NET framework

In .NET Framework, i plug-in sono consentite per richiedere un input dell'utente, sotto forma di una finestra di dialogo.

- Comportamento di autenticazione plug-in .NET core

In .NET Core, non è possibile visualizzare una finestra di dialogo. I plug-in deve usare flow dispositivo per eseguire l'autenticazione.
Il plug-in è possibile inviare i messaggi di log a NuGet con le istruzioni per l'utente.
Si noti che la registrazione sia disponibile dopo aver impostato il livello di registrazione per il plug-in.
NuGet non avrà alcun input interattivo dalla riga di comando.

Quando il client chiama il plug-in con le credenziali di autenticazione un'introduzione, i plug-in necessario sono conformi al commutatore interattività e rispetta l'opzione della finestra di dialogo. 

La tabella seguente riepiloga il comportamento il plug-in per tutte le combinazioni.

| IsNonInteractive | CanShowDialog | Comportamento di plug-in |
| ---------------- | ------------- | --------------- |
| true | true | Il commutatore IsNonInteractive ha la precedenza su commutatore la finestra di dialogo. Il plug-in non è consentito per aprire una finestra di dialogo. Questa combinazione è valida solo per i plug-in .NET Framework |
| true | False | Il commutatore IsNonInteractive ha la precedenza su commutatore la finestra di dialogo. Il plug-in non è consentito per bloccare. Questa combinazione è valida solo per i plug-in .NET Core |
| False | true | Il plug-in deve visualizzare una finestra di dialogo. Questa combinazione è valida solo per i plug-in .NET Framework |
| False | False | Il plug-in deve/can non è visualizzata una finestra di dialogo. Il plug-in deve usare flow dispositivo per l'autenticazione mediante la registrazione di un messaggio di istruzione tramite il logger. Questa combinazione è valida solo per i plug-in .NET Core |

Prima di scrivere un plug-in, vedere le specifiche seguenti.

- [Plug-in di Download del pacchetto NuGet](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet cross-plat plug-in di autenticazione](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
