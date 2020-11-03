---
ms.openlocfilehash: 9c3cb22c8c220a7297eb88db6ff0941e4c11c914
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496045"
---
<span data-ttu-id="a8379-101">Dal profilo personale in nuget.org selezionare **Manage Packages** (Gestisci pacchetti) per visualizzare quello appena pubblicato.</span><span class="sxs-lookup"><span data-stu-id="a8379-101">From your profile on nuget.org, select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="a8379-102">Viene anche inviato un messaggio di posta elettronica di conferma.</span><span class="sxs-lookup"><span data-stu-id="a8379-102">You also receive a confirmation email.</span></span> <span data-ttu-id="a8379-103">Si noti che l'indicizzazione e la visualizzazione del pacchetto nei risultati della ricerca, dove gli altri utenti possono trovarlo, potrebbero richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="a8379-103">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="a8379-104">In questo intervallo di tempo la pagina del pacchetto visualizza un messaggio simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a8379-104">During that time your package page shows the message below:</span></span>

![Il pacchetto non è stato ancora indicizzato.](../media/QS_Create-03-NotIndexed.png)

<span data-ttu-id="a8379-107">Ecco fatto!</span><span class="sxs-lookup"><span data-stu-id="a8379-107">And that's it!</span></span> <span data-ttu-id="a8379-108">È stato pubblicato in nuget.org il primo pacchetto NuGet, che gli altri sviluppatori possono usare nei propri progetti.</span><span class="sxs-lookup"><span data-stu-id="a8379-108">You've just published your first NuGet package to nuget.org that other developers can use in their own projects.</span></span>

<span data-ttu-id="a8379-109">Se in questa procedura dettagliata è stato creato un pacchetto che non è effettivamente utile (ad esempio un pacchetto creato con una libreria di classi vuota), è necessario *rimuovere* il pacchetto per nasconderlo dai risultati della ricerca:</span><span class="sxs-lookup"><span data-stu-id="a8379-109">If in this walkthrough you created a package that isn't actually useful (such as a package created with an empty class library), you should *unlist* the package to hide it from search results:</span></span>

1. <span data-ttu-id="a8379-110">In nuget.org selezionare il nome utente (in alto a destra della pagina) e quindi selezionare **Manage Packages** (Gestisci pacchetti).</span><span class="sxs-lookup"><span data-stu-id="a8379-110">On nuget.org, select your user name (upper right of the page), then select **Manage Packages**.</span></span>

1. <span data-ttu-id="a8379-111">Individuare il pacchetto che si vuole rimuovere in **Published** (Pubblicato) e selezionare l'icona del Cestino a destra:</span><span class="sxs-lookup"><span data-stu-id="a8379-111">Locate the package you want to unlist under **Published** and select the trash can icon on the right:</span></span>

    ![Icona del Cestino visualizzata per un pacchetto pubblicato in nuget.org](../media/qs_create-vs-03-trash-can.png)

1. <span data-ttu-id="a8379-113">Nella pagina successiva deselezionare la casella di controllo **List (package-name) in search results** (Includi nome-pacchetto nei risultati della ricerca) e selezionare **Save** (Salva):</span><span class="sxs-lookup"><span data-stu-id="a8379-113">On the subsequent page, clear the box labeled **List (package-name) in search results** and select **Save** :</span></span>

    ![Deselezione della casella di controllo per la pubblicazione di un pacchetto in nuget.org](../media/qs_create-vs-04-unlist.png)