---
title: Come pubblicare un pacchetto NuGet
description: Istruzioni dettagliate su come pubblicare un pacchetto NuGet in nuget.org o in feed privati e su come gestire la proprietà del pacchetto in nuget.org.
author: JonDouglas
ms.author: jodou
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 5be7a4d4c31df9f2f4bda7bdb1ff9f4887108578
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775986"
---
# <a name="publishing-packages"></a>Pubblicazione di pacchetti

Dopo avere creato un pacchetto e con il file `.nupkg` a portata di mano, il processo per renderlo disponibile per altri sviluppatori, pubblicamente o privatamente, è davvero semplice:

- I pacchetti pubblici diventano disponibili per tutti gli sviluppatori a livello globale tramite [nuget.org](https://www.nuget.org/packages/manage/upload), come descritto in questo articolo (è richiesto NuGet 4.1.0+).
- I pacchetti privati, disponibili solo per un team o un'organizzazione, sono ospitati in una condivisione file, in un server NuGet privato, in [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) o in un repository di terze parti, ad esempio myget, ProGet, Nexus Repository e Artifactory. Per altre informazioni, vedere [Panoramica dell'hosting dei pacchetti](../hosting-packages/overview.md).

Questo articolo illustra la pubblicazione in nuget.org. Per la pubblicazione in Azure Artifacts vedere [Gestione pacchetti](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Pubblicare in nuget.org

Per nuget.org è necessario accedere con un account Microsoft, con il quale verrà richiesto di registrare l'account in nuget.org.

![Posizione di accesso a NuGet](media/publish_NuGetSignIn.png)

Sarà quindi possibile caricare il pacchetto tramite il portale Web di nuget.org, eseguire il push in nuget.org dalla riga di comando (è richiesto `nuget.exe` 4.1.0+) o effettuare la pubblicazione durante un processo di integrazione continua/recapito continuo tramite Azure DevOps Services, come descritto nelle sezioni seguenti.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Portale Web: usare la scheda Upload Package (Carica pacchetto) in nuget.org

1. Selezionare **Upload** (Carica) nel menu in alto di nuget.org e passare alla posizione del pacchetto.

    ![Caricare un pacchetto in nuget.org](media/publish_UploadYourPackage.PNG)

1. Nuget.org indica se il nome del pacchetto è disponibile. Se non lo è, modificare l'identificatore del pacchetto nel progetto, ricompilare e riprovare a eseguire il caricamento.

1. Se il nome del pacchetto è disponibile, nuget.org apre una sezione **Verify** (Verifica) in cui è possibile esaminare i metadati del manifesto del pacchetto. Per modificare i metadati, modificare il progetto (file di progetto o file `.nuspec`), ricompilare, ricreare il pacchetto e caricarlo nuovamente.

1. In **Import Documentation** (Importa documentazione) è possibile incollare Markdown, selezionare documenti con un URL oppure caricare un file di documentazione.

1. Quando tutte le informazioni sono pronte, selezionare il pulsante **Submit** (Invia).

### <a name="command-line"></a>Riga di comando

Per eseguire il push dei pacchetti in nuget.org, è necessario prima di tutto una chiave API creata in nuget.org. È necessario usare dotnet.exe (.NET Core) o nuget.exe v 4.1.0 o versioni successive, che implementano i protocolli NuGet necessari.
Per ulteriori informazioni, vedere la pagina relativa ai protocolli [.NET Core](/dotnet/core/install/), [nuget.exe](https://www.nuget.org/downloads)e [NuGet](../api/nuget-protocols.md).

#### <a name="create-api-keys"></a>Creare chiavi API

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>Pubblicare con dotnet nuget push

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Pubblicare con nuget push

1. Al prompt dei comandi, eseguire il comando seguente, sostituendo `<your_API_key>` con la chiave ottenuta da nuget.org:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    Questo comando Archivia la chiave API nella configurazione di NuGet, in modo che non sia necessario ripetere questo passaggio nello stesso computer.

    > [!NOTE]
    > La chiave API non viene usata per l'autenticazione con il feed privato. Fare riferimento al [ `nuget sources` comando](../reference/cli-reference/cli-ref-sources.md) per gestire le credenziali per l'autenticazione con l'origine.
    > Le chiavi API possono essere ottenute dai singoli server NuGet. Per creare e gestire APIKeys per nuget.org, vedere [creare chiavi API](#create-api-keys).

1. Eseguire il push del pacchetto nella raccolta NuGet usando il comando seguente:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>Pubblicare i pacchetti firmati

Per inviare pacchetti firmati, è prima di tutto necessario [registrare il certificato](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) usato per firmare i pacchetti. 

> [!Warning]
> nuget.org rifiuta i pacchetti che non soddisfano i [requisiti per i pacchetti firmati](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).

### <a name="package-validation-and-indexing"></a>Convalida e indicizzazione dei pacchetti

I pacchetti di cui viene eseguito il push in nuget.org vengono sottoposti a diverse convalide, ad esempio il controllo antivirus. (Tutti i pacchetti in nuget.org vengono analizzati periodicamente.)

Quando il pacchetto ha superato tutti i controlli di convalida, l'indicizzazione e la visualizzazione del pacchetto nei risultati della ricerca potrebbero richiedere qualche minuto. Al termine dell'indicizzazione, viene visualizzato un messaggio di posta elettronica che conferma che il pacchetto è stato pubblicato. Se il pacchetto non supera un controllo di convalida, la pagina dei dettagli del pacchetto verrà aggiornata con l'errore associato e si riceverà anche una notifica tramite posta elettronica.

La convalida e l'indicizzazione del pacchetto richiedono in genere meno di 15 minuti. Se la pubblicazione del pacchetto richiede più tempo del previsto, visitare [status.NuGet.org](https://status.nuget.org/) per verificare se NuGet.org sta riscontrando interruzioni. Se tutti i sistemi sono operativi e il pacchetto non viene pubblicato entro un'ora, accedere a nuget.org e usare il collegamento per contattare il supporto tecnico nella pagina del pacchetto.

Per visualizzare lo stato di un pacchetto, selezionare **Gestisci pacchetti** con il nome dell'account in NuGet.org. Al termine della convalida, si riceverà un messaggio di posta elettronica di conferma.

Si noti che l'indicizzazione e la visualizzazione del pacchetto nei risultati della ricerca, dove altri possono trovarlo, potrebbero richiedere tempo. Nella pagina del pacchetto viene nel frattempo visualizzato il messaggio seguente:

![Messaggio indicante che un pacchetto non è ancora stato pubblicato](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Azure DevOps Services (CI/CD)

Se si esegue il push dei pacchetti in nuget.org usando Azure DevOps Services durante il processo di integrazione continua/recapito continuo, è necessario usare `nuget.exe` 4.1 o versione successiva nelle attività NuGet. Per informazioni, vedere [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Uso della versione più recente di NuGet nella compilazione) nel blog di Microsoft DevOps.

## <a name="managing-package-owners-on-nugetorg"></a>Gestione dei proprietari dei pacchetti in nuget.org

Anche se ogni file `.nuspec` del pacchetto NuGet definisce gli autori del pacchetto, la raccolta nuget.org non usa tali metadati per definire la proprietà. Nuget.org assegna invece la proprietà iniziale alla persona che pubblica il pacchetto, ovvero l'utente connesso che ha caricato il pacchetto tramite l'interfaccia utente di nuget.org o gli utenti la cui chiave API è stata usata con `nuget SetApiKey` o `nuget push`.

Tutti i proprietari del pacchetto hanno autorizzazioni complete per il pacchetto, incluse l'aggiunta e la rimozione di altri proprietari e la pubblicazione di aggiornamenti.

Per modificare il proprietario di un pacchetto, seguire questa procedura:

1. Accedere a nuget.org con l'account che è il proprietario corrente del pacchetto.
1. Selezionare il nome dell'account, selezionare **Manage packages** (Gestisci pacchetti) ed espandere **Published Packages** (Pacchetti pubblicati).
1. Selezionare il pacchetto che si vuole gestire e quindi sul lato destro selezionare **Manage owners** (Gestisci proprietari).

A questo punto sono disponibili diverse alternative:

1. Rimuovere qualsiasi proprietario elencato in **Current Owners** (Proprietari correnti).
1. Aggiungere un proprietario in **Add Owner** (Aggiungi proprietario) immettendo il nome utente, un messaggio e selezionando **Add** (Aggiungi). Questa azione invia a tale nuovo comproprietario un messaggio di posta elettronica con un collegamento di conferma. Dopo la conferma, tale persona ha le autorizzazioni complete per aggiungere e rimuovere i proprietari. Fino all'avvenuta conferma, la sezione **Current Owners** (Proprietari correnti) indica l'approvazione in sospeso per tale persona.
1. Per trasferire la proprietà (ad esempio quando la proprietà cambia o un pacchetto è stato pubblicato con l'account errato), aggiungere il nuovo proprietario che, dopo avere confermato la proprietà, potrà rimuovere l'utente dall'elenco.

Per assegnare la proprietà a una società o a un gruppo, creare un account nuget.org usando un alias di posta elettronica che viene inoltrato ai membri del team appropriati. Diversi pacchetti Microsoft ASP.NET, ad esempio, sono in comproprietà con gli account [microsoft](https://nuget.org/profiles/microsoft) e [aspnet](https://nuget.org/profiles/aspnet) e tali alias risultano semplificati.

### <a name="recovering-package-ownership"></a>Ripristino della proprietà di un pacchetto

Può capitare che un pacchetto non abbia un proprietario attivo. È ad esempio possibile che il proprietario originale abbia lasciato la società che produce il pacchetto, che le credenziali nuget.org vadano perse o che bug precedenti nella raccolta abbiano lasciato un pacchetto senza proprietario.

Se il proprietario legittimo di un pacchetto ha la necessità di ripristinare la proprietà, deve usare il [modulo contatto](https://www.nuget.org/policies/Contact) su nuget.org per illustrare la situazione al team di NuGet. Viene quindi messo in atto un processo per verificare la proprietà del pacchetto, che include il tentativo di rintracciare il proprietario esistente tramite l'URL del progetto del pacchetto, Twitter, posta elettronica o altri mezzi. Se ogni tentativo ha esito negativo, è possibile inviare all'utente un nuovo invito a diventare proprietario.
