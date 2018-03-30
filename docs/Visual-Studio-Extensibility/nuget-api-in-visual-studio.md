---
title: API NuGet in Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Informazioni di riferimento per l'API esportata da NuGet mediante Managed Extensibility Framework in Visual Studio
keywords: API NuGet, NuGet in Visual Studio, interfacce di programmazione di NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 1b23535ae3ec1ea490b513a11906ff1338d1997c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-api-in-visual-studio"></a><span data-ttu-id="34c6c-104">API NuGet in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="34c6c-104">NuGet API in Visual Studio</span></span>

<span data-ttu-id="34c6c-105">Oltre all'interfaccia utente e alla console di Gestione pacchetti in Visual Studio, NuGet esporta anche alcuni utili servizi tramite [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index).</span><span class="sxs-lookup"><span data-stu-id="34c6c-105">In addition to the Package Manager UI and Console in Visual Studio, NuGet also exports some useful services through the [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index).</span></span> <span data-ttu-id="34c6c-106">Questa interfaccia consente ad altri componenti in Visual Studio di interagire con NuGet, che può essere usato per installare e disinstallare i pacchetti e per ottenere informazioni sui pacchetti installati.</span><span class="sxs-lookup"><span data-stu-id="34c6c-106">This interface allows other components in Visual Studio to interact with NuGet, which can be used to install and uninstall packages, and to obtain information about installed packages.</span></span>

<span data-ttu-id="34c6c-107">A partire da NuGet 3.3 +, NuGet esporta i servizi seguenti tutti inclusi nello spazio dei nomi `NuGet.VisualStudio` nell'assembly `NuGet.VisualStudio.dll`:</span><span class="sxs-lookup"><span data-stu-id="34c6c-107">As of NuGet 3.3+, NuGet exports the following services all of which reside in the `NuGet.VisualStudio` namespace in the `NuGet.VisualStudio.dll` assembly:</span></span>

- <span data-ttu-id="34c6c-108">[`IRegistryKey`](#iregistrykey-interface): metodo per recuperare un valore da una sottochiave del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="34c6c-108">[`IRegistryKey`](#iregistrykey-interface): Method to retrieve a value from a registry subkey.</span></span>
- <span data-ttu-id="34c6c-109">[`IVsPackageInstaller`](#ivspackageinstaller-interface): metodi per installare pacchetti NuGet in progetti.</span><span class="sxs-lookup"><span data-stu-id="34c6c-109">[`IVsPackageInstaller`](#ivspackageinstaller-interface): Methods to install NuGet packages into projects.</span></span>
- <span data-ttu-id="34c6c-110">[`IVsPackageInstallerEvents`](#ivspackageinstallerevents-interface): eventi per l'installazione o disinstallazione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="34c6c-110">[`IVsPackageInstallerEvents`](#ivspackageinstallerevents-interface): Events for package install/uninstall.</span></span>
- <span data-ttu-id="34c6c-111">[`IVsPackageInstallerProjectEvents`](#ivspackageinstallerprojectevents-interface): eventi batch per l'installazione o disinstallazione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="34c6c-111">[`IVsPackageInstallerProjectEvents`](#ivspackageinstallerprojectevents-interface): Batch events for package install/uninstall.</span></span>
- <span data-ttu-id="34c6c-112">[`IVsPackageInstallerServices`](#ivspackageinstallerservices-interface): metodi per recuperare i pacchetti installati nella soluzione corrente e per verificare se un determinato pacchetto è installato in un progetto.</span><span class="sxs-lookup"><span data-stu-id="34c6c-112">[`IVsPackageInstallerServices`](#ivspackageinstallerservices-interface): Methods to retrieve installed packages in the current solution and to check whether a given package is installed in a project.</span></span>
- <span data-ttu-id="34c6c-113">[`IVsPackageManagerProvider`](#ivspackagemanagerprovider-interface): metodi per fornire suggerimenti di Gestione pacchetti alternativi per un pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="34c6c-113">[`IVsPackageManagerProvider`](#ivspackagemanagerprovider-interface): Methods to provide alternative Package Manager suggestions for a NuGet package.</span></span>
- <span data-ttu-id="34c6c-114">[`IVsPackageMetadata`](#ivspackagemetadata-interface): metodi per recuperare informazioni su un pacchetto installato.</span><span class="sxs-lookup"><span data-stu-id="34c6c-114">[`IVsPackageMetadata`](#ivspackagemetadata-interface); Methods to retrieve information about an installed package.</span></span>
- <span data-ttu-id="34c6c-115">[`IVsPackageProjectMetadata`](#ivspackageprojectmetadata-interface): metodi per recuperare informazioni su un progetto in cui vengono eseguite azioni NuGet.</span><span class="sxs-lookup"><span data-stu-id="34c6c-115">[`IVsPackageProjectMetadata`](#ivspackageprojectmetadata-interface); Methods to retrieve information about a project where NuGet actions are being executed.</span></span>
- <span data-ttu-id="34c6c-116">[`IVsPackageRestorer`](#ivspackagerestorer-interface): metodi per ripristinare i pacchetti installati in un progetto.</span><span class="sxs-lookup"><span data-stu-id="34c6c-116">[`IVsPackageRestorer`](#ivspackagerestorer-interface): Methods to restore packages installed in a project.</span></span>
- <span data-ttu-id="34c6c-117">[`IVsPackageSourceProvider`](#ivspackagesourceprovider-interface): metodi per recuperare un elenco di origini di pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="34c6c-117">[`IVsPackageSourceProvider`](#ivspackagesourceprovider-interface): Methods to retrieve a list of NuGet package sources.</span></span>
- <span data-ttu-id="34c6c-118">[`IVsPackageUninstaller`](#ivspackageuninstaller-interface): metodi per disinstallare pacchetti NuGet da progetti.</span><span class="sxs-lookup"><span data-stu-id="34c6c-118">[`IVsPackageUninstaller`](#ivspackageuninstaller-interface): Methods to uninstall NuGet packages from projects.</span></span>
- <span data-ttu-id="34c6c-119">[`IVsTemplateWizard`](#ivstemplatewizard-interface): progettata per includere pacchetti preinstallati in modelli di progetto/elemento. Questa interfaccia *non* è concepita per essere richiamata dal codice e non offre metodi pubblici.</span><span class="sxs-lookup"><span data-stu-id="34c6c-119">[`IVsTemplateWizard`](#ivstemplatewizard-interface): Designed for project/item templates to include pre-installed packages; this interface is *not* meant to be invoked from code and has no public methods.</span></span>

## <a name="using-nuget-services"></a><span data-ttu-id="34c6c-120">Uso dei servizi NuGet</span><span class="sxs-lookup"><span data-stu-id="34c6c-120">Using NuGet services</span></span>

1. <span data-ttu-id="34c6c-121">Installare il pacchetto [`NuGet.VisualStudio`](https://www.nuget.org/packages/NuGet.VisualStudio) nel progetto che contiene l'assembly `NuGet.VisualStudio.dll`.</span><span class="sxs-lookup"><span data-stu-id="34c6c-121">Install the [`NuGet.VisualStudio`](https://www.nuget.org/packages/NuGet.VisualStudio) package into your project, which contains the `NuGet.VisualStudio.dll` assembly.</span></span>

    <span data-ttu-id="34c6c-122">Al momento dell'installazione il pacchetto imposta automaticamente la proprietà **Incorpora tipi di interoperabilità** del riferimento all'assembly su **True**.</span><span class="sxs-lookup"><span data-stu-id="34c6c-122">When installed, the package automatically sets the **Embed Interop Types** property of the assembly reference to **True**.</span></span> <span data-ttu-id="34c6c-123">Il codice diventa così resiliente alle modifiche di versione quando gli utenti eseguono l'aggiornamento a versioni più recenti di NuGet.</span><span class="sxs-lookup"><span data-stu-id="34c6c-123">This makes your code  resilient against version changes when users update to newer versions of NuGet.</span></span>

> [!Warning]
> <span data-ttu-id="34c6c-124">Non usare altri tipi oltre alle interfacce pubbliche nel codice e non fare riferimento ad altri assembly NuGet, incluso `NuGet.Core.dll`.</span><span class="sxs-lookup"><span data-stu-id="34c6c-124">Do not use any other types besides the public interfaces in your code, and do not reference any other NuGet assemblies, including `NuGet.Core.dll`.</span></span>

1. <span data-ttu-id="34c6c-125">Per usare un servizio, importarlo tramite l'[attributo Import di MEF](/dotnet/framework/mef/index#imports-and-exports-with-attributes) o tramite il [servizio IComponentModel](/dotnet/api/microsoft.visualstudio.componentmodelhost.icomponentmodel?redirectedfrom=MSDN&view=visualstudiosdk-2017).</span><span class="sxs-lookup"><span data-stu-id="34c6c-125">To use a service, import it through the [MEF Import attribute](/dotnet/framework/mef/index#imports-and-exports-with-attributes), or through the [IComponentModel service](/dotnet/api/microsoft.visualstudio.componentmodelhost.icomponentmodel?redirectedfrom=MSDN&view=visualstudiosdk-2017).</span></span>

    ```cs
    //Using the Import attribute
    [Import(typeof(IVsPackageInstaller2))]
    public IVsPackageInstaller2 packageInstaller;
    packageInstaller.InstallLatestPackage(null, currentProject,
        "Newtonsoft.Json", false, false);

    //Using the IComponentModel service
    var componentModel = (IComponentModel)GetService(typeof(SComponentModel));
    IVsPackageInstallerServices installerServices =
        componentModel.GetService<IVsPackageInstallerServices>();

    var installedPackages = installerServices.GetInstalledPackages();
    ```

<span data-ttu-id="34c6c-126">Per riferimento, il codice sorgente per NuGet.VisualStudio è contenuto all'interno del [repository NuGet.Clients](https://github.com/NuGet/NuGet.Client/tree/dev/src/NuGet.Clients/NuGet.VisualStudio).</span><span class="sxs-lookup"><span data-stu-id="34c6c-126">For reference, the source code for NuGet.VisualStudio is contained within the [NuGet.Clients repository](https://github.com/NuGet/NuGet.Client/tree/dev/src/NuGet.Clients/NuGet.VisualStudio).</span></span>

## <a name="iregistrykey-interface"></a><span data-ttu-id="34c6c-127">Interfaccia IRegistryKey</span><span class="sxs-lookup"><span data-stu-id="34c6c-127">IRegistryKey interface</span></span>

```cs
/// <summary>
/// Specifies methods for manipulating a key in the Windows registry.
/// </summary>
public interface IRegistryKey
    {
    /// <summary>
    /// Retrieves the specified subkey for read or read/write access.
    /// </summary>
    /// <param name="name">The name or path of the subkey to create or open.</param>
    /// <returns>The subkey requested, or null if the operation failed.</returns>
    IRegistryKey OpenSubKey(string name);


    /// <summary>
    /// Retrieves the value associated with the specified name.
    /// </summary>
    /// <param name="name">The name of the value to retrieve. This string is not case-sensitive.</param>
    /// <returns>The value associated with name, or null if name is not found.</returns>
    object GetValue(string name);


    /// <summary>
    /// Closes the key and flushes it to disk if its contents have been modified.
    /// </summary>
    void Close();
}
```

## <a name="ivspackageinstaller-interface"></a><span data-ttu-id="34c6c-128">Interfaccia IVsPackageInstaller</span><span class="sxs-lookup"><span data-stu-id="34c6c-128">IVsPackageInstaller interface</span></span>

```cs
public interface IVsPackageInstaller
{
    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="source">
    /// The package source to install the package from. This value can be <c>null</c>
    /// to indicate that the user's configured sources should be used. Otherwise,
    /// this should be the source path as a string. If the user has credentials
    /// configured for a source, this value must exactly match the configured source
    /// value.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package ID of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    void InstallPackage(string source, Project project, string packageId, Version version, bool ignoreDependencies);

    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="source">
    /// The package source to install the package from. This value can be <c>null</c>
    /// to indicate that the user's configured sources should be used. Otherwise,
    /// this should be the source path as a string. If the user has credentials
    /// configured for a source, this value must exactly match the configured source
    /// value.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package ID of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    void InstallPackage(string source, Project project, string packageId, string version, bool ignoreDependencies);

    /// <summary>
    /// Installs a single package from the specified package source.
    /// </summary>
    /// <param name="repository">The package repository to install the package from.</param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageId">The package id of the package to install.</param>
    /// <param name="version">
    /// The version of the package to install. <c>null</c> can be provided to
    /// install the latest version of the package.
    /// </param>
    /// <param name="ignoreDependencies">
    /// A boolean indicating whether or not to ignore the package's dependencies
    /// during installation.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating if assembly references from the package should be
    /// skipped.
    /// </param>
    void InstallPackage(IPackageRepository repository, Project project, string packageId, string version, bool ignoreDependencies, bool skipAssemblyReferences);

    /// <summary>
    /// Installs one or more packages that exist on disk in a folder defined in the registry.
    /// </summary>
    /// <param name="keyName">
    /// The registry key name (under NuGet's repository key) that defines the folder on disk
    /// containing the packages.
    /// </param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// <para>
    /// Dependencies are always ignored.
    /// </para>
    /// </remarks>
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that exist on disk in a folder defined in the registry.
    /// </summary>
    /// <param name="keyName">
    /// The registry key name (under NuGet's repository key) that defines the folder on disk
    /// containing the packages.
    /// </param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="ignoreDependencies">A boolean indicating whether the package's dependencies should be ignored</param>
    /// <param name="project">The target project for package installation.</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// </remarks>
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, bool ignoreDependencies, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that are embedded in a Visual Studio Extension Package.
    /// </summary>
    /// <param name="extensionId">The Id of the Visual Studio Extension Package.</param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="project">The target project for package installation</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// <para>
    /// Dependencies are always ignored.
    /// </para>
    /// </remarks>
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    /// <summary>
    /// Installs one or more packages that are embedded in a Visual Studio Extension Package.
    /// </summary>
    /// <param name="extensionId">The Id of the Visual Studio Extension Package.</param>
    /// <param name="isPreUnzipped">
    /// A boolean indicating whether the folder contains packages that are
    /// pre-unzipped.
    /// </param>
    /// <param name="skipAssemblyReferences">
    /// A boolean indicating whether the assembly references from the packages
    /// should be skipped.
    /// </param>
    /// <param name="ignoreDependencies">A boolean indicating whether the package's dependencies should be ignored</param>
    /// <param name="project">The target project for package installation</param>
    /// <param name="packageVersions">
    /// A dictionary of packages/versions to install where the key is the package id
    /// and the value is the version.
    /// </param>
    /// <remarks>
    /// If any version of the package is already installed, no action will be taken.
    /// </remarks>
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, bool ignoreDependencies, Project project, IDictionary<string, string> packageVersions);
}
```

## <a name="ivspackageinstallerevents-interface"></a><span data-ttu-id="34c6c-129">Interfaccia IVsPackageInstallerEvents</span><span class="sxs-lookup"><span data-stu-id="34c6c-129">IVsPackageInstallerEvents interface</span></span>

```cs
public interface IVsPackageInstallerEvents
{
    /// <summary>
    /// Raised when a package is about to be installed into the current solution.
    /// </summary>
    event VsPackageEventHandler PackageInstalling;

    /// <summary>
    /// Raised after a package has been installed into the current solution.
    /// </summary>
    event VsPackageEventHandler PackageInstalled;

    /// <summary>
    /// Raised when a package is about to be uninstalled from the current solution.
    /// </summary>
    event VsPackageEventHandler PackageUninstalling;

    /// <summary>
    /// Raised after a package has been uninstalled from the current solution.
    /// </summary>
    event VsPackageEventHandler PackageUninstalled;

    /// <summary>
    /// Raised after a package has been installed into a project within the current solution.
    /// </summary>
    event VsPackageEventHandler PackageReferenceAdded;

    /// <summary>
    /// Raised after a package has been uninstalled from a project within the current solution.
    /// </summary>
    event VsPackageEventHandler PackageReferenceRemoved;
}
```

## <a name="ivspackageinstallerprojectevents-interface"></a><span data-ttu-id="34c6c-130">Interfaccia IVsPackageInstallerProjectEvents</span><span class="sxs-lookup"><span data-stu-id="34c6c-130">IVsPackageInstallerProjectEvents interface</span></span>

```cs
public interface IVsPackageInstallerProjectEvents
{
    /// <summary>
    /// Raised before any IVsPackageInstallerEvents events are raised for a project.
    /// </summary>
    event VsPackageProjectEventHandler BatchStart;

    /// <summary>
    /// Raised after all IVsPackageInstallerEvents events are raised for a project.
    /// </summary>
    event VsPackageProjectEventHandler BatchEnd;
}
```

## <a name="ivspackageinstallerservices-interface"></a><span data-ttu-id="34c6c-131">Interfaccia IVsPackageInstallerServices</span><span class="sxs-lookup"><span data-stu-id="34c6c-131">IVsPackageInstallerServices interface</span></span>

```cs
public interface IVsPackageInstallerServices
{
    // IMPORTANT: do NOT rearrange the methods here. The order is important to maintain
    // backwards compatibility with clients that were compiled against old versions of NuGet.

    /// <summary>
    /// Get the list of NuGet packages installed in the current solution.
    /// </summary>
    IEnumerable<IVsPackageMetadata> GetInstalledPackages();

    /// <summary>
    /// Checks if a NuGet package with the specified Id is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    bool IsPackageInstalled(Project project, string id);

    /// <summary>
    /// Checks if a NuGet package with the specified Id and version is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <param name="version">The version of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    bool IsPackageInstalled(Project project, string id, SemanticVersion version);

    /// <summary>
    /// Checks if a NuGet package with the specified Id and version is installed in the specified project.
    /// </summary>
    /// <param name="project">The project to check for NuGet package.</param>
    /// <param name="id">The id of the package to check.</param>
    /// <param name="versionString">The version of the package to check.</param>
    /// <returns><c>true</c> if the package is install. <c>false</c> otherwise.</returns>
    /// <remarks>
    /// The reason this method is named IsPackageInstalledEx, instead of IsPackageInstalled, is that
    /// when client project compiles against this assembly, the compiler would attempt to bind against
    /// the other overload which accepts SemanticVersion and would require client project to reference NuGet.Core.
    /// </remarks>
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    /// <summary>
    /// Get the list of NuGet packages installed in the specified project.
    /// </summary>
    /// <param name="project">The project to get NuGet packages from.</param>
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
}
```

## <a name="ivspackagemanagerprovider-interface"></a><span data-ttu-id="34c6c-132">Interfaccia IVsPackageManagerProvider</span><span class="sxs-lookup"><span data-stu-id="34c6c-132">IVsPackageManagerProvider interface</span></span>

```cs
public interface IVsPackageManagerProvider
{
    /// <summary>
    /// Localized display package manager name.
    /// </summary>
    string PackageManagerName { get; }

    /// <summary>
    /// Package manager unique id.
    /// </summary>
    string PackageManagerId { get; }

    /// <summary>
    /// The tool tip description for the package
    /// </summary>
    string Description { get; }

    /// <summary>
    /// Check if a recommendation should be surfaced for an alternate package manager.
    /// This code should not rely on slow network calls, and should return rapidly.
    /// </summary>
    /// <param name="packageId">Current package id</param>
    /// <param name="projectName">Unique project name for finding the project through VS dte</param>
    /// <param name="token">Cancellation Token</param>
    /// <returns>return true if need to direct to integrated package manager for this package</returns>
    Task<bool> CheckForPackageAsync(string packageId, string projectName, CancellationToken token);

    /// <summary>
    /// This Action should take the user to the other package manager.
    /// </summary>
    /// <param name="packageId">Current package id</param>
    /// <param name="projectName">Unique project name for finding the project through VS dte</param>
    void GoToPackage(string packageId, string projectName);
}
```

## <a name="ivspackagemetadata-interface"></a><span data-ttu-id="34c6c-133">Interfaccia IVsPackageMetadata</span><span class="sxs-lookup"><span data-stu-id="34c6c-133">IVsPackageMetadata interface</span></span>

```cs
public interface IVsPackageMetadata
{
    /// <summary>
    /// Id of the package.
    /// </summary>
    string Id { get; }

    /// <summary>
    /// Version of the package.
    /// </summary>
    /// <remarks>
    /// Do not use this property because it will require referencing NuGet.Core.dll assembly. Use the VersionString
    /// property instead.
    /// </remarks>
    [Obsolete("Do not use this property because it will require referencing NuGet.Core.dll assembly. Use the VersionString property instead.")]
    NuGet.SemanticVersion Version { get; }

    /// <summary>
    /// Title of the package.
    /// </summary>
    string Title { get; }

    /// <summary>
    /// Description of the package.
    /// </summary>
    string Description { get; }

    /// <summary>
    /// The authors of the package.
    /// </summary>
    IEnumerable<string> Authors { get; }

    /// <summary>
    /// The location where the package is installed on disk.
    /// </summary>
    string InstallPath { get; }

    // IMPORTANT: This property must come LAST, because it was added in 2.5. Having it declared
    // LAST will avoid breaking components that compiled against earlier versions which doesn't
    // have this property.
    /// <summary>
    /// The version of the package.
    /// </summary>
    /// <remarks>
    /// Use this property instead of the Version property becase with the type string,
    /// it doesn't require referencing NuGet.Core.dll assembly.
    /// </remarks>
    string VersionString { get; }
}
```

## <a name="ivspackageprojectmetadata-interface"></a><span data-ttu-id="34c6c-134">Interfaccia IVsPackageProjectMetadata</span><span class="sxs-lookup"><span data-stu-id="34c6c-134">IVsPackageProjectMetadata interface</span></span>

```cs
public interface IVsPackageProjectMetadata
{
    /// <summary>
    /// Unique batch id for batch start/end events of the project.
    /// </summary>
    string BatchId { get; }

    /// <summary>
    /// Name of the project.
    /// </summary>
    string ProjectName { get; }
}
```

## <a name="ivspackagerestorer-interface"></a><span data-ttu-id="34c6c-135">Interfaccia IVsPackageRestorer</span><span class="sxs-lookup"><span data-stu-id="34c6c-135">IVsPackageRestorer interface</span></span>

```cs
public interface IVsPackageRestorer
{
    /// <summary>
    /// Returns a value indicating whether the user consent to download NuGet packages
    /// has been granted.
    /// </summary>
    /// <returns>true if the user consent has been granted; otherwise, false.</returns>
    bool IsUserConsentGranted();

    /// <summary>
    /// Restores NuGet packages installed in the given project within the current solution.
    /// </summary>
    /// <param name="project">The project whose NuGet packages to restore.</param>
    void RestorePackages(Project project);
}
```

## <a name="ivspackagesourceprovider-interface"></a><span data-ttu-id="34c6c-136">Interfaccia IVsPackageSourceProvider</span><span class="sxs-lookup"><span data-stu-id="34c6c-136">IVsPackageSourceProvider interface</span></span>

```cs
public interface IVsPackageSourceProvider
{
    /// <summary>
    /// Provides the list of package sources.
    /// </summary>
    /// <param name="includeUnOfficial">Unofficial sources will be included in the results</param>
    /// <param name="includeDisabled">Disabled sources will be included in the results</param>
    /// <returns>Key: source name Value: source URI</returns>
    IEnumerable<KeyValuePair<string, string>> GetSources(bool includeUnOfficial, bool includeDisabled);

    /// <summary>
    /// Raised when sources are added, removed, disabled, or modified.
    /// </summary>
    event EventHandler SourcesChanged;
}
```

## <a name="ivspackageuninstaller-interface"></a><span data-ttu-id="34c6c-137">Interfaccia IVsPackageUninstaller</span><span class="sxs-lookup"><span data-stu-id="34c6c-137">IVsPackageUninstaller interface</span></span>

```cs
public interface IVsPackageUninstaller
{
    /// <summary>
    /// Uninstall the specified package from a project and specify whether to uninstall its dependency packages
    /// too.
    /// </summary>
    /// <param name="project">The project from which the package is uninstalled.</param>
    /// <param name="packageId">The package to be uninstalled</param>
    /// <param name="removeDependencies">
    /// A boolean to indicate whether the dependency packages should be
    /// uninstalled too.
    /// </param>
    void UninstallPackage(Project project, string packageId, bool removeDependencies);
}
```

## <a name="ivstemplatewizard-interface"></a><span data-ttu-id="34c6c-138">Interfaccia IVsTemplateWizard</span><span class="sxs-lookup"><span data-stu-id="34c6c-138">IVsTemplateWizard interface</span></span>

```cs
/// <summary>
/// Defines the logic for a template wizard extension.
/// </summary>

public interface IVsTemplateWizard : IWizard
{
}
```
