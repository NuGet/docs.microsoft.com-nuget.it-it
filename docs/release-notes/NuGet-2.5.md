---
title: Note sulla versione 2.5 di NuGet
description: Note sulla versione per NuGet 2.5, inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 29d0b33714a574281680e110b967269699afbaf1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550483"
---
# <a name="nuget-25-release-notes"></a>Note sulla versione 2.5 di NuGet

[Note sulla versione di NuGet 2.2.1](../release-notes/nuget-2.2.1.md) | [note sulla versione per NuGet 2.6](../release-notes/nuget-2.6.md)

NuGet 2.5 è stato rilasciato il 25 aprile 2013. Questa versione è stata così grande, è stato ritenuto obbligati a ignorare le versioni 2.3 e 2.4. Fino a oggi questa è la versione più grande per NuGet, ho avuto con failover [elementi di lavoro 160](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.5&status=all) nella versione.

## <a name="acknowledgements"></a>Riconoscimenti

Vorremmo ringraziare i collaboratori esterni seguenti per i contributi significativi a NuGet 2.5:

1. [Daniel Plaisted](https://www.codeplex.com/site/users/view/dsplaisted) ([@dsplaisted](https://twitter.com/dsplaisted))
    - [#2847](https://nuget.codeplex.com/workitem/2847) -aggiungere MonoAndroid MonoTouch e MonoMac per l'elenco degli identificatori di framework di destinazione noti.
2. [Andres g. Aragoneses](https://www.codeplex.com/site/users/view/knocte) ([@knocte](https://twitter.com/knocte))
    - [#2865](https://nuget.codeplex.com/workitem/2865) -correggere l'ortografia del `NuGet.targets` per un sistema operativo distinzione maiuscole/minuscole
3. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - Verificare la soluzione di compilazione in Mono.
4. [Andrew Theken](https://www.codeplex.com/site/users/view/atheken) ([@atheken](https://twitter.com/atheken))
    - Correggere gli unit test non superati in Mono.
5. [Dagenais Olivier](https://www.codeplex.com/site/users/view/OliIsCool) ([@OliIsCool](https://twitter.com/oliiscool))
    - [#2920](https://nuget.codeplex.com/workitem/2920) -comando pack nuget.exe non propaga le proprietà di MSBuild
6. [Miroslav Bajtos](https://www.codeplex.com/site/users/view/MiroslavBajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#1511](https://nuget.codeplex.com/workitem/1511) - XML modificato la gestione del codice per mantenere la formattazione.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - Aggiunte le parole riconosciute al dizionario personalizzato per consentire di build. cmd abbia esito positivo.
8. [Bruno Roggeri](https://www.codeplex.com/site/users/view/broggeri)
    - Correggere gli unit test durante l'esecuzione in Visual Studio localizzato.
9. [Evans Gareth](https://www.codeplex.com/site/users/view/garethevans)
    - Interfaccia estratto dal PackageService
10. [Maxime Brugidou](https://www.codeplex.com/site/users/view/brugidou) ([@brugidou](https://twitter.com/brugidou))
     - [#936](https://nuget.codeplex.com/workitem/936) -gestire le dipendenze del progetto durante la creazione di un pacchetto
11. [A Xavier Decoster](https://www.codeplex.com/site/users/view/XavierDecoster) ([@XavierDecoster](https://twitter.com/xavierdecoster))
     - [#2991](https://nuget.codeplex.com/workitem/2991), [#3164](https://nuget.codeplex.com/workitem/3164) -supporto Password come testo non crittografato quando si archiviano le credenziali dell'origine del pacchetto nel file nuget.cofig
12. [James Manning](http://www.codeplex.com/site/users/view/jmanning) ([@manningj](https://twitter.com/manningj))
     - [#3190](http://nuget.codeplex.com/workitem/3190), [#3191](http://nuget.codeplex.com/workitem/3191) -descrizione della Guida correggere Get-Package

Grazie anche per le persone indicate di seguito per individuare i bug con NuGet 2.5 Beta o RC che sono state approvate e risolto prima della versione finale:

1. [Tony Wall](https://www.codeplex.com/site/users/view/CodeChief) ([@CodeChief](https://twitter.com/codechief))
    - [#3200](https://nuget.codeplex.com/workitem/3200) MSTest interrotto con più di recente NuGet 2.4 e 2.5 compilazioni:

## <a name="notable-features-in-the-release"></a>Funzionalità di rilievo nella versione

### <a name="allow-users-to-overwrite-content-files-that-already-exist"></a>Consentire agli utenti di sovrascrivere i file di contenuto già esistenti

Una delle funzionalità più richieste di tutto il tempo è stata la possibilità di sovrascrivere i file di contenuto che già esistono nel disco quando incluso in un pacchetto NuGet. A partire da NuGet 2.5, tali conflitti vengono identificati e viene richiesto di sovrascrivere i file, mentre in precedenza questi file sono stati sempre ignorati.

![Sovrascrivere i file di contenuto](./media/NuGet-2.5/overwrite-file.png)

'nuget.exe update' e 'Install-Package' a questo punto entrambi hanno la possibilità di '-FileConflictAction' per impostare alcuni valori predefiniti per gli scenari della riga di comando.

Impostare un'azione predefinita quando un file da un pacchetto esiste già nel progetto di destinazione. Impostare su 'Sovrascrivi' per sovrascrivere sempre i file. Impostare su 'Ignore' per ignorare i file. Se non specificato, verrà richiesto per ogni file in conflitto.

### <a name="automatic-import-of-msbuild-targets-and-props-files"></a>Importazione automatica dei file di destinazioni e proprietà di MSBuild

Una nuova cartella convenzionale è stata creata il primo livello del pacchetto NuGet.  Allo stesso `\lib`, `\content`, e `\tools`, è ora possibile includere un `\build` cartella nel pacchetto.  In questa cartella, è possibile inserire due file con nomi fissi `{packageid}.targets` o `{packageid}.props`. Questi due file possono essere direttamente sotto `build` o nelle cartelle specifiche del framework, proprio come le altre cartelle. La regola per scegliere la cartella di .NET framework corrispondente con mapping più appropriato è esattamente le stesse di quelle.

Quando NuGet installa un pacchetto con file di \build, aggiungerà un MSBuild `<Import>` nel file di progetto che punta all'elemento di `.targets` e `.props` file. Il `.props` file viene aggiunto all'inizio, mentre il `.targets` file viene aggiunto alla fine.

### <a name="specify-different-references-per-platform-using-references-element"></a>Specificare i riferimenti diversi per ogni piattaforma usando `<References/>` elemento

Prima di 2.5, in `.nuspec` file utente può specificare solo i file di riferimento, da aggiungere per tutti i framework. A questo punto con questa nuova funzionalità di 2.5, è possibile creare l'utente di `<reference/>` (elemento) per ogni piattaforma supportata, ad esempio:

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

Di seguito è riportato il flusso per la modalità NuGet aggiunge riferimenti a progetti basati sul `.nuspec` file:

1. Trovare il `lib` cartella in cui è appropriato per il framework di destinazione e ottiene l'elenco di assembly da tale cartella
1. Separatamente, trovare il gruppo di riferimenti che è appropriato per il framework di destinazione e ottenere l'elenco degli assembly da tale gruppo. Gruppo di riferimento senza framework di destinazione specificato è il gruppo di fallback.
1. Trovare l'intersezione dei due elenchi e utilizzarlo come i riferimenti da aggiungere

Questa nuova funzionalità consentirà agli autori di usare la funzionalità di riferimenti applicare subset di assembly per diversi Framework sarebbe altrimenti necessario eseguire gli assembly duplicati in più `lib` cartelle.

Nota: è necessario attualmente usare pack nuget.exe per usare questa funzionalità; NuGet Package Explorer non supporta ancora lo.

### <a name="update-all-button-to-allow-updating-all-packages-at-once"></a>Aggiornare tutti i pulsante per consentire l'aggiornamento di tutti i pacchetti in una sola volta

Molti di voi conoscono il cmdlet di PowerShell "Update-Package" affinché aggiornare tutti i pacchetti; ora vi è un modo semplice per eseguire questa operazione tramite l'interfaccia utente anche.

Per provare questa funzionalità:

1. Creare una nuova applicazione MVC ASP.NET
1. Avviare la finestra di dialogo 'Gestisci pacchetti NuGet'
1. Selezionare "Aggiornamenti"
1. Fare clic sul pulsante "Aggiorna tutto"

![Aggiornare tutti i pulsante nella finestra di dialogo](./media/NuGet-2.5/update-all.png)

### <a name="improved-project-reference-support-for-nugetexe-pack"></a>Supporto di riferimento di progetto migliorato per nuget.exe Pack

Ora i processi di comando pack nuget.exe fanno riferimento i progetti con le regole seguenti:

1. Se il progetto con riferimenti corrispondente `.nuspec` file, ad esempio, è presente un file denominato `proj1.nuspec` nella stessa cartella `proj1.csproj`, quindi questo progetto viene aggiunto come dipendenza al pacchetto, utilizzando l'id e versione leggervi il `.nuspec` file.
1. In caso contrario, i file del progetto di riferimento sono contenuti nel pacchetto. Quindi verranno elaborati progetti farvi riferimento questo progetto utilizzando le regole di medesime in modo ricorsivo.
1. Tutte le DLL, `.pdb`, e `.exe` vengono aggiunti file.
1. Tutti gli altri file di contenuto vengono aggiunti.
1. Tutte le dipendenze vengono unite.

In questo modo un progetto di riferimento essere considerato come una dipendenza se è presente un `.nuspec` file, in caso contrario, questa diventa parte del pacchetto.

Per informazioni dettagliate: [http://nuget.codeplex.com/workitem/936](http://nuget.codeplex.com/workitem/936)

### <a name="add-a-minimum-nuget-version-property-to-packages"></a>Aggiungere una proprietà 'Versione di NuGet minima' ai pacchetti

Un nuovo attributo di metadati denominato 'minClientVersion' a questo punto può indicare la versione client NuGet minima richiesta per utilizzare un pacchetto.

Questa funzionalità consente di autore del pacchetto per specificare che un pacchetto funzionerà solo dopo una determinata versione di NuGet. Come nuovi `.nuspec` funzionalità vengono aggiunti dopo NuGet 2.5, i pacchetti saranno in grado di richiedere una versione minima di NuGet.

```xml
<metadata minClientVersion="2.6">
```

Se l'utente ha installato NuGet 2.5 e un pacchetto è identificato in modo che richiedano 2.6, segnali visivi verranno assegnati all'utente che indica che il pacchetto non verrà installabile. L'utente verrà quindi informazioni dettagliata per l'aggiornamento della versione di NuGet.

Ciò migliorerà al momento l'esperienza esistente in cui iniziano a pacchetti da installare, ma l'esito negativo che indica che una versione dello schema non riconosciuto è stata identificata.

### <a name="dependencies-are-no-longer-unnecessarily-updated-during-package-installation"></a>Le dipendenze siano aggiornate non è più inutilmente durante l'installazione del pacchetto

Prima di NuGet 2.5, durante l'installazione di un pacchetto che dipendono da un pacchetto già installato nel progetto, la dipendenza verrebbe aggiornata come parte della nuova installazione, anche se la versione esistente soddisfa la dipendenza.

A partire da NuGet 2.5, se una versione della dipendenza è già soddisfatta, la dipendenza non verrà aggiornata durante le altre installazioni del pacchetto.

**Scenario:**

1. Il repository di origine contiene pacchetto B con la versione 1.0.0 e versione 1.0.2. Include inoltre il pacchetto a, che presenta una dipendenza da B (> = 1.0.0).
1. Si supponga che il progetto corrente ha già la versione del pacchetto B 1.0.0 installato. A questo punto si desidera installare pacchetti r.

**In NuGet versione 2.2 e precedenti:**

* Quando si installa un pacchetto, NuGet verrà aggiornato automaticamente B alla versione 1.0.2, anche se la versione 1.0.0 esistente già soddisfa il vincolo di versione delle dipendenze, che è > = 1.0.0.

**In NuGet 2.5 e versioni successive:**

* NuGet non verrà più aggiornato B, perché rileverà che la versione 1.0.0 esistente soddisfa il vincolo di versione delle dipendenze.

Per altre informazioni su questa modifica, leggere la pagina dettagliata [elemento di lavoro](http://nuget.codeplex.com/workitem/1681) , nonché i relativi [thread di discussione](http://nuget.codeplex.com/discussions/436712).

### <a name="nugetexe-outputs-http-requests-with-detailed-verbosity"></a>NuGet.exe restituisce come output le richieste http con livello di dettaglio massimo

Se sta cercando di risolvere nuget.exe o semplicemente curioso di scoprire quali le richieste HTTP vengono effettuate durante le operazioni di '-livello di dettaglio dettagliata ' commutatore ora restituirà tutte le richieste HTTP effettuate.

![Output HTTP dal nuget.exe](./media/NuGet-2.5/verbosity.png)

### <a name="nugetexe-push-now-supports-unc-and-folder-sources"></a>push NuGet.exe supporta ora origini UNC e cartella

Prima di NuGet 2.5, se si è provato a eseguire 'nuget.exe push' per un'origine pacchetto basata su un percorso UNC o una cartella locale, avrà esito negativo dei push. Con la funzionalità di configuration gerarchico aggiunto di recente, diventa più comune per nuget.exe necessario utilizzare un'origine o la cartella UNC o una raccolta di NuGet basato su HTTP.

A partire da NuGet 2.5, se nuget.exe identifica un'origine o la cartella UNC, viene eseguita la copia del file di origine.

Funzionerà ora il comando seguente:

```
nuget push -source \\mycompany\repo\ mypackage.1.0.0.nupkg
```

### <a name="nugetexe-supports-explicitly-specified-config-files"></a>NuGet.exe supporta i file di configurazione specificato in modo esplicito

i comandi NuGet.exe che accedono a configurazione (tutti ad eccezione di 'pack' e 'Mod') ora supportano un nuovo '-ConfigFile' opzione che impone un file di configurazione specifico da usare al posto di file di configurazione predefinito nel percorso % AppData%\nuget\Nuget.Config.

Esempio:

```
nuget sources add -name test -source http://test -ConfigFile C:\test\.nuget\Nuget.Config
```

### <a name="support-for-native-projects"></a>Supporto per i progetti nativi

Con NuGet 2.5, gli strumenti di NuGet sono ora disponibili per i progetti nativi in Visual Studio. Si prevede che più pacchetti nativi utilizzerà la funzionalità di importazioni MSBuild in precedenza, usando uno strumento creato dal [CoApp progetto](http://coapp.org). Per altre informazioni, leggere [le informazioni sullo strumento](http://coapp.org/news/2013-03-27-The-Long-Awaited-post.html) sul sito Web coapp.org.

Il nome del framework di destinazione di "nativa" è stato introdotto per i pacchetti da includere i file di \build, \content e \tools quando il pacchetto viene installato in un progetto nativo.  Il \`lib' cartella non viene utilizzata per i progetti nativi.
