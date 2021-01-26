---
title: Eliminazione di pacchetti NuGet da nuget.org
description: Criteri per la rimozione di pacchetti dall'elenco di nuget.org; l'eliminazione permanente non è supportata, salvo quando i pacchetti violano altri criteri.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: e5c62177b40162cb8b6b37b0d272fb7a945156c1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775713"
---
# <a name="deleting-packages"></a>Eliminazione di pacchetti

nuget.org non supporta l'eliminazione permanente dei pacchetti. Questa operazione comporterebbe l'interruzione di tutti i progetti che dipendono dalla disponibilità del pacchetto eliminato, in particolare con i flussi di lavoro di compilazione che implicano il ripristino del pacchetto.

nuget.org supporta l'annullamento dell' [elenco di un pacchetto](#unlisting-a-package), che può essere eseguito nella pagina di gestione dei pacchetti nel sito Web. I pacchetti rimossi dall'elenco non vengono visualizzati su nuget.org o nell'interfaccia utente di Visual Studio, né compaiono all'interno dei risultati della ricerca. I pacchetti rimossi dall'elenco, tuttavia, possono essere ancora scaricati e installati usando il numero di versione esatto, che supporta il ripristino del pacchetto. Inoltre, i pacchetti rimossi dall'elenco potrebbero essere ancora individuati negli scenari specifici seguenti:

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

## <a name="unlisting-a-package"></a>Disintegrazione di un pacchetto
Se si rimuove dall'elenco la versione di un pacchetto, questa viene nascosta dalla ricerca e dalla pagina dei dettagli del pacchetto nuget.org. Ciò consente agli utenti esistenti del pacchetto di continuare a usarlo, ma riduce la nuova adozione perché il pacchetto non è visibile nella ricerca.

Passaggi per l'elenco di un pacchetto:

1. Selezionare `Your account name` (nell'angolo in alto a destra) >`Manage packages` > `Published packages`
1. Selezionare l'icona "Gestisci pacchetto"
1. Espandere la sezione "elenco" e selezionare la versione del pacchetto
1. Deselezionare "elenca nei risultati della ricerca" e selezionare "Salva"

La versione del pacchetto specifica è ora riportata nell'elenco. Per verificarlo, disconnettere l'account e passare alla pagina del pacchetto, senza la parte relativa alla versione, ad esempio: https://www.nuget.org/packages/YOUR-PACKAGE-NAME/ . Vengono visualizzate tutte le versioni del pacchetto che **non** sono state riportate nell'elenco. Tuttavia, al momento dell'accesso, il proprietario del pacchetto può visualizzare tutte le versioni e il relativo stato di visualizzazione.

È anche possibile deprecare una versione del pacchetto, nel caso in cui non sia possibile eliminare una versione del pacchetto. Per ulteriori informazioni su come deprecare le versioni dei pacchetti, vedere [deprecating Packages](../deprecate-packages.md).
