---
title: Note sulla versione di NuGet 2,5
description: Note sulla versione per NuGet 2,5, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940582d5173f5a53dcd04cf1258fc02a2439af4e
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428716"
---
# <a name="nuget-25-release-notes"></a>Note sulla versione di NuGet 2,5

[Note sulla versione di NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [Note sulla versione di NuGet 2,6](../release-notes/nuget-2.6.md)

NuGet 2,5 è stato rilasciato il 25 aprile 2013. Questa versione era così grande. ci si era costretti a ignorare le versioni 2,3 e 2,4. Fino a oggi, questa è la versione più grande disponibile per NuGet, con oltre [160 elementi di lavoro](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) nella versione.

## <a name="acknowledgements"></a>Riconoscimenti

Vorremmo ringraziare i collaboratori esterni seguenti per i contributi significativi a NuGet 2,5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) : aggiungere monoandroid, MonoTouch e MonoMac all'elenco di identificatori di Framework di destinazione noti.
2. [Andres G. Aragonesi](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) correggere l'ortografia delle `NuGet.targets` per un sistema operativo con distinzione tra maiuscole e minuscole
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Creare la soluzione in mono.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Correzione degli unit test con errore in mono.
5. [Olivier Bellis](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - il comando [#2920](https://nuget.codeplex.com/workitem/2920) -NuGet. exe Pack non propaga le proprietà a MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) modificare il codice di gestione XML per mantenere la formattazione.
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Sono state aggiunte parole riconosciute al dizionario personalizzato per consentire a Build. cmd di avere esito positivo.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Correzione degli unit test durante l'esecuzione in Visual Studio
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Interfaccia estratta da PackageService
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) gestire le dipendenze di progetto durante la compressione
11. [Decostore Xavier](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) supporta la password non crittografata durante l'archiviazione delle credenziali di origine del pacchetto nei file NuGet. cofig
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), correzione [#3191](http://nuget.codeplex.com/workitem/3191) -Descrizione della Guida di Get-Package

Sono inoltre apprezzate le persone seguenti per individuare i bug con NuGet 2,5 beta/RC che sono stati approvati e corretti prima della versione finale:

1. [Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) -MSTest interruppe con le compilazioni NuGet 2,4 e 2,5 più recenti

## <a name="notable-features-in-the-release"></a>Funzionalità rilevanti della versione

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Consenti agli utenti di sovrascrivere i file di contenuto già esistenti

Una delle funzionalità più richieste di tutti i tempi è la possibilità di sovrascrivere i file di contenuto già presenti sul disco quando sono inclusi in un pacchetto NuGet. A partire da NuGet 2,5, questi conflitti vengono identificati e viene richiesto di sovrascrivere i file, mentre in precedenza questi file venivano sempre ignorati.

![Sovrascrivi file di contenuto](./media/NuGet-2.5/overwrite-file.png)

' NuGet. exe Update ' è Install-Package ' dispongono ora di una nuova opzione '-FileConflictAction ' per impostare alcune impostazioni predefinite per gli scenari da riga di comando.

Impostare un'azione predefinita quando un file di un pacchetto esiste già nel progetto di destinazione. Impostare su' Sovrascrivi ' per sovrascrivere sempre i file. Impostare su' ignore ' per ignorare i file. Se non è specificato, verrà richiesto di specificare ogni file in conflitto.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Importazione automatica di file di destinazione e Props di MSBuild

È stata creata una nuova cartella convenzionale al livello principale del pacchetto NuGet.  Come peer per `\lib`, `\content`e `\tools`, è ora possibile includere una cartella `\build` nel pacchetto.  In questa cartella è possibile inserire due file con nomi fissi, `{packageid}.targets` o `{packageid}.props`. Questi due file possono essere direttamente in `build` o in cartelle specifiche del Framework come le altre cartelle. La regola per la selezione della cartella del Framework con la corrispondenza più appropriata è esattamente identica a quella di.

Quando NuGet installa un pacchetto con i file \Build, aggiunge un elemento MSBuild `<Import>` nel file di progetto che punta ai file di `.targets` e `.props`. Il file `.props` viene aggiunto nella parte superiore, mentre il file di `.targets` viene aggiunto alla fine.

### <a name="specify-different-references-per-platform-using-references-element"></a>Specificare riferimenti diversi per piattaforma usando `<References/>` elemento

Prima del 2,5, in `.nuspec` file, l'utente può specificare solo i file di riferimento da aggiungere per tutti i Framework. Ora, con questa nuova funzionalità di 2,5, l'utente può creare l'elemento `<reference/>` per ciascuna piattaforma supportata, ad esempio:

```xml
<references>
    <group targetFramework="net45">
        <reference file="a.dll" />
    </group>
    <group targetFramework="netcore45">
        <reference file="b.dll" />
    </group>
    <group>
        <reference file="c.dll" />
    </group>
</references>
```

Ecco il flusso per il modo in cui NuGet aggiunge i riferimenti ai progetti basati sul file `.nuspec`:

1. Trovare la cartella `lib` appropriata per il Framework di destinazione e ottenere l'elenco degli assembly da tale cartella
1. Trovare separatamente il gruppo References appropriato per il Framework di destinazione e ottenere l'elenco degli assembly dal gruppo. Gruppo di riferimento senza Framework di destinazione specificato è il gruppo di fallback.
1. Trovare l'intersezione dei due elenchi e usarla come riferimento da aggiungere.

Questa nuova funzionalità consentirà agli autori di pacchetti di utilizzare la funzionalità riferimenti per applicare subset di assembly a Framework diversi quando sarebbe altrimenti necessario eseguire assembly duplicati in più cartelle `lib`.

Nota: per usare questa funzionalità, è necessario usare attualmente il pacchetto NuGet. exe. Gestione pacchetti NuGet non supporta ancora questa operazione.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Pulsante Aggiorna tutto per consentire l'aggiornamento di tutti i pacchetti contemporaneamente

Molti di voi conoscono il cmdlet di PowerShell "Update-Package" per aggiornare tutti i pacchetti; ora esiste un modo semplice per eseguire questa operazione anche tramite l'interfaccia utente.

Per provare questa funzionalità:

1. Creare una nuova applicazione MVC ASP.NET
1. Avvia la finestra di dialogo ' Gestisci pacchetti NuGet '
1. Selezionare ' aggiornamenti '
1. Fai clic sul pulsante ' Aggiorna tutto '

![Pulsante Aggiorna tutto nella finestra di dialogo](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Supporto migliorato per il riferimento al progetto per NuGet. exe Pack

Il comando NuGet. exe Pack ora elabora i progetti a cui si fa riferimento con le regole seguenti:

1. Se il progetto a cui si fa riferimento ha un file di `.nuspec` corrispondente, ad esempio è presente un file denominato `proj1.nuspec` nella stessa cartella `proj1.csproj`, questo progetto viene aggiunto come dipendenza al pacchetto, usando l'ID e la versione letti dal file `.nuspec`.
1. In caso contrario, i file del progetto a cui si fa riferimento vengono aggregati nel pacchetto. I progetti a cui fa riferimento questo progetto verranno elaborati con le stesse regole in modo ricorsivo.
1. Vengono aggiunti tutti i file DLL, `.pdb`e `.exe`.
1. Tutti gli altri file di contenuto vengono aggiunti.
1. Tutte le dipendenze sono unite.

In questo modo un progetto a cui si fa riferimento può essere considerato come una dipendenza se è presente un file di `.nuspec`; in caso contrario, diventa parte del pacchetto.

Per altri dettagli, vedere [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Aggiungere una proprietà' versione minima di NuGet ' ai pacchetti

Un nuovo attributo di metadati denominato ' minClientVersion ' può ora indicare la versione minima del client NuGet necessaria per l'utilizzo di un pacchetto.

Questa funzionalità consente all'autore del pacchetto di specificare che un pacchetto funzionerà solo dopo una particolare versione di NuGet. Quando si aggiungono nuove funzionalità di `.nuspec` dopo NuGet 2,5, i pacchetti saranno in grado di richiedere una versione minima di NuGet.

```xml
<metadata minClientVersion="2.6">
```

Se l'utente ha installato NuGet 2,5 e un pacchetto viene identificato con la richiesta 2,6, i segnali visivi verranno assegnati all'utente che indica che il pacchetto non sarà installabile. L'utente verrà quindi guidato per aggiornare la versione di NuGet.

Ciò consente di migliorare l'esperienza esistente in cui i pacchetti iniziano l'installazione, ma non indica che è stata identificata una versione dello schema non riconosciuta.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Non è più necessario aggiornare le dipendenze durante l'installazione del pacchetto

Prima di NuGet 2,5, quando è stato installato un pacchetto che dipende da un pacchetto già installato nel progetto, la dipendenza verrebbe aggiornata come parte della nuova installazione, anche se la versione esistente soddisfa la dipendenza.

A partire da NuGet 2,5, se è già stata soddisfatta una versione di dipendenza, la dipendenza non verrà aggiornata durante le altre installazioni del pacchetto.

**Scenario:**

1. Il repository di origine contiene il pacchetto B con versione 1.0.0 e 1.0.2. Contiene anche il pacchetto A che ha una dipendenza da B (> = 1.0.0).
1. Si supponga che nel progetto corrente sia già installato il pacchetto B versione 1.0.0. A questo punto si vuole installare il pacchetto A.

**In NuGet 2,2 e versioni precedenti:**

* Quando si installa il pacchetto A, NuGet aggiorna automaticamente B a 1.0.2, anche se la versione esistente 1.0.0 soddisfa già il vincolo della versione di dipendenza, che è > = 1.0.0.

**In NuGet 2,5 e versioni successive:**

* NuGet non aggiornerà più B, perché rileva che la versione esistente 1.0.0 soddisfa il vincolo della versione di dipendenza.

Per ulteriori informazioni su questa modifica, leggere l' [elemento di lavoro](http://nuget.codeplex.com/workitem/1681) dettagliato e il thread di [discussione](http://nuget.codeplex.com/discussions/436712)correlato.

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>NuGet. exe genera richieste HTTP con dettaglio dettagliato

Per la risoluzione dei problemi di NuGet. exe o solo per le richieste HTTP eseguite durante le operazioni, l'opzione '-verbose detailed ' ora restituirà tutte le richieste HTTP effettuate.

![Output HTTP di NuGet. exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>il push NuGet. exe supporta ora le origini UNC e delle cartelle

Prima di NuGet 2,5, se si tentasse di eseguire ' NuGet. exe push ' in un'origine del pacchetto basata su un percorso UNC o una cartella locale, il push avrebbe esito negativo. Con la funzionalità di configurazione gerarchica aggiunta di recente, era diventata comune per NuGet. exe avere come destinazione un'origine UNC/cartella o una raccolta NuGet basata su HTTP.

A partire da NuGet 2,5, se NuGet. exe identifica un'origine UNC/cartella, eseguirà la copia del file nell'origine.

Il comando seguente funzionerà ora:

```cli
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>NuGet. exe supporta i file di configurazione specificati in modo esplicito

i comandi NuGet. exe che accedono alla configurazione (tutti tranne ' spec ' è Pack ') supportano ora una nuova opzione '-ConfigFile ', che impone l'uso di un file di configurazione specifico al posto del file di configurazione predefinito in%AppData%\nuget\Nuget.Config.

Esempio:

```cli
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Supporto per progetti nativi

Con NuGet 2,5, gli strumenti NuGet sono ora disponibili per i progetti nativi in Visual Studio. Si prevede che la maggior parte dei pacchetti nativi utilizzerà la funzionalità di importazione di MSBuild precedente, usando uno strumento creato dal [progetto CoApp](http://coapp.org). Per ulteriori informazioni, leggere [i dettagli sullo strumento](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) nel sito Web coapp.org.

Il nome del Framework di destinazione "native" è stato introdotto per i pacchetti in modo da includere i file in \Build, \Content e \Tools quando il pacchetto viene installato in un progetto nativo.  La cartella \`lib ' non viene utilizzata per i progetti nativi.
