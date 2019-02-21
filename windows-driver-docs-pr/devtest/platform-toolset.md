---
title: プラットフォーム ツールセット
description: Windows Driver Kit (WDK) では、ツール、およびドライバーの開発に固有のライブラリを提供する MSBuild プラットフォーム ツールセットの機能を利用します。
ms.assetid: 9F585CA3-B863-408A-B785-2456460D6626
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbf72527e93fedd2f1865ea4dc246b34952e99e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549810"
---
# <a name="platform-toolset"></a>プラットフォーム ツールセット


Windows Driver Kit (WDK) では、ツール、およびドライバーの開発に固有のライブラリを提供する MSBuild プラットフォーム ツールセットの機能を利用します。 MSBuild プラットフォーム ツールセットの機能は、拡張可能です。 使用するプラットフォーム ツールセットの特定のバージョンと呼ばれる MSBuild プロパティによって制御される**PlatformToolset**します。 プロジェクトは、ツールとライブラリ間を設定して切り替えることができます、 **PlatformToolset**プロジェクト ファイルのプロパティ。

Windows Driver Kit (WDK) 8.1 では、ドライバーの開発の次のプラットフォーム ツールセットを提供します。

| **PlatformToolset** (WDK 8.1)       | 使用                                                                                                                                                                                                                                                                                                                                                                                         |
|-------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **WindowsKernelModeDriver8.1**      | カーネル モード ドライバーとコンポーネント。                                                                                                                                                                                                                                                                                                                                                     |
| **WindowsUserModeDriver8.1**        | ユーザー モード ドライバーとコンポーネント。                                                                                                                                                                                                                                                                                                                                                       |
| **WindowsApplicationForDrivers8.1** | アプリケーションの任意の種類。 このプラットフォーム ツールセットは、Windows Driver Kit (WDK) で Windows 7 (WDK 7.1) のために使用するビルド オプションとの互換性を提供し、またドライバーと対話するユーザー モード アプリケーションの開発の一般的な既定の設定を使用します。 WDK 7 を使用してビルドされたプロジェクトの変換または移行する場合は、この設定を使用する場合があります。 |
| **Visual Studio 2013 (v120)**       | あらゆる種類の Windows アプリケーション (既定値) に使用します。                                                                                                                                                                                                                                                                                                                                          |

 

Windows Driver Kit (WDK) 8 では、ドライバーの開発の次のプラットフォーム ツールセットが用意されています。 この情報は、参照のみ提供されます。

| **PlatformToolset** (WDK 8)         | 使用                                                                                                                                                                                                                                           |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **WindowsKernelModeDriver8.0**      | カーネル モード ドライバーとコンポーネント。                                                                                                                                                                                                       |
| **WindowsUserModeDriver8.0**        | ユーザー モード ドライバーとコンポーネント。                                                                                                                                                                                                         |
| **WindowsApplicationForDrivers8.0** | アプリケーションの任意の種類。 このプラットフォーム ツールセットは、WDK の Windows 7 (WDK 7.1) に使用するビルド オプションとの互換性を提供します。 WDK 7 を使用してビルドされたプロジェクトの変換または移行する場合は、この設定を使用する場合があります。 |
| **Visual Studio 2012 (v110)**       | あらゆる種類の Windows アプリケーション (既定値) に使用します。                                                                                                                                                                                            |

 

**注**  から Visual Studio で、使用可能な Windows ドライバー テンプレートのいずれかのドライバーを作成する場合、 **PlatformToolset**プロパティは自動的に設定します。 選択することも、 **PlatformToolset**ドライバー プロジェクトのプロパティ ページを Visual studio を使用しています。
**Visual Studio でのプラットフォーム ツールセットの設定**

1.  ドライバー プロジェクトのプロパティ ページを開きます。 **ソリューション エクスプローラー**でドライバー プロジェクトを右クリックして、**[プロパティ]** をクリックします。
2.  ドライバー プロジェクトのプロパティ ページで次のようにクリックします。**構成プロパティ**順にクリックします**全般**します。
3.  選択、**プラットフォーム ツールセット**ドロップダウン リストから、プロジェクトのプロパティ。

 

## <a name="span-idexample-settingtheplatformtoolsetpropertyinavisualstudioprojectfilevcxprojspanspan-idexample-settingtheplatformtoolsetpropertyinavisualstudioprojectfilevcxprojspanspan-idexample-settingtheplatformtoolsetpropertyinavisualstudioprojectfilevcxprojspanexample---setting-the-platformtoolset-property-in-a-visual-studio-project-file-vcxproj"></a><span id="Example_-_Setting_the_PlatformToolset_property_in_a_Visual_Studio_project_file__.vcxproj_"></span><span id="example_-_setting_the_platformtoolset_property_in_a_visual_studio_project_file__.vcxproj_"></span><span id="EXAMPLE_-_SETTING_THE_PLATFORMTOOLSET_PROPERTY_IN_A_VISUAL_STUDIO_PROJECT_FILE__.VCXPROJ_"></span>例 - 設定、 **PlatformToolset** Visual Studio プロジェクト ファイル (.vcxproj) のプロパティ


次の例は、どのように**PlatformToolset**プロパティは、プロジェクト ファイルで設定します。

```XML
<PropertyGroup Condition="&#39;$(Configuration)|$(Platform)&#39;==&#39;Debug|Win32&#39;"
      Label="Configuration">
  <ConfigurationType>Driver</ConfigurationType>
  <DriverType>KMDF</DriverType>
  <PlatformToolset>WindowsKernelModeDriver8.1</PlatformToolset>
</PropertyGroup>
```

**ConfigurationType**プロパティは、ターゲットの拡張機能とが構築されるバイナリの出力の種類を制御します。 このプロパティの値の一部は**アプリケーション**、 **dynamiclibrary など**、 **StaticLibrary**、および**ユーティリティ**します。

WDK と呼ばれるこのプロパティの新しい値を導入する**ドライバー**カーネル モード ドライバーをビルドします。 このプロパティを設定する場合**ドライバー**MSBuild の拡張機能として .sys のドライバー ファイルが生成されます。 例では、 **PlatformToolset**プロパティに設定されて**WindowsKernelModeDriver8.1**カーネル モード ドライバーをビルドします。 **WindowsKernelModeDriver8.1**のみ WDK プラットフォーム ツールセットが必要なは、 **DriverConfigurationType**します。 この例で、 **DriverType** KMDF に設定されます。

## <a name="span-idabouttheplatformtoolsetpropertyfordriversspanspan-idabouttheplatformtoolsetpropertyfordriversspanspan-idabouttheplatformtoolsetpropertyfordriversspanabout-the-platformtoolset-property-for-drivers"></a><span id="About_the_PlatformToolset_property_for_drivers"></span><span id="about_the_platformtoolset_property_for_drivers"></span><span id="ABOUT_THE_PLATFORMTOOLSET_PROPERTY_FOR_DRIVERS"></span>について、 **PlatformToolset**ドライバーのプロパティ


**PlatformToolset**プロパティ シート、ターゲット、ツール、および拡張ドライバーまたはその特定のプラットフォーム用のカーネル モード コンポーネントをビルドするには、プラットフォームを変更し連携するタスクのセットです。 ドライバーと関連コンポーネント、およびアプリケーションの**PlatformToolset**にプロパティを設定する必要があります**WindowsKernelModeDriver8.1**、 **WindowsUserModeDriver8.1**、または**WindowsApplicationForDrivers8.1**プロジェクト ファイル。 これらのプラットフォーム ツールセットは、既存の Visual Studio C を拡張するように設計\\ツール チェーンの C++ コンパイラとリンカーの他の WDK に固有のビルド ツールとターゲット WDK ヘッダーとライブラリ。 **WindowsApplicationForDrivers8.1**ツールセットは、WDK の Windows 7 (WDK 7.1) で使用可能になったオプション設定のビルドとの互換性を提供します、また、既定の設定をユーザー モードの開発の一般的なドライバーと対話するアプリケーション。

**プラットフォーム ツールセット**ドライバー プロジェクトのビルドを既定のプラットフォーム レベルの設定とターゲット。 Unicode または ANSI の文字列を使用して、ドライバーのプロジェクトをビルドするときに設定するには、コンパイラやリンカーなどのビルド ツール、システムについては、WDK のインクルードまたはライブラリのパスなど、さまざまなプロパティなどの機能設定の既定のスイッチを使用します。 デスクトップ用の Windows アプリケーションを開発している場合は使用しないで、 **WindowsKernelModeDriver8.1**、 **WindowsUserModeDriver8.1**、または**WindowsApplicationForDrivers8.1**プラットフォーム ツールセットです。 代わりに、使用、 **Visual Studio 2013 (v120)** プラットフォーム ツールセットです。

既定で、 **PlatformToolset**プロパティは**Visual Studio 2013 (v120)** 新しく作成された Win32 ユーザー モードの C++ のプロジェクトと Visual Studio 2013 に変換されたプロジェクトの両方にします。 どちらの場合で、 **PlatformToolset**プロパティは、プロジェクト ファイルに書き込まれません。

ドライバーのプラットフォーム ツールセットのいずれかを選択すると、次のプロパティが設定されます。

-   ExecutablePath と NativeExecutablePath (パス)
-   インクルード パス (INCLUDE)
-   ReferencePath (ライブラリのパス)
-   LibraryPath (LIB)
-   SourcePath
-   ExcludedPath

**注**  とき**UseEnv**に設定されていない**TRUE**パス、LIB、INCLUDE、LIBPATH、プラットフォーム ツールセットに対応するプロパティ値から設定されます。 ときに**UseEnv**に設定されている**TRUE**システムを構築すると、以前のように、PATH、INCLUDE、LIB、LIBPATH および用の環境変数から値が代わりに使用されます。

 

## <a name="span-idwherethewdkinstallsfilesthatenablethedriver-specificplatformtoolsetsspanspan-idwherethewdkinstallsfilesthatenablethedriver-specificplatformtoolsetsspanspan-idwherethewdkinstallsfilesthatenablethedriver-specificplatformtoolsetsspanwhere-the-wdk-installs-files-that-enable-the-driver-specific-platform-toolsets"></a><span id="Where_the_WDK_installs_files_that_enable_the_driver-specific_platform_toolsets"></span><span id="where_the_wdk_installs_files_that_enable_the_driver-specific_platform_toolsets"></span><span id="WHERE_THE_WDK_INSTALLS_FILES_THAT_ENABLE_THE_DRIVER-SPECIFIC_PLATFORM_TOOLSETS"></span>WDK がドライバー固有のプラットフォーム ツールセットを有効にするファイルがインストールされます。


次の表では、WDK がドライバーの開発のプラットフォーム ツールセットを有効にするファイルをインストールする場所をまとめたものです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パス変数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>$ (Vctargetspath)</p></td>
<td align="left"><p>$(MSBuildExtensionsPath) としてレジストリに既定では、$ (vctargetspath) が定義されている&lt;em&gt;&lt;フォルダー&gt;</em>&amp;lt;MSBUILDSYNTAXVERSION&gt;)</p>
<p>新しい構文があり、後で MSBuild が必要ですが、同じプラットフォームの新しいビルド プロセスが使用される場合に、バージョン番号が含まれます。</p>
<p><em>&lt;フォルダー&gt;</em> は、 <strong>Microsoft.Cpp</strong>フォルダー - $(MSBuildExtensionsPath)\Microsoft.Cpp\4.0\v120 します。</p>
<p>これは呼び出されます<em>構文バージョン</em>なく<em>ツール バージョン</em>します。 1 つ目のアセンブリのバージョンは<strong>Microsoft.Build.Engine</strong>すべての必要な構文をサポートします。 <strong>Microsoft.Cpp</strong>プラットフォームを Visual Studio を検索する場所のみフォルダーを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>$(VCTargetsPath) \Platforms$ (プラットフォーム) \ImportAfter<em>.props</p></td>
<td align="left"><p>ファイルが通常含まれていない省略可能なフォルダーです。 このフォルダーに MSBuild 形式のファイルを保存することによって、プラットフォームをカスタマイズできます。 現在のフォルダーが示すとおり、プラットフォームの設定ファイルの下部にインポートされます。 この場所からファイルをインポートする順序は定義されません。 MSBuild を作成するファイルは、$(VCTargetsPath) \Platforms$ (プラットフォーム) \ImportAfter\Microsoft.Cpp です。<em>&lt;プラットフォーム&gt;</em>します。WindowsKernelModeDriver8.1.props Microsoft.Cpp.<em>&lt;プラットフォーム&gt;</em>します。WindowsUserModeDriver8.1.props WDK に固有のいくつかの props ファイルをインポートします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>$(VCTargetsPath)\Platforms$(Platform)\PlatformToolsets$(PlatformToolset)&lt;/p&gt;</td>
<td align="left"><p>WDK: の</p>
<p><strong>$(PlatformToolset)</strong>に設定する必要があります<strong>WindowsKernelModeDriver8.1</strong>カーネル モード ドライバーを構築するために設定します<strong>WindowsUserModeDriver8.1</strong>ユーザー モードを構築するため。ドライバー、および設定する<strong>WindowsApplicationForDrivers8.1</strong> Windows 7 の WDK (WDK 7) で使用されるビルド オプションとの互換性。</p>
<p><strong>PlatformToolset ディレクトリ</strong></p>
<p>たとえば、C:\Program Files\MSBuild\Microsoft.Cpp\v4.0\v120\Platforms\Win32\PlatformToolsets\WindowsKernelModeDriver8.1 します。</p>
<p>PlatformToolsets ディレクトリでは、独自のサブフォルダーにファイルを後で – の他の種類を追加できます。</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left"><p>Microsoft.Cpp.$ (プラットフォーム). $(PlatformToolset) .props</p></td>
<td align="left"><p><strong>プラットフォーム ツールセットの Props ファイル</strong></p>
<p>ドライバーをビルドする props ファイルをインポートします。 また v120 props ファイルをインポートします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Microsoft.Cpp.$ (プラットフォーム). $(PlatformToolset) .targets</p></td>
<td align="left"><p><strong>プラットフォーム ツールセットのターゲット ファイル</strong></p>
<p>インポート対象に、ドライバーをビルドするファイル。 これらのファイルを含む&lt;UsingTask&gt; WDK タスクをプルするタグ。 この機能は、また v120 ターゲットをインポートします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>$(WDKContentRoot)\build</em>.props</p></td>
<td align="left"><p>すべてのドライバー固有の props ファイル。 これらのファイルには、ドライバーをビルドする既定の設定が含まれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>$(WDKContentRoot)\build*.targets</p></td>
<td align="left"><p>すべてのドライバーの特定のターゲット ファイルです。 このファイルは、ドライバーをビルドするターゲットを指定します。</p></td>
</tr>
</tbody>
</table>

 

 

 





