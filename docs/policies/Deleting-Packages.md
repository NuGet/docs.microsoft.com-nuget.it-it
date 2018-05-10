---
title: Eliminazione di pacchetti NuGet da nuget.org
description: Criteri per la rimozione di pacchetti dall'elenco di nuget.org; l'eliminazione permanente non è supportata, salvo quando i pacchetti violano altri criteri.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: bea4f1589f184d38da27e5d82c3ce17a183fbdd1
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="deleting-packages"></a>Eliminazione di pacchetti

nuget.org non supporta l'eliminazione permanente dei pacchetti. Questa operazione comporterebbe l'interruzione di tutti i progetti che dipendono dalla disponibilità del pacchetto eliminato, in particolare con i flussi di lavoro di compilazione che implicano il ripristino del pacchetto.

nuget.org supporta invece la *rimozione dall'elenco* di un pacchetto, che può essere eseguita nella pagina di gestione del pacchetto nel sito Web. I pacchetti rimossi dall'elenco non vengono visualizzati su nuget.org o nell'interfaccia utente di Visual Studio, né compaiono all'interno dei risultati della ricerca. I pacchetti rimossi dall'elenco, tuttavia, possono essere ancora scaricati e installati usando il numero di versione esatto, che supporta il ripristino del pacchetto. Inoltre, i pacchetti rimossi dall'elenco potrebbero essere ancora individuati negli scenari specifici seguenti:

- Ripristino del pacchetto usando versioni mobili (ad esempio, `1.0.0-*`), se il pacchetto più recente disponibile corrispondente alle limitazioni della versione o della dipendenza è un pacchetto rimosso dall'elenco.
- Replica dei pacchetti tramite il catalogo (dal momento che il catalogo contiene anche pacchetti rimossi dall'elenco).

## <a name="exceptions"></a>Eccezioni

In situazioni eccezionali, quali violazione del copyright e contenuto potenzialmente dannoso, i pacchetti possono essere eliminati manualmente dal team di NuGet. Inviare una richiesta di supporto tramite la [raccolta NuGet](http://www.nuget.org) per avviare il processo.

## <a name="prohibited-use"></a>Uso non consentito

I pacchetti che soddisfano uno dei criteri seguenti non sono consentiti nella raccolta NuGet pubblica e verranno immediatamente rimossi senza discussione. I proprietari dei pacchetti verranno tuttavia informati della rimozione.

- Contengono malware, adware o qualsiasi tipo di spyware.
- Sono progettati per danneggiare la workstation dello sviluppatore o l'organizzazione.
- Violano diritti di copyright o licenze.
- Contengono contenuto illecito.
- Vengono usati per appropriarsi degli identificatori dei pacchetti, inclusi i pacchetti che hanno un contenuto produttivo nullo. I pacchetti devono contenere codice oppure i proprietari devono concedere l'identificatore a un utente che abbia effettivamente un prodotto da fornire.
- Tentano di fare in modo che la raccolta esegua operazioni per cui non è stata esplicitamente progettata.

Se si trova un pacchetto che è palesemente in violazione di una di queste condizioni, fare clic sul collegamento **Report Abuse** (Segnala abusi) nella pagina dei dettagli del pacchetto e inviare un report.

Si noti che il team di NuGet e .NET Foundation si riservano il diritto di modificare questi criteri in qualsiasi momento.
