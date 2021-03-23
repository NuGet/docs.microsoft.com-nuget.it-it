---
ms.openlocfilehash: 585537c5e3c7b27e0c7c312db19723d952421ce3
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859558"
---
Nessun contributo è troppo grande o troppo piccolo.

1. Visitare la pagina per modificare in [docs.Microsoft.com/NuGet](https://docs.microsoft.com/nuget/), quindi fare clic sul pulsante **Edit (modifica** ) in alto a destra. Verrà visualizzata la pagina Markdown appropriata nel repository.
1. Modificare il markdown:
    1. Se si includono immagini (usare PNG, in genere), posizionarle nella cartella media che si trova nella cartella dell'argomento. I collegamenti sono quindi `media/<image_name>.png` .
    1. I collegamenti relativi ad altre pagine del docst devono essere nel formato `../<folder>/<topic-file>.md` incluso il training `.md` . Se si sta eseguendo il collegamento a un altro argomento nella stessa cartella, è `../<folder>/` possibile ometterlo. Quando si usano ancoraggi, ricordarsi sempre di includere `.md` prima di `#` .
    1. Quando si usano collegamenti esterni, in particolare per docs.microsoft.com (o msdn.microsoft.com per qualsiasi contenuto precedente), omettere qualsiasi tag di lingua, ad esempio "en-US", in modo che un lettore in un'altra lingua si trovi in una pagina di destinazione nella stessa lingua, se disponibile.
1. Al termine, immettere un messaggio di commit seguente e fare clic su **Proponi modifica file**.
1. Inviare una richiesta pull per la modifica. Si esaminano periodicamente le richieste pull.
1. Grazie!

Se si sta creando un nuovo argomento, tenere presente quanto segue:

1. Posizionare sempre il nuovo argomento in una sottocartella appropriata e seguire le convenzioni per i nomi file, come indicato di seguito.
1. È necessario includere un blocco di metadati come visualizzato in altri argomenti. Le impostazioni predefinite tipiche, ad esempio per MS. workload e MS. Reviewer, sono impostate in docs/docjx.json, quindi è necessario modificare solo quanto segue:

  - title: titolo visualizzato nei risultati della ricerca. Per il SEO, questo è idealmente uguale al numero di primo livello (H1) dell'articolo.
  - Descrizione: abstract dell'articolo visualizzato nei risultati della ricerca.
  - autore: l'ID GitHub dell'autore, a cui vengono assegnati i file di problemi per questo articolo.
  - ms. Author: se l'autore è un dipendente Microsoft, questo è l'alias Microsoft. Utilizzato per la creazione di report e l'invio di commenti e suggerimenti da altri canali.
  - Responsabile: Microsoft alias of the Author ' s Manager, se applicabile.
  - ms. Date: data dell'ultima revisione o revisione dell'articolo nel formato mm/gg/aaaa (usare gli zeri iniziali). Si tratta di una comunicazione con il lettore sull'aggiornamento, quindi non viene aggiornata per le modifiche minime, solo per le revisioni più significative o quando l'articolo è stato riverificato anche se non sono state apportate modifiche.
  - ms. Topic: usato per categorizzare l'articolo nei report. Vedere la tabella seguente. La maggior parte degli articoli sono "concettuali". 
1. Oltre ad aggiungere la pagina, modificare docs/TOC. MD per aggiungere un collegamento a tale pagina.
1. Se si aggiunge un nodo di primo livello al sommario, effettuare anche una voce in docs/index. MD.

| Categoria ms. Topic | Descrizione |
| --- | --- |
| concettuale | Usare per tutti i contenuti che non rientrano in un altro. Viene impostato come predefinito in docfx.json. |
| cenni preliminari | Usare per qualsiasi articolo di panoramica o guida per gli utenti, in genere solo quelli che si trovano in un nodo "Overview" nel sommario. |
| guide rapide | Qualsiasi elemento sotto il nodo "avvio rapido" nel sommario creato in base alle linee guida introduttive. |
| esercitazione | Qualsiasi elemento sotto il nodo "esercitazione" nel sommario creato in base alle linee guida dell'esercitazione. |
| reference | Qualsiasi articolo di tipo riferimento non generato automaticamente. |
| article | Da usare per contenuti con contributo alla community, ovvero qualsiasi elemento all'esterno del team di progettazione o del team docs di Microsoft. |
