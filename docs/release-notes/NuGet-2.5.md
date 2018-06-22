---
title: Note sulla versione 2.5 di NuGet
description: Note sulla versione per NuGet 2.5 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: accea5033e44927259537b5047a4a821babc6146
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2018
ms.locfileid: "32045003"
---
# <a name="nuget-25-release-notes"></a>Note sulla versione 2.5 di NuGet

[Note sulla versione 2.2.1 NuGet](../release-notes/nuget-2.2.1.md) | [note sulla versione 2.6 NuGet](../release-notes/nuget-2.6.md)

NuGet 2.5 è stata rilasciata il 25 aprile 2013. Questa versione è stata così grande, è stato ritenuto obbligati a ignorare versioni 2.3 e 2.4. Per data, questa è la versione più grande, abbiamo utilizzato per NuGet, con su [gli elementi di lavoro di 160](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) nella versione.

## <a name="acknowledgements"></a>Riconoscimenti

Si ringraziano i collaboratori esterni seguenti per il loro contributo significativo a NuGet 2.5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -aggiungere MonoAndroid MonoTouch e MonoMac all'elenco di identificatori di framework di destinazione noti.
2. [Aragoneses g. Andres](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -correggere l'ortografia del `NuGet.targets` per un sistema operativo di distinzione maiuscole/minuscole
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Rendere la soluzione di compilazione su Mono.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Correggere gli unit test non superati in Mono.
5. [Olivier Dagenais](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -comando di nuget.exe pack non propaga le proprietà di MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) - XML modificato la gestione del codice per mantenere la formattazione.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Riconosciuta per parole aggiunte al dizionario personalizzato per consentire build.cmd abbia esito positivo.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Correggere gli unit test durante l'esecuzione in Visual Studio localizzata.
9. [Gareth Evans](https://www.codeplex.com/site/users/view/garethevans)
    - Interfaccia estratto da PackageService
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) -gestire le dipendenze di progetto quando compressione
11. [Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -supporto Password come testo non crittografato quando si archiviano le credenziali dell'origine del pacchetto nel file nuget.cofig
12. [Supervisione relativo personale James](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -descrizione della Guida correggere Get-Package

Si apprezza anche gli utenti seguenti per la ricerca di bug con NuGet 2.5 Beta o RC che sono stati approvati e risolto prima della versione finale:

1. [Tony parete](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) MSTest interrotto con più di recente NuGet 2.4 e 2.5 compilazioni:

## <a name="notable-features-in-the-release"></a>Importanti funzionalità nella versione

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Consentire agli utenti di sovrascrivere i file di contenuto che esistono già

Una delle funzionalità più richieste di tutto il tempo è stata la possibilità di sovrascrivere i file di contenuto che già esistono nel disco quando incluso in un pacchetto NuGet. A partire da NuGet 2.5, tali conflitti vengono identificati e viene chiesto di sovrascrivere i file, mentre in precedenza sempre ignorati questi file.

![Sovrascrivere i file di contenuto](./media/NuGet-2.5/overwrite-file.png)

'nuget.exe update' e 'Install-Package' ora dispongono di una nuova opzione '-FileConflictAction' per impostare alcuni valori predefiniti per gli scenari della riga di comando.

Impostare un'azione predefinita quando un file da un pacchetto esiste già nel progetto di destinazione. Impostare su 'Sovrascrivi' per sovrascrivere sempre i file. Impostare su 'Ignora' per ignorare i file. Se non specificato, verrà richiesto per ogni file in conflitto.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Importazione automatica dei file props e destinazioni di MSBuild

Una nuova cartella convenzionale è stata creata al primo livello del pacchetto NuGet.  Allo stesso livello `\lib`, `\content`, e `\tools`, ora è possibile includere un `\build` cartella nel pacchetto.  In questa cartella, è possibile inserire due file con nomi fissi, `{packageid}.targets` o `{packageid}.props`. Questi due file possono essere direttamente in `build` o in cartelle specifiche del framework come le altre cartelle. La regola per scegliere la cartella di .NET framework corrispondente con mapping più appropriato è esattamente uguale a quello di quelli.

Quando si NuGet installa un pacchetto con file \build, aggiungerà un MSBuild `<Import>` nel file di progetto che punta all'elemento di `.targets` e `.props` file. Il `.props` file viene aggiunto all'inizio, mentre il `.targets` file viene aggiunto alla fine.

### <a name="specify-different-references-per-platform-using-references-element"></a>Specificare i riferimenti diversi per ogni piattaforma utilizzando `<References/>` elemento

Prima di 2.5 in `.nuspec` file utente può specificare solo i file di riferimento da aggiungere per tutti i framework. Ora con questa nuova funzionalità in 2.5, è possibile creare l'utente di `<reference/>` elemento per ogni piattaforma supportata, ad esempio:

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

Di seguito viene illustrato il flusso per la modalità NuGet aggiunge riferimenti ai progetti basati sul `.nuspec` file:

1. Trovare il `lib` cartella appropriata per il framework di destinazione e ottiene l'elenco degli assembly dalla cartella
1. Separatamente, trovare il gruppo di riferimenti che è appropriato per il framework di destinazione e ottenere l'elenco degli assembly da quel gruppo. Gruppo di riferimenti senza il framework di destinazione specificato è il gruppo di fallback.
1. Trovare l'intersezione dei due elenchi e utilizzarlo come i riferimenti da aggiungere

Questa nuova funzionalità consente agli autori di pacchetti di utilizzare la funzionalità di riferimenti ad per applicare subset di assembly Framework diversi quando sono sarebbe altrimenti necessario per eseguire gli assembly duplicati in più `lib` cartelle.

Nota: al momento utilizzare nuget.exe pack per utilizzare questa funzionalità; Esplora pacchetti NuGet non supporta ancora il.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Aggiornare tutti i pulsante per consentire l'aggiornamento di tutti i pacchetti in una sola volta

Molti di voi conoscere il cmdlet PowerShell di "Pacchetto di aggiornamento" per aggiornare tutti i pacchetti; è ora un modo semplice per eseguire questa operazione tramite l'interfaccia utente.

Per provare questa funzionalità:

1. Creare una nuova applicazione MVC ASP.NET
1. Avviare la finestra di dialogo 'Gestisci pacchetti di NuGet'
1. Selezionare 'Updates'
1. Fare clic sul pulsante 'Aggiorna tutto'

![Aggiornare tutti i pulsante nella finestra di dialogo](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Supporto di riferimento di progetto migliorato per nuget.exe Pack

A questo punto i processi di comando di nuget.exe pack riferimento progetti con le regole seguenti:

1. Se il progetto di riferimento corrispondente `.nuspec` file, ad esempio, è presente un file denominato `proj1.nuspec` nella stessa cartella `proj1.csproj`, quindi questo progetto viene aggiunto come una dipendenza per il pacchetto, utilizzando l'id e versione sono leggervi il `.nuspec` file.
1. In caso contrario, i file del progetto di riferimento sono inclusi nel pacchetto. Quindi verranno elaborati i progetti a cui fa riferimento questo progetto utilizzando le regole di medesime in modo ricorsivo.
1. Tutte le DLL, `.pdb`, e `.exe` file vengono aggiunti.
1. Tutti gli altri file di contenuto vengono aggiunti.
1. Tutte le dipendenze vengono unite.

In questo modo un progetto di riferimento devono essere considerati una dipendenza, se è presente un `.nuspec` file, in caso contrario, diventa parte del pacchetto.

Ulteriori dettagli di seguito: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Aggiungere una proprietà 'La versione minima NuGet' per i pacchetti

Un nuovo attributo di metadati denominato 'minClientVersion' ora può indicare la versione minima del client NuGet necessaria per utilizzare un pacchetto.

Questa funzionalità consente l'autore del pacchetto per specificare che un pacchetto funzionerà solo dopo una particolare versione di NuGet. Come nuovi `.nuspec` dopo NuGet 2.5, sono state aggiunte funzionalità pacchetti saranno in grado di richiedere una versione minima di NuGet.

```xml
<metadata minClientVersion="2.6">
```

Se l'utente abbia NuGet 2.5 installato e un pacchetto è stato identificato come richiedere 2.6, segnali visivi verranno forniti all'utente che indica che il pacchetto non sarà installabile. L'utente verrà quindi essere guidata per l'aggiornamento della versione di NuGet.

Questo verrà migliorano l'esperienza esistente in cui iniziano i pacchetti da installare, ma prima dell'esito negativo che indica che è stata identificata una versione dello schema non riconosciuto.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Le dipendenze non è più inutilmente vengono aggiornate durante l'installazione del pacchetto

Prima di NuGet 2.5, durante l'installazione di un pacchetto che dipendono da un pacchetto già installato nel progetto, la dipendenza verranno aggiornata come parte della nuova installazione, anche se la versione esistente è soddisfatta la dipendenza.

A partire da NuGet 2.5, se una versione della dipendenza già viene soddisfatta, la dipendenza non verrà aggiornata durante le altre installazioni del pacchetto.

**Scenario:**

1. Il repository di origine contiene pacchetto B con la versione 1.0.0 e 1.0.2. Contiene inoltre il pacchetto che contiene una dipendenza da B A (> = 1.0.0).
1. Si supponga che il progetto corrente dispone già di versione del pacchetto B 1.0.0 installato. Ora si desidera installare a pacchetto.

**In NuGet 2.2 e versioni precedenti:**

* Quando si installa un pacchetto, NuGet verrà aggiornata automaticamente B alla versione 1.0.2, anche se la versione 1.0.0 di esistente già soddisfa il vincolo di versione di dipendenza, è > = 1.0.0.

**In NuGet 2.5 e versioni successive:**

* NuGet non verrà più aggiornato B, perché viene rilevato che la versione esistente 1.0.0 soddisfa il vincolo di versione della dipendenza.

Per ulteriori informazioni su questa modifica, leggere la sezione dettagliata [elemento di lavoro](http://nuget.codeplex.com/workitem/1681) nonché correlata [thread di discussione](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>NuGet.exe genera richieste http con livello di dettaglio massimo

Se si sta cercando di risolvere nuget.exe o semplicemente sapere quali richieste HTTP effettuate durante le operazioni di '-dettaglio dettagliata ' commutatore genera ora tutte le richieste HTTP effettuate.

![Output HTTP di nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>NuGet.exe push ora supporta origini UNC e cartella

Prima di NuGet 2.5, se si è tentato di eseguire 'nuget.exe push' a un'origine del pacchetto in base a un percorso UNC o una cartella locale, avrà esito negativo il push. Con la funzionalità di configurazione gerarchici aggiunti di recente, diventa comune per nuget.exe devono necessariamente avere come destinazione un'origine o sulla cartella UNC o una raccolta di NuGet basato su HTTP.

A partire da NuGet 2.5, se nuget.exe identifica un'origine o sulla cartella UNC, viene eseguita la copia del file di origine.

Funzionamento dopo il comando seguente:

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>NuGet.exe supporta i file di configurazione specificato in modo esplicito

i comandi di NuGet.exe che accedono a questo punto di configurazione (tutti ad eccezione di 'Mod' e 'pack') supportano un nuovo '-ConfigFile' opzione che impone un file di configurazione specifico da utilizzare al posto di file di configurazione predefinito % AppData%\nuget\Nuget.Config.

Esempio:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Supporto per i progetti nativi

Con NuGet 2.5, gli strumenti di NuGet sono ora disponibili per i progetti nativi in Visual Studio. È probabile che più pacchetti nativi utilizzerà la funzionalità di importazioni di MSBuild, creato da uno strumento di [CoApp progetto](http://coapp.org). Per altre informazioni, vedere [informazioni sullo strumento](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) nel sito Web coapp.org.

Il nome del framework di destinazione di "nativa" è stato introdotto per i pacchetti includere file \build \content e \tools quando il pacchetto viene installato in un progetto nativo.  Il \`lib' cartella non viene utilizzata per i progetti nativi.
