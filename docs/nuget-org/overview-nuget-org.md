---
title: Panoramica di NuGet.org
description: Panoramica di NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427016"
---
# <a name="overview-of-nugetorg"></a>Panoramica di NuGet.org

NuGet.org è un host pubblico di pacchetti NuGet che vengono usati ogni giorno da milioni di sviluppatori .NET e .NET Core.

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>Ruolo di NuGet.org nell'ecosistema NuGet

Come host pubblico, NuGet.org gestisce il repository centrale di oltre 100.000 pacchetti univoci su [nuget.org](https://www.nuget.org). NuGet.org non è l'unico host possibile per i pacchetti. La tecnologia NuGet consente anche di ospitare i pacchetti in modo privato nel cloud (ad esempio in Azure DevOps), in una rete privata o anche direttamente nel file system locale. Se è interessati a un host diverso o a un'opzione di hosting diversa, vedere [Hosting dei feed NuGet](../hosting-packages/overview.md).

Come qualsiasi host di pacchetti NuGet, NuGet.org fa da punto di connessione tra gli *autori* e i *consumer* dei pacchetti. Gli autori compilano utili pacchetti NuGet e li pubblicano. I consumer cercano quindi i pacchetti utili e compatibili negli host accessibili, scaricandoli e includendoli nei loro progetti. Una volta installate in un progetto, le API dei pacchetti sono disponibili per il resto del codice del progetto.

![Relazione tra autori, host e consumer dei pacchetti](media/nuget-roles.png)

## <a name="accounts"></a>Account

Per pubblicare pacchetti in NuGet.org, iniziare creando un [account individuale (account utente)](individual-accounts.md). Questo account diventa l'identità dell'utente in NuGet.org.

NuGet.org consente anche di creare un [account aziendale](organizations-on-nuget-org.md). Un account aziendale ha uno o più account individuali come membri. I membri possono gestire un set di pacchetti mantenendo un'unica identità per la proprietà. L'account personale consente a un utente di essere membro di un numero qualsiasi di organizzazioni.

Un pacchetto può appartenere a un account aziendale come a un account individuale. I consumer di pacchetti non vedono alcuna differenza tra un account individuale e l'account aziendale: entrambi vengono visualizzati come `owners` (proprietari) del pacchetto.

## <a name="api-keys"></a>Chiavi API

Dopo aver creato un pacchetto NuGet (un file con estensione *nupkg*) da pubblicare, pubblicarlo in NuGet.org usando l'interfaccia della riga di comando nuget.exe o dotnet.exe insieme a una [chiave API](scoped-api-keys.md) acquisita da NuGet.org.

Quando si [pubblica un pacchetto](../create-packages/creating-a-package.md), si include il valore della chiave API nel comando dell'interfaccia della riga di comando.

## <a name="id-prefixes"></a>Prefissi ID

Quando si esegue la pubblicazione dei pacchetti, è possibile riservare e proteggere la propria identità [riservando prefissi ID](id-prefix-reservation.md). Quando si installa un pacchetto, ai consumer di pacchetti vengono fornite informazioni aggiuntive indicanti che le proprietà di identificazione del pacchetto in uso non sono fuorvianti.

## <a name="api-endpoint-for-nugetorg"></a>Endpoint API per NuGet.org

Per usare NuGet.org come repository di pacchetti con i client NuGet, è consigliabile usare l'endpoint API V3 seguente: 

`https://api.nuget.org/v3/index.json`

I client meno recenti possono comunque usare il protocollo V2 per raggiungere NuGet.org. Si noti tuttavia che i client NuGet 3.0 o versione successiva avranno un servizio più lento e meno affidabile se usano il protocollo V2:

`https://www.nuget.org/api/v2` (**il protocollo V2 è deprecato.** )
