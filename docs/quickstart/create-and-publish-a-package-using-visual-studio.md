---
title: Creare e pubblicare un pacchetto NuGet .NET Standard - Visual Studio in Windows
description: Esercitazione sulla creazione e pubblicazione di un pacchetto NuGet .NET Standard con Visual Studio in Windows.
author: JonDouglas
ms.author: jodou
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 53f54f6723ad10fca2ed6f75290ba3829dfb9a5e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775688"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Guida introduttiva: Creare e pubblicare un pacchetto NuGet con Visual Studio (.NET Standard, solo Windows)

La creazione di un pacchetto NuGet da una libreria di classi .NET Standard in Visual Studio in Windows e la pubblicazione in nuget.org tramite uno strumento di interfaccia della riga di comando sono un processo semplice.

> [!Note]
> Se si usa Visual Studio per Mac, fare riferimento a [queste informazioni](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) per la creazione di un pacchetto NuGet o usare gli [strumenti dell'interfaccia della riga di comando dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).

## <a name="prerequisites"></a>Prerequisiti

1. Installare qualsiasi edizione di Visual Studio 2019 da [visualstudio.com](https://www.visualstudio.com/) con qualsiasi carico di lavoro correlato a .NET Core.

1. Se non è già installata, installare l'interfaccia della riga di comando di `dotnet`.

   Per l'interfaccia della riga di comando `dotnet`, a partire da Visual Studio 2017, l'interfaccia della riga di comando `dotnet` viene installata automaticamente con qualsiasi carico di lavoro .NET Core correlato. In caso contrario, installare [.NET Core SDK](https://www.microsoft.com/net/download/) per ottenere l'interfaccia della riga di comando `dotnet`. L'interfaccia della riga di comando `dotnet` è necessaria per i progetti .NET Standard che usano il [formato di tipo SDK](../resources/check-project-format.md) (attributo SDK). Il modello di libreria di classi .NET Standard predefinito in Visual Studio 2017 e versioni successive, usato in questo articolo, usa l'attributo SDK.
   
   > [!Important]
   > Se si utilizza un progetto non di tipo SDK, seguire invece le procedure in [Creare e pubblicare un pacchetto .NET Framework (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) per creare e pubblicare il pacchetto. Per questo articolo, è consigliabile usare l'interfaccia della riga di comando `dotnet`. Sebbene sia possibile pubblicare un pacchetto NuGet usando l'interfaccia della riga di comando `nuget.exe`, alcuni dei passaggi descritti in questo articolo sono specifici per i progetti di tipo SDK e l'interfaccia della riga di comando dotnet. L'interfaccia della riga di comando nuget.exe per i [progetti non di tipo SDK](../resources/check-project-format.md) (in genere .NET Framework).

1. [Registrarsi per ottenere un account gratuito in nuget.org](../nuget-org/individual-accounts.md#add-a-new-individual-account) se non è già disponibile. Quando si crea un nuovo account, viene inviato un messaggio di posta elettronica di conferma. È necessario confermare l'account prima di poter caricare un pacchetto.

## <a name="create-a-class-library-project"></a>Creare un progetto di libreria di classi

È possibile usare un progetto libreria di classi .NET Standard esistente per il codice che si vuole includere in un pacchetto oppure creare un progetto semplice come segue:

1. In Visual Studio scegliere **File > Nuovo > Progetto**, espandere il nodo **Visual C# > .NET Standard**, selezionare il modello "Libreria di classi (.NET Standard)", assegnare al progetto il nome AppLogger e fare clic su **OK**.

   > [!Tip]
   > A meno che non esista un motivo valido per decidere diversamente, .NET Standard è la destinazione preferita per i pacchetti NuGet, perché garantisce la compatibilità con la gamma più ampia di progetti consumer.

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

## <a name="configure-package-properties"></a>Configurare le proprietà del pacchetto

1. Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e scegliere il comando di menu **Proprietà**, quindi selezionare la scheda **Pacchetto**.

   La scheda **Pacchetto** viene visualizzata solo per i progetti di tipo SDK in Visual Studio, in genere progetti di libreria di classi .NET Standard o .NET Core. Per i progetti non di tipo SDK (in genere .NET Framework), [eseguire la migrazione del progetto](../consume-packages/migrate-packages-config-to-package-reference.md) o vedere [Creare e pubblicare un pacchetto .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) per istruzioni dettagliate.

    ![Proprietà del pacchetto NuGet in un progetto di Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Per i pacchetti compilati per uso pubblico, prestare particolare attenzione alla proprietà **Tags**, perché i tag consentono ad altri utenti di trovare il pacchetto e di comprenderne le funzioni.

1. Assegnare al pacchetto un identificatore univoco e compilare tutte le altre proprietà desiderate. Per un mapping delle proprietà di MSBuild (progetto di tipo SDK) alle proprietà in un file con estensione *nuspec*, vedere [Destinazione pack](../reference/msbuild-targets.md#pack-target). Per le descrizioni delle proprietà, vedere [Informazioni di riferimento sul file .nuspec](../reference/nuspec.md). Tutte queste proprietà vengono incluse nel manifesto `.nuspec` creato da Visual Studio per il progetto.

    > [!Important]
    > È necessario assegnare al pacchetto un identificatore univoco in nuget.org o per qualsiasi host in uso. Per questa procedura dettagliata, si consiglia di includere "Sample" o "Test" nel nome, perché il passaggio di pubblicazione descritto più avanti rende il pacchetto visibile pubblicamente (nonostante sia improbabile che chiunque lo usi effettivamente).
    >
    > Se si tenta di pubblicare un pacchetto con un nome già esistente, viene visualizzato un errore.

1. (Facoltativo) Per visualizzare le proprietà direttamente nel file di progetto, fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e scegliere **Modifica AppLogger.csproj**.

   Questa opzione è disponibile solo a partire da Visual Studio 2017 per i progetti che usano l'attributo SDK. In caso contrario, fare clic con il pulsante destro del mouse sul progetto e scegliere **Scarica progetto**. Fare quindi clic con il pulsante destro del mouse sul progetto scaricato e scegliere **Modifica AppLogger.csproj**.

## <a name="run-the-pack-command"></a>Eseguire il comando pack

1. Impostare la configurazione da **rilasciare**.

1. Fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e scegliere il comando **Pack**.

    ![Comando pack NuGet nel menu di scelta rapida del progetto di Visual Studio](media/qs_create-vs-02-pack-command.png)

    Se non viene visualizzato il comando **Pack**, il progetto non è probabilmente un progetto di tipo SDK ed è necessario usare l'interfaccia della riga di comando `nuget.exe`. [Eseguire la migrazione del progetto](../consume-packages/migrate-packages-config-to-package-reference.md) e usare l'interfaccia della riga di comando `dotnet` oppure vedere [Creare e pubblicare un pacchetto .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) per istruzioni dettagliate.

1. Visual Studio compila il progetto e crea il file `.nupkg`. Esaminare i dettagli nella finestra **Output** (simile alla seguente), che contiene il percorso del file di pacchetto. Si noti inoltre che l'assembly compilato si trova in `bin\Release\netstandard2.0` secondo quanto conforme alla destinazione .NET Standard 2.0.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a>(Facoltativo) Generare il pacchetto in fase di compilazione

È possibile configurare Visual Studio per generare automaticamente il pacchetto NuGet quando si compila il progetto.

1. In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto e scegliere **Proprietà**.

2. Nella scheda **Pacchetto** selezionare **Genera pacchetto NuGet durante la compilazione**.

   ![Generare automaticamente il pacchetto in fase di compilazione](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> Quando si genera automaticamente il pacchetto, il tempo di creazione del pacchetto aumenta il tempo di compilazione per il progetto.

### <a name="optional-pack-with-msbuild"></a>(Facoltativo) Creare il pacchetto con MSBuild

Come alternativa all'uso del comando di menu **Pack** , NuGet 4. x + e MSBuild 15.1 + supportano una `pack` destinazione quando il progetto contiene i dati necessari del pacchetto. Aprire un prompt dei comandi, passare alla cartella del progetto ed eseguire il comando seguente. (In genere, è consigliabile avviare il "Prompt dei comandi per gli sviluppatori per Visual Studio" dal menu Start, in modo che venga configurato con tutti i percorsi necessari per MSBuild.)

Per altre informazioni, vedere [Creare un pacchetto usando MSBuild](../create-packages/creating-a-package-msbuild.md).

## <a name="publish-the-package"></a>Pubblicare il pacchetto

Dopo aver creato un file `.nupkg`, pubblicarlo in nuget.org usando l'interfaccia della riga di comando `nuget.exe` o `dotnet.exe` insieme a una chiave API acquisita da nuget.org.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Acquisire la chiave API

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a>Pubblicare con l'interfaccia della riga di comando di dotnet o nuget.exe

Selezionare la scheda per lo strumento dell'interfaccia della riga di comando, ovvero **Interfaccia della riga di comando di .NET Core** (interfaccia della riga di comando di dotnet) o **NuGet** (Interfaccia della riga di comando di nuget.exe).

# <a name="net-core-cli"></a>[Interfaccia della riga di comando di .NET Core](#tab/netcore-cli)

Questo passaggio è l'alternativa consigliata all'uso di `nuget.exe`.

Prima di poter pubblicare il pacchetto, è necessario aprire una riga di comando.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[NuGet](#tab/nuget)

Questo passaggio è un'alternativa all'uso di `dotnet.exe`.

1. Aprire una riga di comando e passare alla cartella che contiene il file `.nupkg`.

1. Eseguire il comando seguente, specificando il nome del pacchetto (ID pacchetto univoco) e sostituendo il valore di chiave con la chiave API:

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

Vedere [nuget push](../reference/cli-reference/cli-ref-push.md).

---

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

## <a name="related-video"></a>Video correlato

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

Trova altri video su NuGet su [Channel 9](https://channel9.msdn.com/Series/NuGet-101) e [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).

## <a name="related-topics"></a>Argomenti correlati

- [Creare un pacchetto](../create-packages/creating-a-package-dotnet-cli.md)
- [Pubblicare un pacchetto](../nuget-org/publish-a-package.md)
- [Pacchetti in versione non definitiva](../create-packages/Prerelease-Packages.md)
- [Supportare più framework di destinazione](../create-packages/multiple-target-frameworks-project-file.md)
- [Controllo delle versioni dei pacchetti](../concepts/package-versioning.md)
- [Creazione di pacchetti localizzati](../create-packages/creating-localized-packages.md)
- [Documentazione della libreria .NET Standard](/dotnet/articles/standard/library)
- [Portabilità in .NET Core da .NET Framework](/dotnet/articles/core/porting/index)
