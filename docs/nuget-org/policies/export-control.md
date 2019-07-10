---
title: Criteri di controllo dell'esportazione
description: Criteri che governano le leggi che controllano l'esportazione
author: karann-msft
ms.author: karann
ms.date: 06/27/2019
ms.topic: conceptual
ms.openlocfilehash: 97e7b253bed84fc6e9a97922c19756d138dd0381
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426926"
---
# <a name="export-control-policy"></a>Criteri di controllo dell'esportazione

Il contenuto che si carica in o a cui si accede da NuGet.org può essere soggetto alle leggi degli Stati Uniti che controllano l'esportazione, tra cui le norme EAR (Export Administration Regulations) degli Stati Uniti.  Di seguito vengono fornite alcune informazioni per comodità dell'utente. È tuttavia l'utente ad avere la responsabilità di verificare di usare NuGet.org e tutti i servizi correlati nel rispetto di tutte le leggi e di tutte le normative applicabili, tra cui le leggi degli Stati Uniti per il controllo dell'esportazione, e in conformità con le [Condizioni per l'utilizzo](https://www.nuget.org/policies/Terms) di NuGet.org.

## <a name="publicly-available-encryption-source-code"></a>Codice sorgente di crittografia disponibile pubblicamente

Ai sensi dei requisiti di notifica descritti dalle norme EAR, il codice sorgente di crittografia classificato in ECCN 5D002 non è più soggetto alle norme EAR.  Tale codice sorgente è disponibile pubblicamente, anche se soggetto a un accordo che preveda esplicitamente la concessione in licenza dietro pagamento di una tariffa o la corresponsione di royalty per la produzione a fini commerciali o per la vendita di qualsiasi prodotto sviluppato usando il codice sorgente stesso.

## <a name="notification-requirement"></a>Requisiti di notifica

Come specificato nelle norme EAR (Parti 742.15(b) e 734.3(b)(3)), la persona fisica o giuridica che fornisca o carichi codice sorgente di crittografia deve inviare tramite posta elettronica all'ufficio BIS (Bureau of Industry and Security) degli Stati Uniti e all'ENC Encryption Request Coordinator una notifica della posizione Internet (ad esempio, URL o indirizzo Internet) del codice sorgente di crittografia disponibile pubblicamente classificato in ECCN 5D002 o fornire a ciascuno dei due organismi una copia del codice sorgente di crittografia disponibile pubblicamente. Se il codice sorgente di crittografia viene aggiornato o modificato, è anche necessario fornire copie aggiuntive a ciascuno degli organismi sopra citati ogni volta che la funzionalità di crittografia del codice sorgente viene aggiornata o modificata. Inoltre, se il codice sorgente di crittografia è stato pubblicato su Internet (ad esempio, tramite NuGet.org), è necessario inviare una notifica all'ufficio BIS e all'ENC Encryption Request Coordinator ogni volta che la posizione Internet viene modificata. Non è tuttavia necessario inviare la notifica di aggiornamenti o modifiche apportati al codice sorgente di crittografia presso una posizione notificata in precedenza. In tutti i casi, inviare la notifica o la copia agli indirizzi crypt@bis.doc.gov e enc@nsa.gov.

## <a name="commerical-software"></a>Software commerciale

Il rilascio del codice sorgente disponibile pubblicamente dalla giurisdizione del controllo dell'esportazione attraverso il processo di notifica sopra descritto *non si applica* al software commerciale che incorpora tali elementi o deriva da essi.  L'utente è il solo responsabile del rispetto delle leggi in materia di esportazione per qualsiasi software che incorpori o derivi da codice sorgente o oggetto ospitato tramite NuGet.org.

Per altre informazioni sull'esportazione e sulle limitazioni geografiche all'esportazione, visitare il sito https://www.microsoft.com/en-us/exporting.
