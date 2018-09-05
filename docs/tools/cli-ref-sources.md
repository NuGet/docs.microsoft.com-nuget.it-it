---
title: Comando le origini NuGet CLI
description: Informazioni di riferimento per il nuget.exe origini di comandi
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7ef856f783c8e11cdb40edb0d1c1458730d87262
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548108"
---
# <a name="sources-command-nuget-cli"></a><span data-ttu-id="5b90d-103">Comando sources (interfaccia della riga di comando di NuGet)</span><span class="sxs-lookup"><span data-stu-id="5b90d-103">sources command (NuGet CLI)</span></span>

<span data-ttu-id="5b90d-104">**Si applica a:** utilizzo di un pacchetto, la pubblicazione &bullet; **le versioni supportate:** tutti</span><span class="sxs-lookup"><span data-stu-id="5b90d-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5b90d-105">Gestisce l'elenco delle origini che si trova nel file di configurazione di ambito utente o un file di configurazione specificato.</span><span class="sxs-lookup"><span data-stu-id="5b90d-105">Manages the list of sources located in the user scope configuration file or a specified configuration file.</span></span> <span data-ttu-id="5b90d-106">Il file di configurazione di ambito utente si trova in `%appdata%\NuGet\NuGet.Config` (Windows) e `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5b90d-106">The user scope configuration file is located at `%appdata%\NuGet\NuGet.Config` (Windows) and `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span></span>

<span data-ttu-id="5b90d-107">Si noti che l'URL di origine di nuget.org è `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="5b90d-107">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="usage"></a><span data-ttu-id="5b90d-108">Utilizzo</span><span class="sxs-lookup"><span data-stu-id="5b90d-108">Usage</span></span>

```cli
nuget sources <operation> -Name <name> -Source <source>
```

<span data-ttu-id="5b90d-109">in cui `<operation>` è uno dei *elencare, aggiungere, rimuovere, abilitare, disabilitare* oppure *Update*, `<name>` è il nome dell'origine, e `<source>` è l'URL dell'origine.</span><span class="sxs-lookup"><span data-stu-id="5b90d-109">where `<operation>` is one of *List, Add, Remove, Enable, Disable,* or *Update*, `<name>` is the name of the source, and `<source>` is the source's URL.</span></span>

## <a name="options"></a><span data-ttu-id="5b90d-110">Opzioni</span><span class="sxs-lookup"><span data-stu-id="5b90d-110">Options</span></span>

| <span data-ttu-id="5b90d-111">Opzione</span><span class="sxs-lookup"><span data-stu-id="5b90d-111">Option</span></span> | <span data-ttu-id="5b90d-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5b90d-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5b90d-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5b90d-113">ConfigFile</span></span> | <span data-ttu-id="5b90d-114">Il file di configurazione di NuGet da applicare.</span><span class="sxs-lookup"><span data-stu-id="5b90d-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5b90d-115">Se non specificato, `%AppData%\NuGet\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) viene usato.</span><span class="sxs-lookup"><span data-stu-id="5b90d-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5b90d-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5b90d-116">ForceEnglishOutput</span></span> | <span data-ttu-id="5b90d-117">*(3.5 +)*  Forza nuget.exe affinché venga eseguito usando una cultura invariante e di lingua inglese.</span><span class="sxs-lookup"><span data-stu-id="5b90d-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5b90d-118">Formato</span><span class="sxs-lookup"><span data-stu-id="5b90d-118">Format</span></span> | <span data-ttu-id="5b90d-119">Viene applicata il `list` azione e può essere `Detailed` (predefinito) o `Short`.</span><span class="sxs-lookup"><span data-stu-id="5b90d-119">Applies to the `list` action and can be `Detailed` (the default) or `Short`.</span></span> |
| <span data-ttu-id="5b90d-120">?</span><span class="sxs-lookup"><span data-stu-id="5b90d-120">Help</span></span> | <span data-ttu-id="5b90d-121">Visualizza la Guida informazioni per il comando.</span><span class="sxs-lookup"><span data-stu-id="5b90d-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="5b90d-122">Non interattive</span><span class="sxs-lookup"><span data-stu-id="5b90d-122">NonInteractive</span></span> | <span data-ttu-id="5b90d-123">Elimina richieste di input o conferme dell'utente.</span><span class="sxs-lookup"><span data-stu-id="5b90d-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5b90d-124">Password</span><span class="sxs-lookup"><span data-stu-id="5b90d-124">Password</span></span> | <span data-ttu-id="5b90d-125">Specifica la password per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="5b90d-125">Specifies the password for authenticating with the source.</span></span> |
| <span data-ttu-id="5b90d-126">StorePasswordInClearText</span><span class="sxs-lookup"><span data-stu-id="5b90d-126">StorePasswordInClearText</span></span> | <span data-ttu-id="5b90d-127">Indica di archiviare la password in testo non crittografato anziché il comportamento predefinito di un modulo crittografato di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5b90d-127">Indicates to store the password in unencrypted text instead of the default behavior of storing an encrypted form.</span></span> |
| <span data-ttu-id="5b90d-128">UserName</span><span class="sxs-lookup"><span data-stu-id="5b90d-128">UserName</span></span> | <span data-ttu-id="5b90d-129">Specifica il nome utente per l'autenticazione con l'origine.</span><span class="sxs-lookup"><span data-stu-id="5b90d-129">Specifies the user name for authenticating with the source.</span></span> |
| <span data-ttu-id="5b90d-130">Livello di dettaglio</span><span class="sxs-lookup"><span data-stu-id="5b90d-130">Verbosity</span></span> | <span data-ttu-id="5b90d-131">Specifica la quantità di dettaglio visualizzato nell'output: *normali*, *quiet*, *dettagliate*.</span><span class="sxs-lookup"><span data-stu-id="5b90d-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

> [!Note]
> <span data-ttu-id="5b90d-132">Assicurarsi di aggiungere password delle origini nello stesso contesto utente come il nuget.exe viene successivamente utilizzato per accedere all'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5b90d-132">Make sure to add the sources' password under the same user context as the nuget.exe is later used to access the package source.</span></span> <span data-ttu-id="5b90d-133">La password verrà archiviata crittografati nel file di configurazione e può essere decrittografata solo nello stesso contesto utente perché è stato crittografato.</span><span class="sxs-lookup"><span data-stu-id="5b90d-133">The password will be stored encrypted in the config file and can only be decrypted in the same user context as it was encrypted.</span></span> <span data-ttu-id="5b90d-134">Quindi, ad esempio quando si usa un server di compilazione per ripristinare i pacchetti NuGet che la password deve essere crittografata con lo stesso utente di Windows con cui verrà eseguita l'attività del server di compilazione.</span><span class="sxs-lookup"><span data-stu-id="5b90d-134">So for example when you use a build server to restore NuGet packages the password must be encrypted with the same Windows user under which  the build server task will run.</span></span>

<span data-ttu-id="5b90d-135">Vedere anche [le variabili di ambiente](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5b90d-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5b90d-136">Esempi</span><span class="sxs-lookup"><span data-stu-id="5b90d-136">Examples</span></span>

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
