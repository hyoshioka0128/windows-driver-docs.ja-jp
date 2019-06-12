---
title: Windows ドライバー固有のプロパティ ファイル
description: ドライバーのプロパティ シートでは、すべてのドライバー プロジェクトのビルドに MSBuild を使用するツールの既定の設定があります。
ms.assetid: 696EE510-266B-457A-B74E-491D7804B833
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4c5c533f07d452e2fdba722b40a6bf1f8607773
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379140"
---
# <a name="span-iddevtestwindowsdriver-specificpropertyfilesspanwindows-driver-specific-property-files"></a><span id="devtest.windows_driver-specific_property_files"></span>Windows ドライバー固有のプロパティ ファイル


ドライバーのプロパティ シートでは、すべてのドライバー プロジェクトのビルドに MSBuild を使用するツールの既定の設定があります。

次の表は、これらのプロパティ シートとさまざまなドライバーをビルドする MSBuild を使用する既定の設定の観点からは、その使用を示します。

**注**  などで、Windows Driver Kit (WDK) 8 では、名前のドライバーのプロパティ シート ファイルにキットのバージョン番号 (8.0) が含まれている**WindowsDriver8.0.KernelMode.ExportDriver.props**します。

 

<span id="__WDKContentRoot_"></span><span id="__wdkcontentroot_"></span><span id="__WDKCONTENTROOT_"></span> **$(WDKContentRoot)**  
レジストリに既定では、WDKContentRoot が定義されている: <strong>$(レジストリ: HKEY\_ローカル\_マシン\\ソフトウェア\\Microsoft\\Windows キット\\WDK@WDKContentRoot)</strong>を表しています * *%programfiles%\\Windows キット\\* バージョン * * *。

$(WDKContentRoot)\\ビルドでビルド拡張機能ドライバーをビルドするために必要なすべてのコアが必要があります。

<span id="WindowsDriver.Default.props"></span><span id="windowsdriver.default.props"></span><span id="WINDOWSDRIVER.DEFAULT.PROPS"></span>**WindowsDriver.Default.props**  
任意のドライバーによって使用されているバージョン管理の定数を定義します。 たとえば、  **&lt; \_NT\_ターゲット\_バージョン\_WIN7&gt;0x0601&lt;/\_NT\_ターゲット\_バージョン\_WIN7&gt;** します。

<span id="WindowsDriver.Common.props"></span><span id="windowsdriver.common.props"></span><span id="WINDOWSDRIVER.COMMON.PROPS"></span>**WindowsDriver.Common.props**  
-カーネル モードとユーザー モードの両方のすべてのドライバーをビルドに必要な一般的な設定です。

<span id="WindowsDriver.Shared.props"></span><span id="windowsdriver.shared.props"></span><span id="WINDOWSDRIVER.SHARED.PROPS"></span>**WindowsDriver.Shared.props**  
このプロパティのファイルには、ドライバーとアプリケーションを構築するために必要な共有のビルド設定が含まれています。 このファイルは、すべての WDK ツールセット、WindowsKernelModeDriver8.1、WindowsUserModeDriver8.1、および WindowsApplicationForDrivers8.1 などで使用されます。

<span id="WindowsDriver.__Platform_.props"></span><span id="windowsdriver.__platform_.props"></span><span id="WINDOWSDRIVER.__PLATFORM_.PROPS"></span>**WindowsDriver $(プラットフォーム) の .props。**  
これらの設定は、MSBuild のターゲット アーキテクチャに応じてが適用される一般的なドライバーの設定です。 **$(プラットフォーム) Win32 を = | x64**

<span id="WindowsDriver.KernelMode.props"></span><span id="windowsdriver.kernelmode.props"></span><span id="WINDOWSDRIVER.KERNELMODE.PROPS"></span>**WindowsDriver.KernelMode.props**  
このプロパティ ファイルは、カーネル モード バイナリのみをビルドに必要な一般的な設定。 つまり、これらの設定は、ユーザー モード ドライバーとアプリケーションに適用されません。

<span id="WindowsDriver.KernelMode.Driver.props"></span><span id="windowsdriver.kernelmode.driver.props"></span><span id="WINDOWSDRIVER.KERNELMODE.DRIVER.PROPS"></span>**WindowsDriver.KernelMode.Driver.props**  
このプロパティのファイルは、特定のカーネル モード ドライバーの種類プロパティ ファイル (たとえば、WindowsDriver.8.1.KernelMode.KMDF.props) をインポートします。

<span id="WindowsDriver.KernelMode.KMDF.props"></span><span id="windowsdriver.kernelmode.kmdf.props"></span><span id="WINDOWSDRIVER.KERNELMODE.KMDF.PROPS"></span>**WindowsDriver.KernelMode.KMDF.props**  
これらのプロパティ設定は、KMDF ドライバーをビルドする場合にのみ適用する必要がある特別な設定を含めます。 MSBuild を使用して、 **$(DriverType)** としてドライバーの種類を指定するプロパティ**KMDF**、次の例。 *&lt;DriverType&gt;KMDF&lt;/DriverType&gt;*

<span id="WindowsDriver.KernelMode.Wdm.props"></span><span id="windowsdriver.kernelmode.wdm.props"></span><span id="WINDOWSDRIVER.KERNELMODE.WDM.PROPS"></span>**WindowsDriver.KernelMode.Wdm.props**  
これらのプロパティ設定は、WDM ドライバーをビルドする場合にのみ適用する必要がある特別な設定を含めます。 MSBuild を使用して、 **$(DriverType)** としてドライバーの種類を指定するプロパティ**WDM**、次の例。 *&lt;DriverType&gt;wdm&lt;/DriverType&gt;* します。

<span id="WindowsDriver.KernelMode.Gdidriver.props"></span><span id="windowsdriver.kernelmode.gdidriver.props"></span><span id="WINDOWSDRIVER.KERNELMODE.GDIDRIVER.PROPS"></span>**WindowsDriver.KernelMode.Gdidriver.props**  
これらのプロパティ設定は、GDI ドライバーをビルドする場合にのみ適用する必要がある特別な設定を含めます。 MSBuild を使用して、 **$(DriverType)** としてドライバーの種類を指定するプロパティ**Gdidriver**、次の例。 *&lt;DriverType&gt;Gdidriver&lt;/DriverType&gt;* します。

<span id="WindowsDriver.KernelMode.ExportDriver.props"></span><span id="windowsdriver.kernelmode.exportdriver.props"></span><span id="WINDOWSDRIVER.KERNELMODE.EXPORTDRIVER.PROPS"></span>**WindowsDriver.KernelMode.ExportDriver.props**  
これらのプロパティ設定には、エクスポートされたドライバーをビルドする場合にのみ適用する必要がある特別な設定が含まれて。 MSBuild を使用して、 **$(DriverType)** としてドライバーの種類を指定するプロパティ**ExportDriver**、次の例。 *&lt;DriverType&gt;ExportDriver&lt;/DriverType&gt;* します。

<span id="WindowsDriver.KernelMode.Miniport.props"></span><span id="windowsdriver.kernelmode.miniport.props"></span><span id="WINDOWSDRIVER.KERNELMODE.MINIPORT.PROPS"></span>**WindowsDriver.KernelMode.Miniport.props**  
これらのプロパティ設定は、ミニポート ドライバーをビルドするときに適用する必要がある特別な設定です。 MSBuild を使用して、 **$(DriverType)** としてドライバーの種類を指定するプロパティ**ミニポート**、次の例。 *&lt;DriverType&gt;ミニポート&lt;/DriverType&gt;* します。

<span id="WindowsDriver.LateEvaluation.props_"></span><span id="windowsdriver.lateevaluation.props_"></span><span id="WINDOWSDRIVER.LATEEVALUATION.PROPS_"></span>**WindowsDriver.LateEvaluation.props**   
内部使用のみです。 編集したり、使用しないでください。

<span id="WindowsDriver.masm.props"></span><span id="windowsdriver.masm.props"></span><span id="WINDOWSDRIVER.MASM.PROPS"></span>**WindowsDriver.masm.props**  
これらのプロパティ設定には、サポートされているアーキテクチャ (プラットフォーム) のアセンブリ ファイル (MASM) を構築するための設定が含まれます。

<span id="WindowsDriver.UserMode.props"></span><span id="windowsdriver.usermode.props"></span><span id="WINDOWSDRIVER.USERMODE.PROPS"></span>**WindowsDriver.UserMode.props**  
これらのプロパティ設定は、任意のユーザー モード ドライバーのみをビルドするために必要な一般的な設定です。 つまり、カーネル モード ドライバーとアプリケーションのこれらの設定は適用されません。

<span id="WindowsDriver.UserMode.UMDF"></span><span id="windowsdriver.usermode.umdf"></span><span id="WINDOWSDRIVER.USERMODE.UMDF"></span>**WindowsDriver.UserMode.UMDF**  
これらのプロパティ設定は、UMDF ドライバーをビルドするときに適用する必要がある特別な設定です。 MSBuild を使用して、 **$(DriverType)** としてドライバーの種類を指定するプロパティ**UMDF**、次の例。 *&lt;DriverType&gt;UMDF&lt;/DriverType&gt;* します。

 

 





