---
ms.openlocfilehash: e8949e9964ed19d342df53f08f59bb0f89e5feb0
ms.sourcegitcommit: 5aa49478dc466c67db5c3edda7c6ce8dcd8ae033
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/06/2019
ms.locfileid: "68817475"
---
<span data-ttu-id="836f5-101">L'identificatore del pacchetto e il numero di versione sono i due valori più importanti del progetto perché identificano in modo univoco il codice esatto contenuto nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="836f5-101">The package identifier and the version number are the two most important values in the project because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="836f5-102">**Procedure consigliate per l'identificatore del pacchetto:**</span><span class="sxs-lookup"><span data-stu-id="836f5-102">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="836f5-103">**Univocità**: l'identificatore deve essere univoco in nuget.org o in qualsiasi raccolta che ospita il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="836f5-103">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="836f5-104">Prima di scegliere un identificatore, eseguire una ricerca nella raccolta applicabile per controllare se il nome è già in uso.</span><span class="sxs-lookup"><span data-stu-id="836f5-104">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="836f5-105">Per evitare conflitti, è consigliabile usare il nome della società come prima parte dell'identificatore, ad esempio `Contoso.`.</span><span class="sxs-lookup"><span data-stu-id="836f5-105">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="836f5-106">**Nomi simili a spazi dei nomi**: seguono un modello simile a quello degli spazi dei nomi in .NET, usando la notazione con punto invece dei trattini.</span><span class="sxs-lookup"><span data-stu-id="836f5-106">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="836f5-107">Usare, ad esempio, `Contoso.Utility.UsefulStuff` invece di `Contoso-Utility-UsefulStuff` o `Contoso_Utility_UsefulStuff`.</span><span class="sxs-lookup"><span data-stu-id="836f5-107">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="836f5-108">Per gli utenti è anche utile che l'identificatore del pacchetto corrisponda agli spazi dei nomi usati nel codice.</span><span class="sxs-lookup"><span data-stu-id="836f5-108">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="836f5-109">**Pacchetti di esempio**: se si produce un pacchetto di codice di esempio che illustra come usare un altro pacchetto, aggiungere `.Sample` come suffisso all'identificatore, come in `Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="836f5-109">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="836f5-110">Il pacchetto di esempio avrà naturalmente una dipendenza dall'altro pacchetto. Quando si crea un pacchetto di esempio, usare il valore `contentFiles` in `<IncludeAssets>`.</span><span class="sxs-lookup"><span data-stu-id="836f5-110">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the `contentFiles` value in `<IncludeAssets>`.</span></span> <span data-ttu-id="836f5-111">Nella cartella `content` inserire il codice di esempio in una cartella denominata `\Samples\<identifier>` come in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span><span class="sxs-lookup"><span data-stu-id="836f5-111">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="836f5-112">**Procedure consigliate per la versione del pacchetto:**</span><span class="sxs-lookup"><span data-stu-id="836f5-112">**Best practices for the package version:**</span></span>

- <span data-ttu-id="836f5-113">In generale, impostare la versione del pacchetto in modo che corrisponda al progetto (o all'assembly), anche se non è strettamente necessario.</span><span class="sxs-lookup"><span data-stu-id="836f5-113">In general, set the version of the package to match the project (or assembly), though this is not strictly required.</span></span> <span data-ttu-id="836f5-114">Si tratta di un'operazione semplice quando si limita un pacchetto a un singolo assembly.</span><span class="sxs-lookup"><span data-stu-id="836f5-114">This is a simple matter when you limit a package to a single assembly.</span></span> <span data-ttu-id="836f5-115">In generale, tenere presente che, durante la risoluzione delle dipendenze, di per sé NuGet gestisce le versioni dei pacchetti, non le versioni degli assembly.</span><span class="sxs-lookup"><span data-stu-id="836f5-115">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="836f5-116">Quando si usa uno schema della versione non standard, tenere in considerazione le regole di controllo delle versioni di NuGet, come illustrato in [Controllo delle versioni dei pacchetti](../../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="836f5-116">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../../reference/package-versioning.md).</span></span> <span data-ttu-id="836f5-117">NuGet è in gran parte [conforme a semver 2](../../reference/package-versioning.md#semantic-versioning-200).</span><span class="sxs-lookup"><span data-stu-id="836f5-117">NuGet is mostly [semver 2 compliant](../../reference/package-versioning.md#semantic-versioning-200).</span></span>

> <span data-ttu-id="836f5-118">Per informazioni sulla risoluzione delle dipendenze, vedere [Risoluzione delle dipendenze con PackageReference](../../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).</span><span class="sxs-lookup"><span data-stu-id="836f5-118">For information on dependency resolution, see [Dependency resolution with PackageReference](../../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).</span></span> <span data-ttu-id="836f5-119">Per informazioni meno recenti che possono essere utili anche per comprendere meglio il controllo delle versioni, vedere questa serie di post di blog.</span><span class="sxs-lookup"><span data-stu-id="836f5-119">For older information that may also be helpful to better understand versioning, see this series of blog posts.</span></span>
>
> - <span data-ttu-id="836f5-120">[Parte 1. Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html) (Parte 1: Affrontare l'inferno delle DLL)</span><span class="sxs-lookup"><span data-stu-id="836f5-120">[Part 1: Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)</span></span>
> - <span data-ttu-id="836f5-121">[Parte 2. The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html) (Parte 2: L'algoritmo principale)</span><span class="sxs-lookup"><span data-stu-id="836f5-121">[Part 2: The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)</span></span>
> - <span data-ttu-id="836f5-122">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html) (Parte 3: Unificazione tramite i reindirizzamenti di binding)</span><span class="sxs-lookup"><span data-stu-id="836f5-122">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)</span></span>