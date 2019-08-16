---
ms.assetid: 176A3794-E9E9-46C3-B242-422843436D2A
title: 異なるバージョンの Windows に対するドライバーのビルド
description: 以下のセクションでは、異なるバージョンの Windows に対するドライバーの作成をしている方のために、Windows Driver Kit (WDK) 8.1 か WDK 8、Visual Studio、MSBuild を使ってドライバーをビルドするためのガイドラインをいくつか紹介しています。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4ed6f801a077a40912921455f3c904721f09397
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370356"
---
# <a name="building-drivers-for-different-versions-of-windows"></a>異なるバージョンの Windows に対するドライバーのビルド

以下のセクションでは、[異なるバージョンの Windows に対するドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/platforms-and-driver-versions)をしている方のために、Windows Driver Kit (WDK) 8.1 か WDK 8、Visual Studio、MSBuild を使ってドライバーをビルドするためのガイドラインをいくつか紹介しています。

## <a name="span-idguidelines_that_apply_to_building_both_user-mode_and_kernel-mode_driversspanspan-idguidelines_that_apply_to_building_both_user-mode_and_kernel-mode_driversspanspan-idguidelines_that_apply_to_building_both_user-mode_and_kernel-mode_driversspanguidelines-that-apply-to-building-both-user-mode-and-kernel-mode-drivers"></a><span id="Guidelines_that_apply_to_building_both_user-mode_and_kernel-mode_drivers"></span><span id="guidelines_that_apply_to_building_both_user-mode_and_kernel-mode_drivers"></span><span id="GUIDELINES_THAT_APPLY_TO_BUILDING_BOTH_USER-MODE_AND_KERNEL-MODE_DRIVERS"></span>ユーザー モード ドライバーとカーネル モード ドライバーをビルドする際の共通のガイドライン


-   WDK に備わっているターゲット構成とプラットフォームを使ってドライバーをビルドします。 必ず、対象の Windows バージョンをサポートする最新バージョンの WDK を使ってください。 たとえば、ドライバーを Windows XP 用にビルドするには、Windows 7 WDK を使う必要があります。 一方、Windows 8.1、Windows 8、Windows 7 のいずれかを対象にドライバーをビルドする場合は、WDK 8.1 と Visual Studio を使います。
-   ドライバーの実行環境となる Windows のバージョンが 1 つしかない場合は、対象となる Windows バージョンのターゲット構成とプラットフォーム用にドライバーをビルドします。 たとえば、WDK 8.1 でのみ実行されるドライバーをビルドする場合は、構成マネージャーで **Win8.1** を指定します。
-   複数の Windows バージョンで実行する必要はあるものの、機能的には最も古いバージョンでよいという場合は、ドライバーでサポートする最古のバージョン用にドライバーをビルドします。 たとえば、Windows Vista 以降のすべての Windows バージョンでドライバーを動作させる場合で、なおかつ Windows Vista に装備されている機能のみを使う場合は、プロジェクトの構成で **Vista** を指定します。

## <a name="span-idguidelines_that_apply_to_building_kernel-mode_driversspanspan-idguidelines_that_apply_to_building_kernel-mode_driversspanspan-idguidelines_that_apply_to_building_kernel-mode_driversspanguidelines-that-apply-to-building-kernel-mode-drivers"></a><span id="Guidelines_that_apply_to_building_kernel-mode_drivers"></span><span id="guidelines_that_apply_to_building_kernel-mode_drivers"></span><span id="GUIDELINES_THAT_APPLY_TO_BUILDING_KERNEL-MODE_DRIVERS"></span>カーネル モード ドライバーをビルドする際のガイドライン


-   カーネル モード ドライバーを複数の Windows バージョンに対応させ、ドライバーから利用できる機能を動的に判断させる場合、最新バージョンのオペレーティング システム用のビルド構成を使ってドライバーをビルドします。 たとえば、Windows 7 以降のすべての Windows バージョンをサポートする一方で、ドライバーが Windows 8.1 以降のバージョンで実行されている場合には Windows 8.1 で新たに導入された特定の機能を利用できるようにするには、ターゲット構成として Windows 8.1 (**Win8.1**) を指定します。

-   ドライバーから利用できる Windows のバージョンを実行時に調べるには、[**RtlIsNtDdiVersionAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlisntddiversionavailable) 関数と [**RtlIsServicePackVersionInstalled**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlisservicepackversioninstalled) 関数を使います。 詳しくは、「[異なるバージョンの Windows に対するドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/platforms-and-driver-versions)」をご覧ください。
-   ドライバーから条件付きで呼び出す関数へのポインターのプロトタイプを作成します。
-   WDM ドライバーまたは非 KMDF カーネル モード ドライバーで、Windows 8.1 Preview や Windows 8 をターゲットとしながら、それ以前のバージョンの Windows でも動作させる必要がある場合は、リンカーの **$(KernelBufferOverflowLib)** オプションを上書きする必要があります。 Windows 8 または Windows 8.1 Preview の構成を選んだ場合、ドライバーは BufferOverflowFastFailK.lib とリンクされますが、これは以前のバージョンの Windows では利用できません。 Windows 7 と Vista では、BufferOverflowK.lib をリンクする必要があります。

    **$(KernelBufferOverflowLib)** リンカー オプションの上書きは、MSBuild または Visual Studio を使って行います。

    **MSBuild を使用:**

    ```cpp
    msbuild /p:KernelBufferOverflowLib="C:\Program Files (x86)\Windows Kits\8.1\Lib\win8\km\x64\BufferOverflowK.lib" /p:platform=x64 /p:Configuration="Win8 Release" myDriver.sln
    ```

    **Visual Studio を使用:**

    メモ帳などのテキスト エディターで、ドライバー プロジェクト ファイル (\*.vcxproj) を開きます。 プロジェクト ファイルで、ドライバーがサポートする構成の **&lt;PropertyGroup&gt;** を探して、次の行を追加し、既定のリンカー オプションを上書きします。

    <span codelanguage="XML"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">XML</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code> 
       &lt;KernelBufferOverflowLib&gt;$(DDK_LIB_PATH)\BufferOverflowK.lib&lt;/KernelBufferOverflowLib&gt;
    </code></pre></td>
    </tr>
    </tbody>
    </table>

    たとえば、ドライバーが Windows 8.1 と Windows 8 のデバッグ用ビルドとリリース用ビルドをサポートしている場合、構成セクションは次のようになります。

    <span codelanguage="XML"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">XML</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>  &lt;PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Win8.1 Debug|Win32'" Label="Configuration"&gt;
        &lt;TargetVersion&gt;WindowsV6.3&lt;/TargetVersion&gt;
        &lt;UseDebugLibraries&gt;true&lt;/UseDebugLibraries&gt;
        &lt;KernelBufferOverflowLib&gt;$(DDK_LIB_PATH)\BufferOverflowK.lib&lt;/KernelBufferOverflowLib&gt;
        &lt;PlatformToolset&gt;WindowsKernelModeDriver8.1&lt;/PlatformToolset&gt;
        &lt;ConfigurationType&gt;Driver&lt;/ConfigurationType&gt;
        &lt;DriverType&gt;KMDF&lt;/DriverType&gt;
      &lt;/PropertyGroup&gt;
      &lt;PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Win8.1 Release|Win32'" Label="Configuration"&gt;
        &lt;TargetVersion&gt;WindowsV6.3&lt;/TargetVersion&gt;
        &lt;UseDebugLibraries&gt;false&lt;/UseDebugLibraries&gt;
        &lt;KernelBufferOverflowLib&gt;$(DDK_LIB_PATH)\BufferOverflowK.lib&lt;/KernelBufferOverflowLib&gt;
        &lt;PlatformToolset&gt;WindowsKernelModeDriver8.1&lt;/PlatformToolset&gt;
        &lt;ConfigurationType&gt;Driver&lt;/ConfigurationType&gt;
        &lt;DriverType&gt;KMDF&lt;/DriverType&gt;
      &lt;/PropertyGroup&gt;
      &lt;PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Win8 Debug|Win32'" Label="Configuration"&gt;
        &lt;TargetVersion&gt;Windows8&lt;/TargetVersion&gt;
        &lt;UseDebugLibraries&gt;true&lt;/UseDebugLibraries&gt;
        &lt;KernelBufferOverflowLib&gt;$(DDK_LIB_PATH)\BufferOverflowK.lib&lt;/KernelBufferOverflowLib&gt;
        &lt;PlatformToolset&gt;WindowsKernelModeDriver8.1&lt;/PlatformToolset&gt;
        &lt;ConfigurationType&gt;Driver&lt;/ConfigurationType&gt;
        &lt;DriverType&gt;KMDF&lt;/DriverType&gt;
      &lt;/PropertyGroup&gt;
      &lt;PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Win8 Release|Win32'" Label="Configuration"&gt;
        &lt;TargetVersion&gt;Windows8&lt;/TargetVersion&gt;
        &lt;UseDebugLibraries&gt;false&lt;/UseDebugLibraries&gt;
        &lt;KernelBufferOverflowLib&gt;$(DDK_LIB_PATH)\BufferOverflowK.lib&lt;/KernelBufferOverflowLib&gt;
        &lt;PlatformToolset&gt;WindowsKernelModeDriver8.1&lt;/PlatformToolset&gt;
        &lt;ConfigurationType&gt;Driver&lt;/ConfigurationType&gt;
        &lt;DriverType&gt;KMDF&lt;/DriverType&gt;
      &lt;/PropertyGroup&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

    **&lt;KernelBufferOverflowLib&gt;** 要素は、ドライバー プロジェクト ファイル内で、ツールセットをインポートする Microsoft.Cpp.props をインポートする要素の前に配置する必要があります。

    ドライバー プロジェクト ファイルを変更および保存した後、Visual Studio でプロジェクト ファイルを開き、ドライバーをビルドすることができます。

## <span id="how_to_customize_target_configuration"></span><span id="HOW_TO_CUSTOMIZE_TARGET_CONFIGURATION"></span>


## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [異なるバージョンの Windows に対するドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/platforms-and-driver-versions)
* [ドライバーのビルド](building-a-driver.md)
 

 






