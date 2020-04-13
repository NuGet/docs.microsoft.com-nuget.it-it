---
title: Eliminazione di pacchetti NuGet da nuget.org
description: Criteri per la rimozione di pacchetti dall'elenco di nuget.org; l'eliminazione permanente non è supportata, salvo quando i pacchetti violano altri criteri.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 3abe809d76e75801c2f936aba129d27ba7b64913
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "80581273"
---
# <a name="deleting-packages"></a>Eliminazione di pacchetti

nuget.org non supporta l'eliminazione permanente dei pacchetti. Questa operazione comporterebbe l'interruzione di tutti i progetti che dipendono dalla disponibilità del pacchetto eliminato, in particolare con i flussi di lavoro di compilazione che implicano il ripristino del pacchetto.

nuget.org supporta [l'annullamento dell'elenco](#unlisting-a-package)di un pacchetto , che può essere eseguito nella pagina di gestione del pacchetto sul sito Web. I pacchetti rimossi dall'elenco non vengono visualizzati su nuget.org o nell'interfaccia utente di Visual Studio, né compaiono all'interno dei risultati della ricerca. I pacchetti rimossi dall'elenco, tuttavia, possono essere ancora scaricati e installati usando il numero di versione esatto, che supporta il ripristino del pacchetto. Inoltre, i pacchetti rimossi dall'elenco potrebbero essere ancora individuati negli scenari specifici seguenti:

- Ripristino del pacchetto usando versioni mobili (ad esempio, `1.0.0-*`), se il pacchetto più recente disponibile corrispondente alle limitazioni della versione o della dipendenza è un pacchetto rimosso dall'elenco.
- Replica dei pacchetti tramite il catalogo (dal momento che il catalogo contiene anche pacchetti rimossi dall'elenco).

## <a name="exceptions"></a>Eccezioni

In situazioni eccezionali, quali violazione del copyright e contenuto potenzialmente dannoso, i pacchetti possono essere eliminati manualmente dal team di NuGet. È possibile segnalare un pacchetto usando il pulsante "Segnala abusi" nella pagina dei dettagli del pacchetto NuGet.org. I proprietari dei pacchetti possono accedere al proprio account NuGet.org per contattare il supporto NuGet tramite il pulsante "Supporto tecnico" nella pagina dei dettagli del pacchetto NuGet.org.

## <a name="prohibited-use"></a>Uso non consentito

I pacchetti che soddisfano uno dei criteri seguenti non sono consentiti nella raccolta NuGet pubblica e verranno immediatamente rimossi senza discussione. I proprietari dei pacchetti verranno tuttavia informati della rimozione.

- Contengono malware, adware o qualsiasi tipo di spyware.
- Sono progettati per danneggiare la workstation dello sviluppatore o l'organizzazione.
- Violano diritti di copyright o licenze.
- Contengono contenuto illecito.
- Vengono usati per appropriarsi degli identificatori dei pacchetti, inclusi i pacchetti che hanno un contenuto produttivo nullo. I pacchetti devono contenere codice oppure i proprietari devono concedere l'identificatore a un utente che abbia effettivamente un prodotto da fornire.
- Tentano di fare in modo che la raccolta esegua operazioni per cui non è stata esplicitamente progettata.

Se si rileva un pacchetto che viola gli elementi sopra elencati, fare clic sul collegamento **Report Abuse** (Segnala abusi) nella pagina dei dettagli del pacchetto e inviare un report.

Si noti che il team di NuGet e .NET Foundation si riservano il diritto di modificare questi criteri in qualsiasi momento.

## <a name="unlisting-a-package"></a>Annullamento dell'elenco di un pacchettoUnlisting a package
L'annullamento dell'elenco di una versione del pacchetto lo nasconde dalla ricerca e dalla pagina dei dettagli del pacchetto nuget.org. Ciò consente agli utenti esistenti del pacchetto di continuare a utilizzarlo, ma riduce la nuova adozione poiché il pacchetto non è visibile nella ricerca.

Passaggi per annullare l'elenco di un pacchetto:

1. Seleziona `Your account name` (nell'angolo in alto a destra) >`Manage packages` > `Published packages`
1. Seleziona l'icona "Gestisci pacchetto"
1. Espandere la sezione "Listing" e selezionare la versione del pacchetto
1. Deseleziona "Elenca nei risultati della ricerca" e seleziona "Salva"

La versione specifica del pacchetto non è stata elencata. Per verificarlo, disconnettersi dall'account e passare alla pagina del pacchetto (senza https://www.nuget.org/packages/YOUR-PACKAGE-NAME/la parte della versione) ad esempio: . Vedrai tutte le versioni del pacchetto che **non** sono state in elenco. Tuttavia, il proprietario del pacchetto, una volta effettuato l'accesso, può visualizzare tutte le versioni e il relativo stato di presentazione.

È anche possibile deprecare una versione del pacchetto (nel caso in cui non sia possibile eliminare una versione del pacchetto). Per ulteriori informazioni sulla deprecazione delle versioni dei pacchetti, vedere [Deprechezione dei pacchetti](../deprecate-packages.md).
