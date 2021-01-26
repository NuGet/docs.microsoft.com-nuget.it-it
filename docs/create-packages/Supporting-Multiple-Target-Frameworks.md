---
title: Multitargeting per i pacchetti NuGet
description: Descrizione dei vari metodi per selezionare come destinazione più versioni di .NET Framework da un singolo pacchetto NuGet.
author: JonDouglas
ms.author: jodou
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: e919b11670589900d9e588db33fd68b8df592ac2
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774564"
---
# <a name="support-multiple-net-versions"></a>Supporto di più versioni di .NET

Molte librerie hanno come destinazione una versione specifica di .NET Framework. Ad esempio, si potrebbe disporre di una versione della libreria specifica per UWP e di un'altra versione che sfrutta le funzionalità di .NET Framework 4.6. Per risolvere questo problema, NuGet supporta l'inserimento di più versioni della stessa libreria in un singolo pacchetto.

Questo articolo descrive il layout di un pacchetto NuGet, indipendentemente dalla modalità di compilazione del pacchetto o degli assembly (ovvero, il layout è lo stesso se si usano più file con *estensione csproj* non SDK e un file con *estensione NuSpec* personalizzato o un singolo file con estensione *csproj* con più destinazioni). Per un progetto di tipo SDK, le [destinazioni per pack](../reference/msbuild-targets.md) di NuGet conoscono il layout previsto per il pacchetto e automatizzano l'inserimento degli assembly nelle cartelle lib corrette e la creazione dei gruppi di dipendenze per ogni framework di destinazione (TFM). Per istruzioni dettagliate, vedere [Supportare più versioni di .NET Framework nel file di progetto](multiple-target-frameworks-project-file.md).

È necessario impostare manualmente il layout del pacchetto come descritto in questo articolo quando si usa il metodo della directory di lavoro basata sulle convenzioni descritto in [Creazione di un pacchetto](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). Per un progetto di tipo SDK, è consigliabile usare il metodo automatico, ma è anche possibile scegliere di impostare manualmente il layout del pacchetto come descritto in questo articolo.

## <a name="framework-version-folder-structure"></a>Struttura di cartelle della versione del framework

Quando si compila un pacchetto che contiene solo una versione di una libreria o che ha come destinazione più framework, si creano sempre sottocartelle in `lib` usando nomi di framework diversi con distinzione tra maiuscole e minuscole in base alla convenzione seguente:

```
lib\{framework name}[{version}]
```

Per un elenco completo dei nomi supportati, vedere le [informazioni di riferimento sui framework di destinazione](../reference/target-frameworks.md#supported-frameworks).

Non si deve mai disporre di una versione della libreria che non sia specifica di un framework e che sia inserita direttamente nella cartella `lib` radice (questa funzionalità è supportata solo con `packages.config`). Così facendo, si renderebbe la libreria compatibile con qualsiasi framework di destinazione consentendone l'installazione in qualunque posizione, con probabili errori di runtime imprevisti. L'aggiunta di assembly nella cartella radice (ad esempio `lib\abc.dll`) o nelle sottocartelle (ad esempio `lib\abc\abc.dll`) è deprecata e viene ignorata quando si usa il formato PackagesReference.

Ad esempio, la struttura di cartelle seguente supporta quattro versioni di un assembly che sono specifiche del framework:

```
\lib
    \net46
        \MyAssembly.dll
    \net461
        \MyAssembly.dll
    \uap
        \MyAssembly.dll
    \netcore
        \MyAssembly.dll
```

Per includere facilmente tutti i file durante la compilazione del pacchetto, usare un carattere jolly `**` ricorsivo nella sezione `<files>` di `.nuspec`:

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Cartelle specifiche dell'architettura

Se si dispone di assembly specifici dell'architettura, vale a dire assembly distinti che hanno come destinazione ARM, x86 e x64, è necessario inserirli in una cartella denominata `runtimes` all'interno di sottocartelle denominate `{platform}-{architecture}\lib\{framework}` o `{platform}-{architecture}\native`. Ad esempio, la struttura di cartelle seguente potrebbe contenere sia DLL native che gestite che hanno come destinazione Windows 10 e il framework `uap10.0`:

```
\runtimes
    \win10-arm
        \native
        \lib\uap10.0
    \win10-x86
        \native
        \lib\uap10.0
    \win10-x64
        \native
        \lib\uap10.0
```

Poiché questi assembly saranno disponibili solo in fase di esecuzione, per fornire l'assembly corrispondente anche in fase di compilazione, l'assembly `AnyCPU` deve essere presente nella cartella `/ref/{tfm}`. 

Ricordare che, poiché NuGet seleziona sempre questi asset di compilazione o di runtime da una sola cartella, se sono presenti asset compatibili in `/ref`, `/lib` non verrà considerata per l'aggiunta di assembly in fase di compilazione. Analogamente, se sono presenti alcune risorse compatibili da, `/runtimes` anche `/lib` per il runtime verrà ignorato.

Vedere [Creare pacchetti UWP](../guides/create-uwp-packages.md) per un esempio di riferimento a questi file nel manifesto `.nuspec`.

Vedere anche [Packing a Windows store app component with NuGet](/archive/blogs/mim/packaging-a-windows-store-apps-component-with-nuget-part-2) (Creazione di un pacchetto di un componente app di Windows Store con NuGet)

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Corrispondenza tra le versioni di assembly e il framework di destinazione in un progetto

Quando NuGet installa un pacchetto che dispone di più versioni di assembly, tenta di associare il nome del framework dell'assembly con il framework di destinazione del progetto.

Se non viene trovata una corrispondenza, NuGet copia l'assembly per la versione più alta inferiore o uguale al framework di destinazione del progetto, se disponibile. Se non viene trovato un assembly compatibile, NuGet restituisce un messaggio di errore appropriato.

Si consideri ad esempio la struttura di cartelle seguente in un pacchetto:

```
\lib
    \net45
        \MyAssembly.dll
    \net461
        \MyAssembly.dll
```

Quando si installa questo pacchetto in un progetto che ha come destinazione .NET Framework 4.6, NuGet installa l'assembly nella cartella `net45`, trattandosi della versione più alta disponibile inferiore o uguale alla versione 4.6.

Se il progetto ha come destinazione .NET Framework 4.6.1, invece, NuGet installa l'assembly nella cartella `net461`.

Se il progetto ha come destinazione .NET Framework 4.0 e versioni precedenti, NuGet genera un messaggio di errore appropriato per non avere trovato un assembly compatibile.

## <a name="grouping-assemblies-by-framework-version"></a>Raggruppamento di assembly per versione del framework

NuGet copia gli assembly solo da una singola cartella di libreria nel pacchetto. Si supponga ad esempio che un pacchetto abbia la struttura di cartelle seguente:

```
\lib
    \net40
        \MyAssembly.dll (v1.0)
        \MyAssembly.Core.dll (v1.0)
    \net45
        \MyAssembly.dll (v2.0)
```

Quando il pacchetto viene installato in un progetto che ha come destinazione .NET Framework 4.5, `MyAssembly.dll` (v2.0) è l'unico assembly installato. `MyAssembly.Core.dll` (v1.0) non è installato perché non è elencato nella cartella `net45`. NuGet ha questo comportamento perché `MyAssembly.Core.dll` potrebbe essere stato unito nella versione 2.0 di `MyAssembly.dll`.

Se si vuole che `MyAssembly.Core.dll` sia installato per .NET Framework 4.5, inserire una copia nella cartella `net45`.

## <a name="grouping-assemblies-by-framework-profile"></a>Raggruppamento di assembly per profilo del framework

NuGet supporta anche la selezione di uno specifico profilo del framework come destinazione accodando un trattino e il nome del profilo alla fine della cartella.

\{nome del Framework lib}-{profile}

I profili supportati sono i seguenti:

- `client`: Client Profile
- `full`: Full Profile
- `wp`: Windows Phone
- `cf`: Compact Framework

## <a name="declaring-dependencies-advanced"></a>Dichiarazione delle dipendenze (scenari avanzati)

Quando si crea un pacchetto per il file di progetto, NuGet tenta di generare automaticamente le dipendenze dal progetto. Le informazioni contenute in questa sezione sull'uso di un file con estensione *nuspec* per dichiarare le dipendenze sono in genere necessarie solo per gli scenari avanzati.

*(Versione 2.0 +)* È possibile dichiarare le dipendenze del pacchetto nel file *nuspec* corrispondente al framework di destinazione del progetto di destinazione usando elementi `<group>` all'interno dell'elemento `<dependencies>`. Per altre informazioni, vedere [Elemento dependencies](../reference/nuspec.md#dependencies-element).

Ogni gruppo ha un attributo denominato `targetFramework` e contiene zero o più elementi `<dependency>`. Tali dipendenze vengono installate insieme quando il framework di destinazione è compatibile con il profilo di framework del progetto. Vedere [Framework di destinazione](../reference/target-frameworks.md) per gli identificatori di framework esatti.

Si consiglia di usare un gruppo per ogni moniker framework di destinazione (TFM) per i file nelle cartelle *lib/* e *ref/*.

L'esempio seguente mostra variazioni diverse dell'elemento `<group>`:

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a>Determinazione della destinazione NuGet da usare

Quando si inseriscono in un pacchetto librerie che hanno come destinazione la libreria di classi portabile, può essere difficile determinare quale destinazione NuGet usare nei nomi delle cartelle e nel file `.nuspec`, in particolare se la destinazione è solo un subset della libreria di classi portabile. Le risorse esterne seguenti possono essere di aiuto:

- [Framework profiles in .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (Profili di framework in .NET) (stephencleary.com)
- [Profili della libreria di classi portabile](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): tabella che enumera i profili della libreria di classi portabile e le destinazioni NuGet equivalenti
- [Strumento per i profili della libreria di classi portabile](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): strumento da riga di comando per determinare i profili della libreria di classi portabile disponibili nel sistema

## <a name="content-files-and-powershell-scripts"></a>File di contenuto e script PowerShell

> [!Warning]
> I file di contenuto modificabili e l'esecuzione degli script sono disponibili solo con il formato `packages.config`. Sono deprecati per tutti gli altri formati e non dovrebbero essere usati per i nuovi pacchetti.

Con `packages.config`, i file di contenuto e gli script PowerShell possono essere raggruppati per framework di destinazione usando la stessa convenzione di cartelle all'interno delle cartelle `content` e `tools`. Ad esempio:

```
\content
    \net46
        \MyContent.txt
    \net461
        \MyContent461.txt
    \uap
        \MyUWPContent.html
    \netcore
\tools
    init.ps1
    \net46
        install.ps1
        uninstall.ps1
    \uap
        install.ps1
        uninstall.ps1
```

Se una cartella framework viene lasciata vuota, NuGet non aggiunge riferimenti ad assembly o file di contenuto né esegue script PowerShell per tale framework.

> [!Note]
> Poiché `init.ps1` viene eseguito a livello di soluzione e indipendentemente dal progetto, deve essere inserito direttamente sotto la cartella `tools`. Viene ignorato se inserito in una cartella framework.