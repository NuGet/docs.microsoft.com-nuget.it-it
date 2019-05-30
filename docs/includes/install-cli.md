---
ms.openlocfilehash: 1f65939493cf423a76c024607264acee6c7e9050
ms.sourcegitcommit: ef08f376688f0191a8d3d873b6a4386afd799373
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/28/2019
ms.locfileid: "66271500"
---
#### <a name="windows"></a><span data-ttu-id="d8617-101">WINDOWS</span><span class="sxs-lookup"><span data-stu-id="d8617-101">Windows</span></span>

> [!Note]
> <span data-ttu-id="d8617-102">Per l'esecuzione di NuGet.exe 5.0 e versioni successive è richiesto .NET Framework 4.7.2 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="d8617-102">NuGet.exe 5.0 and later require .NET Framework 4.7.2 or later to execute.</span></span>

1. <span data-ttu-id="d8617-103">Visitare [nuget.org/downloads](https://nuget.org/downloads) e selezionare NuGet 3.3 o versioni successive (la versione 2.8.6 non è compatibile con Mono).</span><span class="sxs-lookup"><span data-stu-id="d8617-103">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="d8617-104">È sempre consigliata la versione più recente e la versione 4.1.0+ è obbligatoria per pubblicare i pacchetti in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="d8617-104">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
1. <span data-ttu-id="d8617-105">Ogni download è direttamente il file `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="d8617-105">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="d8617-106">Indicare al browser di salvare il file in una cartella di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="d8617-106">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="d8617-107">Il file *non* è un programma di installazione. Non verrà visualizzato alcun elemento se lo si esegue direttamente dal browser.</span><span class="sxs-lookup"><span data-stu-id="d8617-107">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
1. <span data-ttu-id="d8617-108">Aggiungere la cartella in cui è stato posizionato il file `nuget.exe` alla variabile di ambiente PATH per usare lo strumento dell'interfaccia della riga di comando da qualsiasi posizione.</span><span class="sxs-lookup"><span data-stu-id="d8617-108">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="d8617-109">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="d8617-109">macOS/Linux</span></span>

<span data-ttu-id="d8617-110">I comportamenti possono variare leggermente in base alla distribuzione del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="d8617-110">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="d8617-111">Installare [Mono 4.4.2 o versioni successive](http://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="d8617-111">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>

1. <span data-ttu-id="d8617-112">Eseguire il comando seguente da un prompt della shell:</span><span class="sxs-lookup"><span data-stu-id="d8617-112">Execute the following command at a shell prompt:</span></span>

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. <span data-ttu-id="d8617-113">Creare un alias aggiungendo lo script seguente al file appropriato per il sistema operativo (in genere `~/.bash_aliases` o `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="d8617-113">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. <span data-ttu-id="d8617-114">Ricaricare la shell.</span><span class="sxs-lookup"><span data-stu-id="d8617-114">Reload the shell.</span></span>  <span data-ttu-id="d8617-115">Testare l'installazione immettendo `nuget` senza parametri.</span><span class="sxs-lookup"><span data-stu-id="d8617-115">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="d8617-116">Dovrebbe essere visualizzata la Guida dell'interfaccia della riga di comando di NuGet.</span><span class="sxs-lookup"><span data-stu-id="d8617-116">NuGet CLI help should display.</span></span>
