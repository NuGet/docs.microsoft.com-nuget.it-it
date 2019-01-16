---
title: Comando di NuGet CLI firmatari attendibili
description: Informazioni di riferimento per il comando di firmatari attendibili nuget.exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ee4ffaa7e250cdbf313476fd794a8d87c80b69f9
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324708"
---
# <a name="trusted-signers-command-nuget-cli"></a>comando firmatari attendibili (NuGet CLI)

**Si applica a:** consumo del pacchetto &bullet; **versioni supportate:** 4.9.1+

Ottiene o imposta i firmatari attendibili per la configurazione di NuGet. Per altre informazioni sulla sintassi, vedere [configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md). Per informazioni dettagliate su come lo schema di NuGet. config sembra, vedere la [riferimento al file di configurazione NuGet](../reference/nuget-config-file.md).

## <a name="usage"></a>Utilizzo

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Se nessuna delle `list|add|remove|sync` viene specificato, il comando per impostazione predefinita sarà `list`.

## <a name="nuget-trusted-signers-list"></a>elenco di firmatari attendibili di NuGet

Elenca tutti i firmatari attendibili nella configurazione. Questa opzione includerà tutti i certificati, con impronta digitale e algoritmo di impronta digitale, con ogni firmatario. Se un certificato con una precedente `[U]`, significa che la voce certificato ha `allowUntrustedRoot` imposta come `true`.

Di seguito è un esempio di output da questo comando:

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>attendibili i firmatari NuGet add [opzioni]

Aggiunge un'entità attendibile con il nome specificato al file di configurazione. Questa opzione non ha i movimenti diversi per aggiungere un repository o autore attendibile.

## <a name="options-for-add-based-on-a-package"></a>Opzioni per l'aggiunta in un pacchetto di base

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

in cui `<package(s)>` è uno o più `.nupkg` file.

| Opzione | Descrizione |
| --- | --- |
| Autore | Specifica che la firma dell'autore dei pacchetti debba essere attendibile. |
| Repository | Specifica che la firma di repository o controfirma dei pacchetti deve essere considerato attendibile. |
| AllowUntrustedRoot | Specifica se il certificato del firmatario attendibile deve essere consentito concatenarsi a una radice non attendibile. |
| Proprietari | Elenco separato da punti e virgola dei proprietari attendibili per limitare ulteriormente l'attendibilità di un repository. Valido solo quando si usa il `-Repository` opzione. |

Forniscono `-Author` e `-Repository` allo stesso tempo non è supportato.

## <a name="options-for-add-based-on-a-service-index"></a>Opzioni Aggiungi basato su un indice di servizio

```cli
nuget trusted-signers add -Name <name> [options]
```

_Nota_: Questa opzione solo aggiungerà i repository attendibili. 

| Opzione | Descrizione |
| --- | --- |
| ServiceIndex | Specifica l'indice del servizio V3 del repository per essere considerato attendibile. Questo repository deve supportare la risorsa di firme di repository. Se non specificato, il comando cercherà il file di origine con lo stesso `-Name` e ottenere l'indice del servizio da tale posizione. |
| AllowUntrustedRoot | Specifica se il certificato del firmatario attendibile deve essere consentito concatenarsi a una radice non attendibile. |
| Proprietari | Elenco separato da punti e virgola dei proprietari attendibili per limitare ulteriormente l'attendibilità di un repository. |

## <a name="options-for-add-based-on-the-certificate-information"></a>Opzioni per aggiungere le informazioni sul certificato in base

```cli
nuget trusted-signers add -Name <name> [options]
```

_Nota_: Se un'entità attendibile con il nome specificato esiste già, l'elemento certificato verrà aggiunto a tale firmatario. In caso contrario, verrà creato un autore attendibile a un elemento di certificato da fornito informazioni sul certificato.

| Opzione | Descrizione |
| --- | --- |
| CertificateFingerprint | Specifica un certificato le impronte digitali di un certificato di pacchetti firmati devono essere firmate con. Un'impronta digitale certificato è un hash del certificato. Specifica l'algoritmo hash usato per calcolare l'hash deve essere il `FingerprintAlgorithm` opzione. |
| FingerprintAlgorithm | Specifica l'algoritmo hash usato per calcolare l'impronta digitale del certificato. Il valore predefinito è `SHA256`. Valori supportati sono `SHA256`, `SHA384` e `SHA512` |
| AllowUntrustedRoot | Specifica se il certificato del firmatario attendibile deve essere consentito concatenarsi a una radice non attendibile. |

## <a name="nuget-trusted-signers-remove--name-name"></a>rimuovere i firmatari attendibile-NuGet - nome <name>

Rimuove tutti i firmatari attendibili che corrispondono al nome specificato.

## <a name="nuget-trusted-signers-sync--name-name"></a>sincronizzare i firmatari attendibile-NuGet - nome <name>

Richiede l'elenco più recente di certificati usata in un repository attualmente considerato attendibile per aggiornare l'elenco certificato esistente in un'entità attendibile.

_Nota_: Questa azione verrà Elimina l'elenco corrente dei certificati e li sostituisce con un elenco aggiornato dal repository.

## <a name="options"></a>Opzioni

| Opzione | Descrizione |
| --- | --- |
| ConfigFile | Il file di configurazione di NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.|
| ForceEnglishOutput | Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese. |
| ? | Visualizza la Guida informazioni per il comando. |
| Livello di dettaglio | Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*. |

## <a name="examples"></a>Esempi

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
