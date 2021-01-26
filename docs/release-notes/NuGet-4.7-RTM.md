---
title: Note sulla versione per NuGet 4.7 RTM
description: Note sulla versione per NuGet 4.7.0 incluse informazioni su problemi noti, correzioni di bug e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 143781cf0a95c6a156d4afcd83ad277f3e227711
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780155"
---
# <a name="nuget-47-release-notes"></a>Note sulla versione per NuGet 4.7

[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) include [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).

## <a name="summary-whats-new-in-470"></a>Riepilogo: novità di 4.7.0

* Le funzionalità di firma dei pacchetti sono state estese per abilitare i [pacchetti firmati da repository](https://github.com/NuGet/Home/wiki/Repository-Signatures)

* Con Visual Studio versione 15.7, è stata introdotta la possibilità di [eseguire la migrazione di progetti esistenti che usano il formato packages.config per usare invece PackageReference](../consume-packages/migrate-packages-config-to-package-reference.md).

## <a name="summary-whats-new-in-472"></a>Riepilogo: novità di 4.7.2

* Correzione della sicurezza: le autorizzazioni per i file creati all'interno di ~/.NuGet sono troppo aperte [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-473"></a>Riepilogo: novità di 4.7.3

* Correzione della sicurezza: i file all'interno di transitiva possono avere un percorso relativo sopra la directory NUPKG [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Problemi noti

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>L'opzione `Migrate packages.config to PackageReference...` non è disponibile nel menu di scelta rapida

#### <a name="issue"></a>Problema

Alla prima apertura di un progetto, NuGet potrebbe non essere inizializzato fino all'esecuzione di un'operazione NuGet. Per questo motivo, l'opzione di migrazione non viene visualizzata nel menu di scelta rapida per `packages.config` o `References`.

#### <a name="workaround"></a>Soluzione alternativa

Eseguire una delle azioni NuGet seguenti:
* Aprire l'interfaccia utente di Gestione pacchetti - fare clic con il pulsante destro del mouse su `References` e scegliere `Manage NuGet Packages...`
* Aprire la console di Gestione pacchetti - Da `Tools > NuGet Package Manager` selezionare `Package Manager Console`
* Eseguire un ripristino NuGet - Fare clic con il pulsante destro del mouse sul nodo della soluzione in Esplora soluzioni e scegliere `Restore NuGet Packages`
* Compilare il progetto, ovvero un altro modo per attivare un ripristino NuGet

A questo punto, l'opzione di migrazione dovrebbe essere visibile. Si noti che questa opzione non è supportata e non verrà visualizzata per i tipi di progetto ASP.NET e C++.

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemi relativi a .NET 2.0 Standard con .NET Framework e NuGet

.NET Standard e i relativi strumenti sono stati progettati in modo che i progetti destinati a .NET Framework 4.6.1 possano utilizzare pacchetti e progetti NuGet destinati a .NET Standard 2.0 o versioni precedenti. [Questo documento](https://github.com/dotnet/standard/issues/481) riepiloga i problemi relativi a questo scenario, i piani per risolverli e le soluzioni alternative implementabili allo stato attuale degli strumenti.

## <a name="top-issues-fixed-in-this-release"></a>Problemi principali corretti in questa versione

### <a name="bugs"></a>Bug

* NuGet genera un deadlock nel sistema di progetti .NET Core (nuova regressione). - [#6733](https://github.com/NuGet/Home/issues/6733)
* Pack: costruzione non corretta di PackagePath se si usa TfmSpecificPackageFile con percorsi di globbing - [#6726](https://github.com/NuGet/Home/issues/6726)
* Pack: un progetto API Web non può creare un pacchetto se non viene impostato in modo esplicito ispackable. - [#6156](https://github.com/NuGet/Home/issues/6156)
* L'interfaccia utente di Visual Studio e PMC richiedono 30 minuti per visualizzare un nuovo pacchetto (nuget.exe lo vede subito) - [#6657](https://github.com/NuGet/Home/issues/6657)
* Firma:  SignatureUtility.GetCertificateChain(...) non controlla tutti gli stati della catena - [#6565](https://github.com/NuGet/Home/issues/6565)
* Firma: miglioramento della gestione DER GeneralizedTime - [#6564](https://github.com/NuGet/Home/issues/6564)
* Firma: VS non visualizza un errore NU3002 durante l'installazione di un pacchetto manomesso - [#6337](https://github.com/NuGet/Home/issues/6337)
* lockFile.GetLibrary distingue tra maiuscole e minuscole - [#6500](https://github.com/NuGet/Home/issues/6500)
* I percorsi del codice di installazione/aggiornamento e del codice di ripristino non sono coerenti - [#3471](https://github.com/NuGet/Home/issues/3471)
* La casella combinata della versione di PackageManager della soluzione consente la selezione del separatore tramite tastiera - [#2606](https://github.com/NuGet/Home/issues/2606)
* Non è possibile caricare l'indice del servizio per l'origine `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: il codice di stato della risposta non indica l'esito positivo: 403 (non consentito) - [#2530](https://github.com/NuGet/Home/issues/2530)

### <a name="dcrs"></a>DCR

* Generare l'intestazione X-NuGet-Session-Id per la correlazione tra le richieste [proposta di funzionalità] - [#5330](https://github.com/NuGet/Home/issues/5330)
* Esporre un modo per attendere durante l'esecuzione dell'operazione di ripristino in Visual Studio tramite API di IV. - [#6029](https://github.com/NuGet/Home/issues/6029)
* NuGet.exe -NoServiceEndpoint eviterà l'aggiunta del suffisso dell'URL del servizio - [#6586](https://github.com/NuGet/Home/issues/6586)
* Aggiungere l'hash di commit alla versione informativa - [#6492](https://github.com/NuGet/Home/issues/6492)
* Firma: abilitare la rimozione di firma/controfirma del repository - [#6646](https://github.com/NuGet/Home/issues/6646)
* Firma: API per rimuovere firma/controfirma del repository - [#6589](https://github.com/NuGet/Home/issues/6589)
* Registrare le informazioni sull'origine in Visual Studio - [#6527](https://github.com/NuGet/Home/issues/6527)
* Filtrare /tools solo per TFM e RID, in modo che il file XML di impostazioni possa essere inserito nella cartella /tools - [#6197](https://github.com/NuGet/Home/issues/6197)
* Avvisare quando il comando Pack esclude un file che inizia con.  - [#3308](https://github.com/NuGet/Home/issues/3308)

[Elenco di tutti i problemi corretti in questa versione](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
