---
title: Come pubblicare un pacchetto NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/5/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2342aabd-983e-4db1-9230-57c84fa36969
description: "Istruzioni dettagliate su come pubblicare un pacchetto NuGet in nuget.org o in feed privati e su come gestire la proprietà del pacchetto in nuget.org."
keywords: "pubblicazione di un pacchetto NuGet, pubblicare un pacchetto NuGet, proprietà del pacchetto NuGet, pubblicare in nuget.org, feed NuGet privati"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: fab25931165afb65aa3fd09c5bc37492ce814a49
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="publishing-packages"></a>Pubblicazione di pacchetti

Dopo avere [creato un pacchetto](../create-packages/creating-a-package.md) con `nuget pack`, il processo per renderlo disponibile per altri sviluppatori, pubblicamente o privatamente, è davvero semplice:

- I pacchetti pubblici diventano disponibili per tutti gli sviluppatori a livello globale tramite [nuget.org](https://www.nuget.org/packages/manage/upload), come illustrato in questo argomento.
- I pacchetti privati, disponibili solo per un team o un'organizzazione, sono ospitati in una condivisione file, in un server NuGet privato, in [Gestione pacchetti di Visual Studio Team Services](https://www.visualstudio.com/docs/package/nuget/publish) o in un repository di terze parti, ad esempio myget, ProGet, Nexus Repository e Artifactory. Per altre informazioni, vedere [Panoramica dell'hosting dei pacchetti](../hosting-packages/overview.md).

Questo argomento illustra la pubblicazione in nuget.org. Per la pubblicazione in Visual Studio Team Services, vedere [Package Management](https://www.visualstudio.com/docs/package/nuget/publish) (Gestione pacchetti).

## <a name="publish-to-nugetorg"></a>Pubblicare in nuget.org

Per nuget.org, prima è necessario [effettuare la registrazione a un account gratuito](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) o eseguire l'accesso se si è già registrati:

![Posizione di registrazione e accesso a NuGet](media/publish_NuGetSignIn.png)

Sarà quindi possibile caricare il pacchetto tramite il portale Web di nuget.org, eseguire il push in nuget.org dalla riga di comando o effettuare la pubblicazione durante un processo di integrazione continua/recapito continuo tramite Visual Studio Team Services, come descritto nelle sezioni seguenti.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Portale Web: usare la scheda Upload Package (Carica pacchetto) in nuget.org:

![Caricare un pacchetto con Gestione pacchetti NuGet](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a>Riga di comando:
> [!Important]
> Per eseguire il push dei pacchetti in nuget.org, è necessario usare [nuget.exe v4.1.0 o versione successiva](https://www.nuget.org/downloads), che implementa i [protocolli NuGet](../api/nuget-protocols.md) necessari.

1. Fare clic sul nome utente per passare alle impostazioni dell'account.
2. In **Chiave API** fare clic su **copia negli Appunti** per recuperare la chiave di accesso che sarà necessaria nell'interfaccia della riga di comando:

    ![Copia di una chiave API dalle impostazioni dell'account](media/publish_APIKey.png)

3. Al prompt dei comandi, eseguire il comando seguente:

    ```
    nuget setApiKey Your-API-Key
    ```

    La chiave API viene archiviata nel computer, quindi non sarà più necessario ripetere questo passaggio nello stesso computer.

4. Eseguire il push del pacchetto nella raccolta NuGet usando il comando:

    ```
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

5. Prima di essere resi pubblici, tutti i pacchetti caricati in nuget.org vengono analizzati alla ricerca di virus e rifiutati se vengono trovati virus. Tutti i pacchetti elencati in nuget.org vengono anche analizzati periodicamente.

6. Nell'account in nuget.org fare clic su **Manage my packages** (Gestisci i pacchetti) per visualizzare quello appena pubblicato. Si riceverà anche un messaggio di posta elettronica di conferma. Si noti che l'indicizzazione e la visualizzazione del pacchetto nei risultati della ricerca, dove altri possono trovarlo, potrebbero richiedere qualche minuto. Nella pagina del pacchetto verrà nel frattempo visualizzato il messaggio seguente:

    ![Messaggio indicante che un pacchetto non è ancora indicizzato](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a>Convalida e indicizzazione dei pacchetti

I pacchetti di cui viene eseguito il push in NuGet.org vengono sottoposti a diverse convalide. Quando il pacchetto ha superato tutti i controlli di convalida, l'indicizzazione e la visualizzazione del pacchetto nei risultati della ricerca potrebbero richiedere qualche minuto. Al termine dell'indicizzazione, si riceverà un messaggio di posta elettronica che conferma che il pacchetto è stato pubblicato. Se il pacchetto non supera un controllo di convalida, la pagina dei dettagli del pacchetto verrà aggiornata con l'errore associato e si riceverà anche una notifica tramite posta elettronica.

La convalida e l'indicizzazione del pacchetto richiedono in genere meno di 15 minuti. Se la pubblicazione del pacchetto richiede più tempo del previsto, visitare [status.nuget.org](https://status.nuget.org/) per controllare se si stanno verificando interruzioni in NuGet.org. Se tutti i sistemi sono operativi e il pacchetto non viene pubblicato entro un'ora, accedere a NuGet.org e contattarci usando il collegamento per contattare il supporto tecnico nella pagina del pacchetto.

### <a name="visual-studio-team-services-cicd"></a>Visual Studio Team Services (integrazione continua/recapito continuo)

Se si esegue il push dei pacchetti in nuget.org usando Visual Studio Team Services durante il processo di integrazione continua/recapito continuo, è necessario usare nuget.exe 4.1 o versione successiva nelle attività NuGet. Per informazioni, vedere [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Uso della versione più recente di NuGet nella compilazione) nel blog di Microsoft DevOps.

## <a name="managing-package-owners-on-nugetorg"></a>Gestione dei proprietari dei pacchetti in nuget.org

Anche se ogni file `.nuspec` del pacchetto NuGet definisce gli autori del pacchetto, la raccolta nuget.org non usa tali metadati per definire la proprietà. Nuget.org assegna invece la proprietà iniziale alla persona che pubblica il pacchetto, ovvero l'utente connesso che ha caricato il pacchetto tramite l'interfaccia utente di nuget.org o gli utenti la cui chiave API è stata usata con `nuget SetApiKey` o `nuget push`.

Tutti i proprietari del pacchetto hanno autorizzazioni complete per il pacchetto, incluse l'aggiunta e la rimozione di altri proprietari e la pubblicazione di aggiornamenti.

Per modificare il proprietario di un pacchetto, seguire questa procedura:

1. Accedere a nuget.org con l'account che è il proprietario corrente del pacchetto.
1. Fare clic sul nome utente, quindi su **Manage my packages** (Gestisci i pacchetti) e infine sul pacchetto che si vuole gestire.
1. Fare clic sul collegamento **Manage owners** (Gestisci proprietari) a sinistra.

A questo punto sono disponibili diverse alternative:

1. Per aggiungere un proprietario, immettere il nome account NuGet e fare clic su **Add** (Aggiungi). Viene inviato a tale nuovo comproprietario un messaggio di posta elettronica con un collegamento di conferma. Dopo la conferma, tale persona ha le autorizzazioni complete per aggiungere e rimuovere i proprietari. Fino all'avvenuta conferma, la pagina **Manage owners** (Gestisci proprietari) indica "pending approval" (approvazione in sospeso) per tale persona.
1. Per rimuovere un proprietario, selezionarne il nome in **Manage owners** (Gestisci proprietari) e fare clic su **Remove** (Rimuovi).
1. Per trasferire la proprietà (ad esempio quando la proprietà cambia o un pacchetto è stato pubblicato con l'account errato), è sufficiente aggiungere il nuovo proprietario che, dopo avere confermato la proprietà, potrà rimuovere l'utente dall'elenco.

Per assegnare la proprietà a una società o a un gruppo, creare un account nuget.org usando un alias di posta elettronica che viene inoltrato ai membri del team appropriati. Diversi pacchetti Microsoft ASP.NET, ad esempio, sono in comproprietà con gli account [microsoft](http://nuget.org/profiles/microsoft) e [aspnet](http://nuget.org/profiles/aspnet) e tali alias risultano semplificati.

### <a name="recovering-package-ownership"></a>Ripristino della proprietà di un pacchetto

Può capitare che un pacchetto non abbia un proprietario attivo. È ad esempio possibile che il proprietario originale abbia lasciato la società che produce il pacchetto, che le credenziali nuget.org vadano perse o che bug precedenti nella raccolta abbiano lasciato un pacchetto senza proprietario.

Se il proprietario legittimo di un pacchetto ha la necessità di ripristinare la proprietà, deve usare il [modulo contatto](https://www.nuget.org/policies/Contact) su nuget.org per illustrare la situazione al team di NuGet. Viene quindi messo in atto un processo per verificare la proprietà del pacchetto, che include il tentativo di rintracciare il proprietario esistente tramite l'URL del progetto del pacchetto, Twitter, posta elettronica o altri mezzi. Se ogni tentativo ha esito negativo, è possibile inviare all'utente un nuovo invito a diventare proprietario.
