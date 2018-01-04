---
title: Riferimenti ai framework di destinazione per NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/11/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 4343a48e-f6df-4a44-9d66-4616c3caacf5
description: I riferimenti ai framework di destinazione NuGet consentono di identificare e isolare i componenti dipendenti dai framework di un pacchetto.
keywords: Destinazione dei pacchetti NuGet, destinazioni .NET Framework, versioni di .NET Framework
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4d1d2e6850f22306d715b1c2071ee45b0eb050dc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="target-frameworks"></a>Framework di destinazione

NuGet usa I riferimenti ai framework di destinazione in svariate posizioni per identificare e isolare i componenti dipendenti dai framework di un pacchetto:

- [Manifesto .nuspec](../schema/nuspec.md): un pacchetto può indicare i pacchetti distinti da includere in un progetto a seconda del framework di destinazione del progetto.
- [Nome delle cartella .nupkg](../create-packages/creating-a-package.md#from-a-convention-based-working-directory): le cartelle all'interno della cartella `lib` di un pacchetto possono essere denominate in base al framework di destinazione e ognuna contiene le DLL e altro contenuto appropriati per tale framework.
- [packages.config](../Schema/packages-config.md): l'attributo `targetframework` di una dipendenza specifica la variante di un pacchetto da installare.
- [project.json](../Schema/project-json.md): il nodo `frameworks` specifica le versioni del framework per le quali può essere compilato il progetto.

> [!Note]
> Il codice sorgente del client NuGet che consente di calcolare le tabelle riportate di seguito è disponibile nelle posizioni seguenti:
> -  Nomi dei framework supportati: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> -  Precedenza e mapping dei framework: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>Framework supportati

In genere si fa riferimento a un framework tramite un breve moniker del framework di destinazione o TFM (Target Framework Moniker). In .NET Standard questo viene inoltre generalizzato in *TxM* per consentire un unico riferimento a più framework.

I client NuGet supportano i framework nella tabella seguente. Gli equivalenti sono visualizzati tra parentesi quadre []. Si noti che alcuni strumenti, ad esempio `dotnet`, potrebbero usare varianti dei moniker TFM canonici in alcuni file. Ad esempio, `dotnet pack` usa `.NETCoreApp2.0` in un file `.nuspec` invece di `netcoreapp2.0`. I vari strumenti client NuGet gestiscono queste variazioni correttamente, ma è consigliabile usare sempre i TFM canonici quando si modificano direttamente i file.

| Nome           | Abbreviazione | TFM/TxM |
| -------------  | ------------ | --------- |
|.NET Framework  | net          | net11     |
|                |              | net20     |
|                |              | net35     |
|                |              | net40     |
|                |              | net403    |
|                |              | net45      |
|                |              | net451     |
|                |              | net452     |
|                |              | net46      |
|                |              | net461     |
|                |              | net462     |
|Windows Store   | netcore      | netcore [netcore45] |
|                |              | netcore45 [win, win8] |
|                |              | netcore451 [win81] |
|                |              | netcore50 |
|.NET MicroFramework | netmf    | netmf |
|Windows         | win          | win [win8, netcore45] |
| | | win8 [netcore45, win] |
| | | win81 [netcore451] |
| | | win10 (non supportato dalla piattaforma Windows 10) |
Silverlight | sl | sl4 |
| | | sl5 |
Windows Phone (SL) | wp | wp [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
Piattaforma UWP (Universal Windows Platform) | uap | uap [uap10.0] |
| | | uap10.0 |
.NET Standard | netstandard | netstandard1.0 |
| | | netstandard1.1 |
| | | netstandard1.2 |
| | | netstandard1.3 |
| | | netstandard1.4 |
| | | netstandard1.5 |
| | | netstandard1.6 |
| | | netstandard2.0 |
App .NET Core | netcoreapp | netcoreapp1.0 |
| | | netcoreapp1.1 |
| | | netcoreapp2.0 |
Tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>Framework deprecati
I framework seguenti sono deprecati. I pacchetti che hanno come destinazione questi framework devono essere migrati alle sostituzioni indicate.

| Framework deprecato | Sostituzione
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| dnx |
| dnx45 |
| dnx451 |
| dnx452 |
| dotnet | netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| winrt | win |

## <a name="precedence"></a>Precedenza

Alcuni framework sono correlati e compatibili tra loro, ma non necessariamente equivalenti:

| Framework | È possibile usare: |
| --- | --- |
| uap (piattaforma UWP) | win81 |
| | wpa81 |
| | netcore50 |
| win (Microsoft Store) | winrt |
| | | winrt45 |

## <a name="net-platform-standard"></a>NET Platform Standard

[.NET Platform Standard](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md) semplifica i riferimenti tra framework compatibili con il codice binario, consentendo a un framework di destinazione singolo di fare riferimento a una combinazione di altri framework. (Per informazioni generali, vedere [Nozioni di base su .NET](https://docs.microsoft.com/dotnet/articles/standard/index).)

Lo [strumento NuGet Get Nearest Framework](https://aka.ms/s2m3th) simula la logica usata da NuGet per la selezione di un framework da molte risorse di framework disponibili in un pacchetto sulla base del framework di progetto.

La serie `dotnet` di moniker deve essere usata in NuGet 3.3 e versioni precedenti, mentre la sintassi per i moniker `netstandard` deve essere usata nella versione 3.4 e versioni successive.

## <a name="portable-class-libraries"></a>Librerie di classi portabili

> [!Warning]
> **Le librerie di classi portabili (PCL) non sono consigliate**. Anche se sono supportate, gli autori di pacchetti devono supportare netstandard. .NET Platform Standard è un'evoluzione delle librerie di classi portabili e rappresenta la portabilità binaria su più piattaforme tramite un singolo moniker non associato a un valore statico, come i moniker *portable-a+b+c*.

Per definire un framework di destinazione che fa riferimento a più framework di destinazione figlio, la parola chiave `portable` viene usata come prefisso per l'elenco dei framework a cui si fa riferimento. Evitare di includere artificialmente framework aggiuntivi non usati direttamente per la compilazione, perché ciò può portare a effetti collaterali imprevisti in tali framework.

I framework aggiuntivi definiti da terze parti garantiscono la compatibilità con altri ambienti accessibili in questo modo. Esistono, inoltre, numeri di profilo abbreviati per fare riferimento a queste combinazioni di framework correlati come `Profile#`, ma non è consigliabile usare questi numeri, in quanto risulta ridotta la leggibilità delle cartelle e di `.nuspec`.

| N. di profilo | Framework | Nome completo | .NET Standard |
 --- | --- | --- | ---
 Profile2 | .NETFramework 4.0 | portable-net40+win8+sl4+wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | WindowsPhone 7.0|
 Profile3 | .NETFramework 4.0 | portable-net40+sl4
 | | Silverlight 4.0 |
 Profile4 | .NETFramework 4.5 | portable-net45+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile5 | .NETFramework 4.0 | portable-net40+win8
 | | Windows 8.0 |
 Profile6 | .NETFramework 4.0.3 | portable-net403+win8
 | | Windows 8.0 |
 Profile7 | .NETFramework 4.5 | portable-net45+win8 | netstandard1.1
 | | Windows 8.0 |
 Profile14 | .NETFramework 4.0 | portable-net40+sl5
 | | Silverlight 5.0 |
 Profile18 | .NETFramework 4.0.3 | portable-net403+sl4
 | | Silverlight 4.0 |
 Profile19 | .NETFramework 4.0.3 | portable-net403+sl5
 | | Silverlight 5.0 |
 Profile23 | .NETFramework 4.5 | portable-net45+sl4
 | | Silverlight 4.0 |
 Profile24 | .NETFramework 4.5 | portable-net45+sl5
 | | Silverlight 5.0 |
 Profile31 | Windows 8,1 | portable-win81+wp81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 Profile32 | Windows 8,1 | portable-win81+wpa81 | netstandard1.2
 | | WindowsPhone 8.1 (UWP) |
 Profile36 | .NETFramework 4.0 | portable-net40+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile37 | .NETFramework 4.0 | portable-net40+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile41 | .NETFramework 4.0.3 | portable-net403+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile42 | .NETFramework 4.0.3 | portable-net403+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile44 | .NETFramework 4.5.1 | portable-net451+win81 | netstandard1.2
 | | Windows 8,1 |
 Profile46 | .NETFramework 4.5 | portable-net45+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile47 | .NETFramework 4.5 | portable-net45+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile49 | .NETFramework 4.5 | portable-net45+wp8 | netstandard1.0
 | | WindowsPhone 8.0 (SL) |
 Profile78 | .NETFramework 4.5 | portable-net45+win8+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile84 | WindowsPhone 8.1 | portable-wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (UWP) |
 Profile88 | .NETFramework 4.0 | portable-net40+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile92 | .NETFramework 4.0 | portable-net40+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile95 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile96 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile102 | .NETFramework 4.0.3 | portable-net403+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile104 | .NETFramework 4.5 | portable-net45+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile111 | .NETFramework 4.5 | portable-net45+win8+wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile136 | .NETFramework 4.0 | portable-net40+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile143 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile147 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile151 | NETFramework 4.5.1 | portable-net451+win81+wpa81 | netstandard1.2
 | | Windows 8,1 |
 | | WindowsPhone 8.1 (UWP) |
 Profile154 | .NETFramework 4.5 | portable-net45+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile157 | Windows 8,1 | portable-win81+wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 | | WindowsPhone 8.1 (UWP) |
 Profile158 | .NETFramework 4.5 | portable-net45+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile225 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile240 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile255 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile259 | .NETFramework 4.5 | portable-net45+win8+wpa81+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile328 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile336 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile344 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |

Inoltre, i pacchetti NuGet destinati a Xamarin possono usare framework aggiuntivi definiti da Xamarin. Vedere [Manually Creating NuGet Packages for Xamarin](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/) (Creazione manuale di pacchetti NuGet per Xamarin).

| Nome | Descrizione | .NET Standard |
| --- | --- | ---
| monoandroid | Supporto di Mono per sistema operativo Android | netstandard1.4 |
| monotouch | Supporto di Mono per iOS | netstandard1.4 |
| monomac | Supporto di Mono per OSX | netstandard1.4 |
| xamarinios | Supporto di Xamarin per iOS | netstandard1.4 |
| xamarinmac | Supporto di Xamarin per Mac | netstandard1.4 |
| xamarinpsthree | Supporto di Xamarin su Playstation 3 | netstandard1.4 |
| xamarinpsfour | Supporto di Xamarin su Playstation 4 | netstandard1.4 |
| xamarinpsvita | Supporto di Xamarin su PS Vita | netstandard1.4 |
| xamarinwatchos | Xamarin per Watch OS | netstandard1.4 |
| xamarintvos | Xamarin per tvOS | netstandard1.4 |
| xamarinxboxthreesixty | Xamarin per XBox 360 | netstandard1.4 |
| xamarinxboxone | Xamarin per XBox One | netstandard1.4 |

> [!Note]
> Stephen Cleary ha creato uno strumento che elenca le librerie di classi portabili supportate, disponibile nel suo post [Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (Profili di framework in .NET).
