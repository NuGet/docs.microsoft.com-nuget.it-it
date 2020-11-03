---
ms.openlocfilehash: 9c3cb22c8c220a7297eb88db6ff0941e4c11c914
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496045"
---
Dal profilo personale in nuget.org selezionare **Manage Packages** (Gestisci pacchetti) per visualizzare quello appena pubblicato. Viene anche inviato un messaggio di posta elettronica di conferma. Si noti che l'indicizzazione e la visualizzazione del pacchetto nei risultati della ricerca, dove gli altri utenti possono trovarlo, potrebbero richiedere qualche minuto. In questo intervallo di tempo la pagina del pacchetto visualizza un messaggio simile al seguente:

![Il pacchetto non è stato ancora indicizzato. Verrà visualizzato nei risultati della ricerca e sarà disponibile per l'installazione e il ripristino al termine dell'indicizzazione.](../media/QS_Create-03-NotIndexed.png)

Ecco fatto! È stato pubblicato in nuget.org il primo pacchetto NuGet, che gli altri sviluppatori possono usare nei propri progetti.

Se in questa procedura dettagliata è stato creato un pacchetto che non è effettivamente utile (ad esempio un pacchetto creato con una libreria di classi vuota), è necessario *rimuovere* il pacchetto per nasconderlo dai risultati della ricerca:

1. In nuget.org selezionare il nome utente (in alto a destra della pagina) e quindi selezionare **Manage Packages** (Gestisci pacchetti).

1. Individuare il pacchetto che si vuole rimuovere in **Published** (Pubblicato) e selezionare l'icona del Cestino a destra:

    ![Icona del Cestino visualizzata per un pacchetto pubblicato in nuget.org](../media/qs_create-vs-03-trash-can.png)

1. Nella pagina successiva deselezionare la casella di controllo **List (package-name) in search results** (Includi nome-pacchetto nei risultati della ricerca) e selezionare **Save** (Salva):

    ![Deselezione della casella di controllo per la pubblicazione di un pacchetto in nuget.org](../media/qs_create-vs-04-unlist.png)