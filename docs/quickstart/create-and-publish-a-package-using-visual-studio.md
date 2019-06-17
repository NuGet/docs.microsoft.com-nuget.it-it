---
title: Creare e pubblicare un pacchetto .NET Standard con Visual Studio in Windows
description: Esercitazione sulla creazione e pubblicazione di un pacchetto NuGet .NET Standard con Visual Studio 2017 in Windows.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: d30e89473b5f00895136b75a90d8d95b7645a100
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812987"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Guida introduttiva: Creare e pubblicare un pacchetto NuGet con Visual Studio (.NET Standard, solo Windows)

La creazione di un pacchetto NuGet da una libreria di classi .NET Standard in Visual Studio in Windows e la pubblicazione in nuget.org tramite uno strumento di interfaccia della riga di comando sono un processo semplice.

> [!Note]
> Questa guida introduttiva si applica solo a Visual Studio 2017 per Windows. Visual Studio per Mac non include le funzionalità descritte di seguito. Usare invece gli [strumenti dell'interfaccia della riga di comando dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Prerequisiti

1. Installare qualsiasi edizione di Visual Studio 2017 da [visualstudio.com](https://www.visualstudio.com/) con qualsiasi carico di lavoro correlato a .NET. Visual Studio 2017 include automaticamente le funzionalità di NuGet quando viene installato un carico di lavoro .NET.

1. Installare uno degli strumenti dell'interfaccia della riga di comando.

   * Per l'interfaccia della riga di comando `dotnet`, installare [.NET Core SDK](https://www.microsoft.com/net/download/). L'interfaccia della riga di comando dotnet è necessaria per i progetti .NET Standard che usano il formato in stile SDK (attributo SDK).

   * Per l'interfaccia della riga di comando `nuget.exe`, scaricarla da [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), salvare il file `.exe` in una cartella appropriata e aggiungere tale cartella alla variabile di ambiente PATH. L'interfaccia della riga di comando nuget.exe viene usata per le librerie .NET Standard in formato non in stile SDK.

1. [Registrarsi per ottenere un account gratuito in nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) se non è già disponibile. Quando si crea un nuovo account, viene inviato un messaggio di posta elettronica di conferma. È necessario confermare l'account prima di poter caricare un pacchetto.

## <a name="create-a-class-library-project"></a>Creare un progetto di libreria di classi

È possibile usare un progetto libreria di classi .NET Standard esistente per il codice che si vuole includere in un pacchetto oppure creare un progetto semplice come segue:

1. In Visual Studio scegliere **File > Nuovo > Progetto**, espandere il nodo **Visual C# > .NET Standard**, selezionare il modello "Libreria di classi (.NET Standard)", assegnare al progetto il nome AppLogger e fare clic su **OK**.

1. Fare clic con il pulsante destro del mouse sul file di progetto risultante e scegliere **Compila** per verificare che il progetto sia stato creato correttamente. La DLL è presente nella cartella Debug (o Release se si crea invece tale configurazione).

In un vero pacchetto NuGet si implementano ovviamente molte funzionalità utili, che altri possono sfruttare per compilare nuove applicazioni. In questa procedura dettagliata tuttavia non si scriverà codice aggiuntivo perché una libreria di classi dal modello è sufficiente per creare un pacchetto. Tuttavia, se si desidera del codice funzionale per il pacchetto, usare le opzioni riportate di seguito:

```cs
namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> A meno che non esista un motivo valido per decidere diversamente, .NET Standard è la destinazione preferita per i pacchetti NuGet, perché garantisce la compatibilità con la gamma più ampia di progetti consumer.

## <a name="configure-package-properties"></a>Configurare le proprietà del pacchetto

1. Scegliere il comando di menu **Progetto > Proprietà** e quindi selezionare la scheda **Pacchetto**. (La scheda **Pacchetto** viene visualizzata solo per i progetti di libreria di classi .NET Standard. Se la destinazione è .NET Framework, vedere invece [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) (Creare e pubblicare un pacchetto .NET Framework). Se non viene visualizzata per un progetto .NET Standard, potrebbe essere necessario aggiornare Visual Studio 2017 alla versione più recente.)

    ![Proprietà del pacchetto NuGet in un progetto di Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Per i pacchetti compilati per uso pubblico, prestare particolare attenzione alla proprietà **Tags**, perché i tag consentono ad altri utenti di trovare il pacchetto e di comprenderne le funzioni.

1. Assegnare al pacchetto un identificatore univoco e compilare tutte le altre proprietà desiderate. Per una descrizione delle diverse proprietà, vedere [Informazioni di riferimento sul file .nuspec](../reference/nuspec.md). Tutte queste proprietà vengono incluse nel manifesto `.nuspec` creato da Visual Studio per il progetto.

    > [!Important]
    > È necessario assegnare al pacchetto un identificatore univoco in nuget.org o per qualsiasi host in uso. Per questa procedura dettagliata, si consiglia di includere "Sample" o "Test" nel nome, perché il passaggio di pubblicazione descritto più avanti rende il pacchetto visibile pubblicamente (nonostante sia improbabile che chiunque lo usi effettivamente).
    >
    > Se si tenta di pubblicare un pacchetto con un nome già esistente, viene visualizzato un errore.

1. Facoltativo: per visualizzare le proprietà direttamente nel file di progetto, fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e selezionare **Edit AppLogger.csproj** (Modifica AppLogger.csproj).

## <a name="run-the-pack-command"></a>Eseguire il comando pack

1. Impostare la configurazione da **rilasciare**.

1. Fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e scegliere il comando **Pack**.

    ![Comando pack NuGet nel menu di scelta rapida del progetto di Visual Studio](media/qs_create-vs-02-pack-command.png)

1. Visual Studio compila il progetto e crea il file `.nupkg`. Esaminare i dettagli nella finestra **Output** (simile alla seguente), che contiene il percorso del file di pacchetto. Si noti inoltre che l'assembly compilato si trova in `bin\Release\netstandard2.0` secondo quanto conforme alla destinazione .NET Standard 2.0.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a>Opzione alternativa: pacchetto con MSBuild

In alternativa all'uso del comando di menu **Pack** (Pacchetto), NuGet 4.x+ e MSBuild 15.1+ supportano una destinazione `pack` quando il progetto contiene i dati necessari del pacchetto. Aprire un prompt dei comandi, passare alla cartella del progetto ed eseguire il comando seguente. (In genere, è consigliabile avviare il "Prompt dei comandi per gli sviluppatori per Visual Studio" dal menu Start, in modo che venga configurato con tutti i percorsi necessari per MSBuild.)

```cli
msbuild -t:pack -p:Configuration=Release
```

Pertanto, è possibile trovare il pacchetto nella cartella `bin\Release`.

Per altre opzioni con `msbuild -t:pack`, vedere [Pack e restore di NuGet come destinazioni MSBuild](../reference/msbuild-targets.md#pack-target).

## <a name="publish-the-package"></a>Pubblicare il pacchetto

Dopo aver creato un file `.nupkg`, pubblicarlo in nuget.org usando l'interfaccia della riga di comando `nuget.exe` o `dotnet.exe` insieme a una chiave API acquisita da nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Acquisire la chiave API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a>Pubblicare con dotnet nuget push (interfaccia della riga di comando dotnet)

Questo passaggio è un'alternativa all'uso di `nuget.exe`.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a>Pubblicare con nuget push (interfaccia della riga di comando nuget.exe)

Questo passaggio è un'alternativa all'uso di `dotnet.exe`.

1. Passare alla cartella contenente il file `.nupkg`.

1. Eseguire il comando seguente, specificando il nome del pacchetto e sostituendo il valore di chiave con la chiave API:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe visualizza i risultati del processo di pubblicazione:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Vedere [nuget push](../tools/cli-ref-push.md).

### <a name="publish-errors"></a>Errori di pubblicazione

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Gestire il pacchetto pubblicato

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a>Aggiunta di un file leggimi e di altri file

Per specificare direttamente i file da includere nel pacchetto, modificare il file di progetto e usare la proprietà `content`:

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

Verrà incluso un file denominato `readme.txt` nella radice del pacchetto. Visual Studio visualizza i contenuti del file come testo normale subito dopo avere installato direttamente il pacchetto. I file leggimi non vengono visualizzati per i pacchetti installati come dipendenze. Ecco ad esempio come viene visualizzato il file leggimi per il pacchetto HtmlAgilityPack:

![Visualizzazione di un file leggimi per un pacchetto NuGet durante l'installazione](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> La semplice aggiunta del file readme.txt nella radice del progetto non consente di includerlo nel pacchetto risultante.

## <a name="related-topics"></a>Argomenti correlati

- [Creare un pacchetto](../create-packages/creating-a-package.md)
- [Pubblicare un pacchetto](../create-packages/publish-a-package.md)
- [Pacchetti in versione non definitiva](../create-packages/Prerelease-Packages.md)
- [Supportare più framework di destinazione](../create-packages/supporting-multiple-target-frameworks.md)
- [Controllo delle versioni dei pacchetti](../reference/package-versioning.md)
- [Creazione di pacchetti localizzati](../create-packages/creating-localized-packages.md)
- [Documentazione della libreria .NET Standard](/dotnet/articles/standard/library)
- [Portabilità in .NET Core da .NET Framework](/dotnet/articles/core/porting/index)
