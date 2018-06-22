---
title: Richieste di dati degli utenti
description: Criteri per le richieste di esportazione ed eliminazione dei dati degli utenti
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: 595a47da59c9b2672a10fc0f19e528c36a790134
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2018
ms.locfileid: "33086204"
---
# <a name="user-data-requests"></a>Richieste di dati degli utenti

Gli utenti di nuget.org possono inviare le richieste di eliminazione ed esportazione delle informazioni tramite [nuget.org](https://www.nuget.org). Entrambi i tipi vengono inviati sotto forma di richieste di supporto e vengono eseguiti dagli amministratori di nuget.org entro 30 giorni.

I dati utente seguenti sono accessibili direttamente tramite nuget.org:

* Dati relativi all'account, ad esempio indirizzo di posta elettronica, account di accesso, immagine del profilo e impostazioni di notifica tramite posta elettronica
* Chiavi API di proprietà
* Elenco dei pacchetti di proprietà

Questi dati non sono inclusi nei dati esportati tramite la richiesta di supporto.

## <a name="identifying-customer-data"></a>Identificazione dei dati dei clienti

I dati dei clienti possono essere identificati come nomi di account utente di nuget.org.

## <a name="deleting-customer-data"></a>Eliminazione dei dati dei clienti

Per richiedere l'eliminazione dei dati degli utenti da nuget.org:

1. L'utente deve accedere a [nuget.org](https://www.nuget.org)
1. L'utente deve inviare una richiesta di eliminazione del proprio account [nuget.org/account/delete](https://www.nuget.org/account/delete)

Gli utenti che sono gli unici proprietari dei pacchetti sono invitati a trovare nuovi proprietari prima di richiedere l'eliminazione del proprio account. Se non è possibile trasferire la proprietà del pacchetto, il pacchetto NuGet viene escluso dall'elenco e, di conseguenza, non è più disponibile nelle query di ricerca in Visual Studio o nel sito Web nuget.org. Prima di eliminare l'account, gli amministratori di nuget.org collaborano con l'utente per trovare nuovi proprietari per i pacchetti di loro proprietà.

L'azione di eliminazione dell'account viene completata dall'amministratore di nuget.org entro 30 giorni dalla data della richiesta.

In seguito all'eliminazione dell'account, tutti i dati dell'utente vengono rimossi dal sistema nuget.org e vengono eseguite le azioni seguenti:

* L'account eliminato diventa non registrato con nuget.org
* Tutte le chiavi API di proprietà vengono eliminate
* Tutti gli spazi dei nomi riservati vengono rilasciati
* Tutte le proprietà dei pacchetti vengono rimosse

I pacchetti di proprietà *non* vengono eliminati. Anche se rimossi dall'elenco dei risultati della ricerca, rimangono disponibili tramite il ripristino del pacchetto per i progetti che dipendono da essi.

## <a name="exporting-customer-data"></a>Esportazione dei dati dei clienti

Dopo l'accesso a nuget.org, un utente può inviare una richiesta di esportazione tramite [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)

I dati esportati vengono resi disponibili per 48 ore all'utente per il download tramite un BLOB di Azure. Dopo 48 ore, l'accesso scade e l'utente deve inviare una nuova richiesta di esportazione in base alle esigenze.

I dati esportati includono:

* Le richieste di supporto dell'utente
* Le azioni dell'utente (pubblicazione del pacchetto, creazione di account) come resi persistenti nei log di controllo
* Le informazioni sull'utente come rese persistenti nei log di IIS
