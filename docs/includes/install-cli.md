#### <a name="windows"></a><span data-ttu-id="e100b-101">WINDOWS</span><span class="sxs-lookup"><span data-stu-id="e100b-101">Windows</span></span>
1. <span data-ttu-id="e100b-102">Visitare [nuget.org/downloads](https://nuget.org/downloads) e selezionare NuGet 3.3 o versioni successive (non è compatibile con Mono 2.8.6).</span><span class="sxs-lookup"><span data-stu-id="e100b-102">Visit [nuget.org/downloads](https://nuget.org/downloads) and select NuGet 3.3 or higher (2.8.6 is not compatible with Mono).</span></span> <span data-ttu-id="e100b-103">La versione più recente è sempre consigliata e 4.1.0+ è necessario pubblicare i pacchetti in nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e100b-103">The latest version is always recommended, and 4.1.0+ is required to publish packages to nuget.org.</span></span>
2. <span data-ttu-id="e100b-104">Ogni download di `nuget.exe` file direttamente.</span><span class="sxs-lookup"><span data-stu-id="e100b-104">Each download is the `nuget.exe` file directly.</span></span> <span data-ttu-id="e100b-105">Indicare il browser per salvare il file in una cartella di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="e100b-105">Instruct your browser to save the file to a folder of your choice.</span></span> <span data-ttu-id="e100b-106">Il file è *non* un programma di installazione; non verrà visualizzato alcun elemento se viene eseguito direttamente dal browser.</span><span class="sxs-lookup"><span data-stu-id="e100b-106">The file is *not* an installer; you won't see anything if you run it directly from the browser.</span></span>
3. <span data-ttu-id="e100b-107">Aggiungere la cartella in cui è stata inserita `nuget.exe` per la variabile di ambiente PATH per utilizzare lo strumento CLI da qualsiasi posizione.</span><span class="sxs-lookup"><span data-stu-id="e100b-107">Add the folder where you placed `nuget.exe` to your PATH environment variable to use the CLI tool from anywhere.</span></span>

#### <a name="macoslinux"></a><span data-ttu-id="e100b-108">macOS/Linux</span><span class="sxs-lookup"><span data-stu-id="e100b-108">macOS/Linux</span></span>
<span data-ttu-id="e100b-109">I comportamenti possono variare leggermente tramite la distribuzione del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e100b-109">Behaviors may vary slightly by OS distribution.</span></span>

1. <span data-ttu-id="e100b-110">Installare [Mono 4.4.2 o in un secondo momento](http://www.mono-project.com/docs/getting-started/install/).</span><span class="sxs-lookup"><span data-stu-id="e100b-110">Install [Mono 4.4.2 or later](http://www.mono-project.com/docs/getting-started/install/).</span></span>
2. <span data-ttu-id="e100b-111">Eseguire i comandi seguenti al prompt dei comandi della shell:</span><span class="sxs-lookup"><span data-stu-id="e100b-111">Execute the following commands at a shell prompt:</span></span>
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. <span data-ttu-id="e100b-112">Creare un alias aggiungendo il seguente script per il file appropriato per il sistema operativo (in genere `~/.bash_aliases` o `~/.bash_profile`):</span><span class="sxs-lookup"><span data-stu-id="e100b-112">Create an alias by adding the following script to the appropriate file for your OS (typically `~/.bash_aliases` or `~/.bash_profile`):</span></span>
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. <span data-ttu-id="e100b-113">Ricaricare la shell.</span><span class="sxs-lookup"><span data-stu-id="e100b-113">Reload the shell.</span></span>  <span data-ttu-id="e100b-114">Test dell'installazione immettendo `nuget` senza parametri.</span><span class="sxs-lookup"><span data-stu-id="e100b-114">Test the installation by entering `nuget` with no parameters.</span></span> <span data-ttu-id="e100b-115">Guida di NuGet CLI deve essere visualizzato.</span><span class="sxs-lookup"><span data-stu-id="e100b-115">NuGet CLI help should display.</span></span>