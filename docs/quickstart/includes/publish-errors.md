---
ms.openlocfilehash: b0af2000b1f43cd0b91f2c95dfc0c11540a94cab
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495968"
---
<span data-ttu-id="4d144-101">Gli errori dal comando `push` indicano in genere il problema.</span><span class="sxs-lookup"><span data-stu-id="4d144-101">Errors from the `push` command typically indicate the problem.</span></span> <span data-ttu-id="4d144-102">Ad esempio, è possibile avere dimenticato di aggiornare il numero di versione nel progetto e quindi tentare di pubblicare un pacchetto già esistente.</span><span class="sxs-lookup"><span data-stu-id="4d144-102">For example, you may have forgotten to update the version number in your project and are therefore trying to publish a package that already exists.</span></span>

<span data-ttu-id="4d144-103">È anche possibile che vengano visualizzati errori quando si tenta di pubblicare un pacchetto usando un identificatore già esistente nell'host.</span><span class="sxs-lookup"><span data-stu-id="4d144-103">You also see errors when trying to publish a package using an identifier that already exists on the host.</span></span> <span data-ttu-id="4d144-104">Il nome "AppLogger", ad esempio, esiste già.</span><span class="sxs-lookup"><span data-stu-id="4d144-104">The name "AppLogger", for example, already exists.</span></span> <span data-ttu-id="4d144-105">In tal caso, il comando `push` genera l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="4d144-105">In such a case, the `push` command gives the following error:</span></span>

```output
Response status code does not indicate success: 403 (The specified API key is invalid,
has expired, or does not have permission to access the specified package.).
```

<span data-ttu-id="4d144-106">Se si usa una chiave API valida appena creata, questo messaggio indica un conflitto di denominazione, condizione non completamente chiara nella parte dell'errore relativa alle autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="4d144-106">If you're using a valid API key that you just created, then this message indicates a naming conflict, which isn't entirely clear from the "permission" part of the error.</span></span> <span data-ttu-id="4d144-107">Modificare l'identificatore del pacchetto, ricompilare il progetto, ricreare il file `.nupkg` e quindi ripetere il comando `push`.</span><span class="sxs-lookup"><span data-stu-id="4d144-107">Change the package identifier, rebuild the project, recreate the `.nupkg` file, and retry the `push` command.</span></span>