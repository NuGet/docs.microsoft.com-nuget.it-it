---
ms.openlocfilehash: e8949e9964ed19d342df53f08f59bb0f89e5feb0
ms.sourcegitcommit: 5aa49478dc466c67db5c3edda7c6ce8dcd8ae033
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/06/2019
ms.locfileid: "68817475"
---
L'identificatore del pacchetto e il numero di versione sono i due valori più importanti del progetto perché identificano in modo univoco il codice esatto contenuto nel pacchetto.

**Procedure consigliate per l'identificatore del pacchetto:**

- **Univocità**: l'identificatore deve essere univoco in nuget.org o in qualsiasi raccolta che ospita il pacchetto. Prima di scegliere un identificatore, eseguire una ricerca nella raccolta applicabile per controllare se il nome è già in uso. Per evitare conflitti, è consigliabile usare il nome della società come prima parte dell'identificatore, ad esempio `Contoso.`.
- **Nomi simili a spazi dei nomi**: seguono un modello simile a quello degli spazi dei nomi in .NET, usando la notazione con punto invece dei trattini. Usare, ad esempio, `Contoso.Utility.UsefulStuff` invece di `Contoso-Utility-UsefulStuff` o `Contoso_Utility_UsefulStuff`. Per gli utenti è anche utile che l'identificatore del pacchetto corrisponda agli spazi dei nomi usati nel codice.
- **Pacchetti di esempio**: se si produce un pacchetto di codice di esempio che illustra come usare un altro pacchetto, aggiungere `.Sample` come suffisso all'identificatore, come in `Contoso.Utility.UsefulStuff.Sample`. Il pacchetto di esempio avrà naturalmente una dipendenza dall'altro pacchetto. Quando si crea un pacchetto di esempio, usare il valore `contentFiles` in `<IncludeAssets>`. Nella cartella `content` inserire il codice di esempio in una cartella denominata `\Samples\<identifier>` come in `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Procedure consigliate per la versione del pacchetto:**

- In generale, impostare la versione del pacchetto in modo che corrisponda al progetto (o all'assembly), anche se non è strettamente necessario. Si tratta di un'operazione semplice quando si limita un pacchetto a un singolo assembly. In generale, tenere presente che, durante la risoluzione delle dipendenze, di per sé NuGet gestisce le versioni dei pacchetti, non le versioni degli assembly.
- Quando si usa uno schema della versione non standard, tenere in considerazione le regole di controllo delle versioni di NuGet, come illustrato in [Controllo delle versioni dei pacchetti](../../reference/package-versioning.md). NuGet è in gran parte [conforme a semver 2](../../reference/package-versioning.md#semantic-versioning-200).

> Per informazioni sulla risoluzione delle dipendenze, vedere [Risoluzione delle dipendenze con PackageReference](../../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference). Per informazioni meno recenti che possono essere utili anche per comprendere meglio il controllo delle versioni, vedere questa serie di post di blog.
>
> - [Parte 1. Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html) (Parte 1: Affrontare l'inferno delle DLL)
> - [Parte 2. The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html) (Parte 2: L'algoritmo principale)
> - [Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html) (Parte 3: Unificazione tramite i reindirizzamenti di binding)