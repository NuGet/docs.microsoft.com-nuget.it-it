---
title: Comando Di firma attendibile dell'interfaccia della riga di comando di NuGet
description: Informazioni di riferimento per il nuget.exe trusted signers
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: a5f3564af8b96dfa673d2252aea2e77a79c184a4
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323590"
---
# <a name="trusted-signers-command-nuget-cli"></a>Comando trusted-signers (interfaccia della riga di comando di NuGet)

**Si applica a:** Utilizzo pacchetti &bullet; **Versioni supportate:** 4.9.1+

Ottiene o imposta i firmatari attendibili per la configurazione NuGet. Per un utilizzo aggiuntivo, vedere [Configurazioni NuGet comuni.](../../consume-packages/configuring-nuget-behavior.md) Per informazioni dettagliate sull'aspetto nuget.config schema, vedere il riferimento al [file di configurazione NuGet](../nuget-config-file.md).

## <a name="usage"></a>Utilizzo

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

Se non viene specificato `list|add|remove|sync` nessuno di , il comando verrà utilizzato per impostazione `list` predefinita.

## <a name="nuget-trusted-signers-list"></a>Elenco di firmatari attendibili nuget

Elenca tutti i firmatari attendibili nella configurazione. Questa opzione includerà tutti i certificati (con impronta digitale e algoritmo di impronta digitale) di ogni firmatario. Se un certificato ha un precedente `[U]` , significa che la voce del certificato è `allowUntrustedRoot` impostata su `true` .

Di seguito è riportato un output di esempio di questo comando:

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a>nuget trusted-signers add [options]

Aggiunge un firmatario attendibile con il nome specificato alla configurazione. Questa opzione ha movimenti diversi per aggiungere un autore o un repository attendibile.

## <a name="options-for-add-based-on-a-package"></a>Opzioni per l'aggiunta in base a un pacchetto

```cli
nuget trusted-signers add <package> -Name <name> [options]
```

dove `<package>` è un file `.nupkg` firmato.

- **`-Author`**

  Specifica che la firma dell'autore del pacchetto firmato deve essere attendibile.

- **`-AllowUntrustedRoot`**

  Specifica se il certificato per il firmatario attendibile deve essere autorizzato a concatenare a una radice non attendibile.

- **`-Owners`**

  Elenco di proprietari attendibili separati da punto e virgola per limitare ulteriormente l'attendibilità di un repository. Valido solo quando si usa `-Repository` l'opzione .

- **`-Repository`**

  Specifica che la firma del repository o la controfirma del pacchetto firmato deve essere attendibile.

Non è supportato specificare sia che `-Author` `-Repository` contemporaneamente.

## <a name="options-for-add-based-on-a-service-index"></a>Opzioni per l'aggiunta in base a un indice del servizio

```cli
nuget trusted-signers add -Name <name> [options]
```

_Nota:_ questa opzione aggiungerà solo repository attendibili. 

- **`-AllowUntrustedRoot`**

  Specifica se il certificato per il firmatario attendibile deve essere autorizzato a concatenare a una radice non attendibile.

- **`-Owners`**

  Elenco di proprietari attendibili separati da punto e virgola per limitare ulteriormente l'attendibilità di un repository.

- **`-ServiceIndex`**

  Specifica l'indice del servizio V3 del repository da considerato attendibile. Questo repository deve supportare la risorsa firme del repository. Se non viene specificato, il comando cerca un'origine del pacchetto con lo stesso `-Name` valore e ottiene l'indice del servizio da qui.

## <a name="options-for-add-based-on-the-certificate-information"></a>Opzioni per l'aggiunta in base alle informazioni sul certificato

```cli
nuget trusted-signers add -Name <name> [options]
```

_Nota:_ se esiste già un firmatario attendibile con il nome specificato, l'elemento del certificato verrà aggiunto a tale firmatario. In caso contrario, verrà creato un autore attendibile con un elemento certificato dalle informazioni sul certificato specificato.


- **`-AllowUntrustedRoot`**

  Specifica se il certificato per il firmatario attendibile deve essere autorizzato a concatenare a una radice non attendibile.

- **`-CertificateFingerprint`**

  Specifica le impronte digitali di un certificato con cui devono essere firmati i pacchetti firmati. Un'impronta digitale del certificato è un hash del certificato. L'algoritmo hash usato per calcolare questo hash deve essere specificato `FingerprintAlgorithm` nell'opzione .

- **`-FingerprintAlgorithm`**

  Specifica l'algoritmo hash utilizzato per calcolare l'impronta digitale del certificato. Il valore predefinito è `SHA256`. I valori supportati `SHA256` sono , `SHA384` e `SHA512` .

## <a name="nuget-trusted-signers-remove--name-name"></a>nuget trusted-signers remove -Name \<name\>

Rimuove tutti i firmatari attendibili che corrispondono al nome specificato.

## <a name="nuget-trusted-signers-sync--name-name"></a>nuget trusted-signers sync -Name \<name\>

Richiede l'elenco più recente dei certificati usati in un repository attualmente attendibile per aggiornare l'elenco di certificati esistente nel firmatario attendibile.

_Nota:_ questo movimento eliminerà l'elenco corrente di certificati e li sostituirà con un elenco aggiornato dal repository.

## <a name="options"></a>Opzioni

- **`-ConfigFile`**

  File di configurazione NuGet da applicare. Se non specificato, `%AppData%\NuGet\NuGet.Config` viene usato `~/.nuget/NuGet/NuGet.Config` (Windows) o `~/.config/NuGet/NuGet.Config` (Mac/Linux).

- **`-ForceEnglishOutput`**

  Forza nuget.exe'esecuzione usando impostazioni cultura invarianti basate sull'inglese.

- **`-?|-help`**

  Visualizza le informazioni della Guida per il comando.

- **`-Name`**

  Nome del firmatario attendibile.

- **`-NonInteractive`**

  Elimina le richieste di input o di conferma dell'utente.

- **`-Verbosity [normal|quiet|detailed]`**

  Specifica la quantità di dettagli visualizzati nell'output: `normal` (impostazione predefinita), `quiet` o `detailed` .


## <a name="examples"></a>Esempi

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
