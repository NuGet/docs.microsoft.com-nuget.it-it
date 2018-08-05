---
title: Riferimento di avvisi e gli errori di NuGet
description: Informazioni di riferimento complete per avvisi ed errori generati da NuGet durante varie operazioni di NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 73de86a4eed1a06979a86a0969b95f011de741fa
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508140"
---
# <a name="errors-and-warnings"></a>Errori e avvisi

In NuGet 4.3.0 + e forniscono informazioni dettagliate che consentono di risolvere i problemi relativi ad errori e avvisi sono numerati come descritto in questo argomento.

Gli errori e avvisi riportati di seguito sono disponibili solo con [basati su PackageReference](../consume-packages/package-references-in-project-files.md) progetti e NuGet 4.3.0 +. Inoltre, NuGet rispetta le proprietà di MSBuild per eliminare gli avvisi oppure di innalzarli di livello a errori. Per altre informazioni, vedere [procedura: eliminare gli avvisi del compilatore](/visualstudio/ide/how-to-suppress-compiler-warnings) nella documentazione di Visual Studio.

**Errori**

| Gruppo | Numeri di errore |
| --- | --- |
| Errori di input non validi | [NU1001](./errors-and-warnings/NU1001.md), [NU1002](./errors-and-warnings/NU1002.md), [NU1003](./errors-and-warnings/NU1003.md) |
| Errori di pacchetto e progetto mancanti | [NU1100](./errors-and-warnings/NU1100.md), [NU1101](./errors-and-warnings/NU1101.md), [NU1102](./errors-and-warnings/NU1102.md), [NU1103](./errors-and-warnings/NU1103.md), [NU1104](./errors-and-warnings/NU1104.md), [NU1105](./errors-and-warnings/NU1105.md), [NU1106](./errors-and-warnings/NU1106.md), [NU1107](./errors-and-warnings/NU1107.md), [NU1108](./errors-and-warnings/NU1108.md) |
| Errori di compatibilità | [NU1201](./errors-and-warnings/NU1201.md), [NU1202](./errors-and-warnings/NU1202.md), [NU1203](./errors-and-warnings/NU1203.md), [NU1401](./errors-and-warnings/NU1401.md) |
| Errori interni di NuGet | [NU1000](./errors-and-warnings/NU1000.md) |
| Errori pacchetti firmati (creazione e verifica) | [NU3000](./errors-and-warnings/NU3000.md), [NU3001](./errors-and-warnings/NU3001.md), [NU3004](./errors-and-warnings/NU3004.md), [NU3008](./errors-and-warnings/NU3008.md) |
| Errori dei pacchetti | [NU5000](./errors-and-warnings/NU5000.md), [NU5002](./errors-and-warnings/NU5002.md), [NU5003](./errors-and-warnings/NU5003.md), [NU5004](./errors-and-warnings/NU5004.md), [NU5008](./errors-and-warnings/NU5008.md), [NU5009](./errors-and-warnings/NU5009.md), [NU5010](./errors-and-warnings/NU5010.md), [NU5011](./errors-and-warnings/NU5011.md), [NU5012](./errors-and-warnings/NU5012.md), [NU5013](./errors-and-warnings/NU5013.md), [NU5014](./errors-and-warnings/NU5014.md), [NU5015](./errors-and-warnings/NU5015.md), [NU5016](./errors-and-warnings/NU5016.md), [NU5017](./errors-and-warnings/NU5017.md), [NU5018](./errors-and-warnings/NU5018.md), [NU5019](./errors-and-warnings/NU5019.md), [NU5026](./errors-and-warnings/NU5026.md)

**Avvisi**

| Gruppo | Numeri di avviso |
| --- | --- |
| Avvisi di input non validi | [NU1501](./errors-and-warnings/NU1501.md), [NU1502](./errors-and-warnings/NU1502.md), [NU1503](./errors-and-warnings/NU1503.md) |
| Avvisi versione pacchetto imprevisto | [NU1601](./errors-and-warnings/NU1601.md), [NU1602](./errors-and-warnings/NU1602.md), [NU1603](./errors-and-warnings/NU1603.md), [NU1604](./errors-and-warnings/NU1604.md), [NU1605](./errors-and-warnings/NU1605.md), [NU1606](./errors-and-warnings/NU1108.md), [NU1607](./errors-and-warnings/NU1107.md) |
| Avvisi di sistema di risoluzione dei conflitti | [NU1608](./errors-and-warnings/NU1608.md) |
| Avvisi di fallback del pacchetto | [NU1701](./errors-and-warnings/NU1701.md) |
| Gli avvisi del feed | [NU1801](./errors-and-warnings/NU1801.md) |
| Avvisi interni di NuGet | [NU1500](./errors-and-warnings/NU1500.md) |
| Avvisi di pacchetti firmati (creazione e verifica) | [NU3002](./errors-and-warnings/NU3002.md), [NU3018](./errors-and-warnings/NU3018.md), [NU3028](./errors-and-warnings/NU3028.md) |
| Avvisi di Pack | [NU5100](./errors-and-warnings/NU5100.md), [NU5101](./errors-and-warnings/NU5101.md), [NU5115](./errors-and-warnings/NU5115.md), [NU5500](./errors-and-warnings/NU5500.md)
