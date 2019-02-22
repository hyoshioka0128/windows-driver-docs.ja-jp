---
title: ProjectUpgradeTool
description: ProjectUpgradeTool は Microsoft Visual Studio 2012 プロジェクト (*.vcxproj) ファイルとソリューション ファイル (*.sln) for Windows 8 と Windows Driver Kit (WDK) に作成され、Windows 8.1 の WDK で動作するようにアップグレードしてMicrosoft Visual Studio 2013。
ms.assetid: DEB7799C-D505-40E6-B2B0-CF774A99B1BE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 721587fdeadc05d616f68b66aadb381ab87ea207
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536794"
---
# <a name="projectupgradetool"></a>ProjectUpgradeTool


ProjectUpgradeTool は Microsoft Visual Studio 2012 プロジェクト (\*.vcxproj) ファイルとソリューション ファイル (\*.sln) for Windows 8 と Windows Driver Kit (WDK) に作成され、Windows 8.1 の WDK で動作するようにアップグレードしてMicrosoft Visual Studio 2013。

**重要な**ProjectUpgradeTool では、ソース ファイルは変更されません。 このツールには、プロジェクトとソリューション ファイルのみに変換します。 既定では、ツールは、元のファイルのバックアップ コピーを保存します。



**WDK 8 のプロジェクトまたはソリューションを WDK 8.1 にアップグレードするには**

1.  Visual Studio のコマンド プロンプト ウィンドウを開きます。
2.  コマンドを入力して**ProjectUpgradeTool**ルート (または親) に Windows 8.1 用に、Windows Driver Kit (WDK) 8.1 をアップグレードする Windows Driver Kit (WDK) 8 プロジェクトまたはソリューション ファイルを含むディレクトリを指定します。 次のコマンドが c: すべてのファイルをアップグレードするなど、\\myDriver ディレクトリとサブディレクトリ。

    ```
    ProjectUpgradeTool.exe  C:\myDriver
    ```

3.  Visual Studio 2013 を使用して WDK 8.1 プロジェクトまたはソリューション ファイルを開きます。 このツールは、ファイルの元の名前を保持します。 以前のバージョンは、.backup ファイル名拡張子で保存されます。
    **注**できるように Windows Vista のターゲットをビルドする場合は、Visual Studio 2013 と WDK 8.1 の場合を使用して参照してください[WDK 8 プロジェクトを WDK 8.1 に移行した後、Windows Vista のターゲットをビルドできるようにする場合の対処](#build-vista-with-wdk-8-1)します。



## <a name="span-idprojectupgradetoolsyntaxspanspan-idprojectupgradetoolsyntaxspanspan-idprojectupgradetoolsyntaxspanprojectupgradetool-syntax"></a><span id="ProjectUpgradeTool_Syntax"></span><span id="projectupgradetool_syntax"></span><span id="PROJECTUPGRADETOOL_SYNTAX"></span>ProjectUpgradeTool 構文


プロジェクトのアップグレード ツールは %windowssdkdir にある\\bin\\x86\\ディレクトリ。 たとえば、c:\\Program Files (x86)\\Windows キット\\8.1\\bin\\x86。

ProjectUpgradeTool.exe では、次の構文があります。

```
ProjectUpgradeTool.exe  < rootDir >
                          [-Log:[<LogFile>]:[<Verbosity>]]
                          [-ConsoleLog:<Verbosity>]
                          [-NoBackup]
                          [-NoToolsetUpgrade]
                          [-InPlaceUpgrade]
                          [-ForceUpgrade]
                          [-KeepObsoleteConfigs]   
```

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-Log:</strong><em>&lt;LogFile&gt;</em><strong>:[</strong><em>&lt;Verbosity&gt;</em><strong>]</strong></p></td>
<td align="left"><p>ログ ファイルの名前を指定し、ログ記録のレベルを指定します (を参照してください<em>詳細度</em>)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-ConsoleLog:</strong><em>&lt;詳細度&gt;</em></p></td>
<td align="left"><p>コンソールのログ ファイルの名前を指定し、ログ記録のレベルを指定します (を参照してください<em>詳細度</em>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>詳細度</em></p></td>
<td align="left"><p>ログ ファイルとコンソールのログ記録の既定のログ記録レベルは<strong>Verbose</strong>と<strong>情報</strong>それぞれします。 <em>詳細度</em>の 1 つ<strong>System.Diagnostics.SourceLevels</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-バックアップ</strong></p></td>
<td align="left"><p>元のプロジェクト (.vcxproj) またはソリューション (.sln) のバックアップ コピーしないように ProjectUpgradeTool に指示します。 このオプションを選択して元のプロジェクトとソリューション ファイルは上書きは、WDK の Windows 8.1 と Visual Studio 2013 でのみ機能します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-NoToolsetUpgrade</strong></p></td>
<td align="left"><p>指定、 <strong>- NoToolsetUpgrade</strong> Windows 8.1 より前の Windows バージョンのビルド構成を指定する場合は、WDK 8.1 プラットフォームのツールセットを使用したくない場合はオプションです。 このオプションのみを選択すると、 <strong>WinPreRel</strong>構成は、最新の WDK を使用して構築します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-InPlaceUpgrade</strong></p></td>
<td align="left"><p>新しいすべて既存のビルド構成と置き換わります<strong>WinPreRel</strong>構成します。 こうと、以前のバージョンの Windows 向けのビルドから。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-ForceUpgrade</strong></p></td>
<td align="left"><p>プロジェクトがドライバーのプロジェクトの要件を満たしていない場合でも、アップグレードするすべてのプロジェクト ファイル (.vcxproj) を強制します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-KeepObsoleteConfigs</strong></p></td>
<td align="left"><p>WDK (たとえば、Windows Vista) ではサポートされなくなったオペレーティング システム用のターゲット構成を保持します。 ただし、これらの古いターゲットをビルドするにして、Visual Studio 2012 および WDK 8 WDK 8.1 と Visual Studio 2013 だけでなく、コンピューターにインストールされている必要があります。 たとえば、すべてのサポートされているターゲット バージョン (Windows 7、Windows 8 および Windows 8.1) WDK 8.1 を使用するドライバーのプロジェクトをアップグレードするとします。 まだ同じドライバーのプロジェクトを使用して、Windows Vista の開発を続けたいとします。 使用して、プロジェクト ファイルをアップグレードするには、 <strong>- KeepObsoleteConfigs</strong>プロジェクトのターゲットの構成を Windows Vista を保持するオプション。 Windows Vista の構成を引き続き使用、 <strong>WindowsKernelModeDriver8.0</strong> Visual Studio 2013 でプロジェクトをビルドする場合でも、ツール セット (WDK 8 で使用可能)。</p></td>
</tr>
</tbody>
</table>



## <a name="span-idcommentsspanspan-idcommentsspanspan-idcommentsspancomments"></a><span id="Comments"></span><span id="comments"></span><span id="COMMENTS"></span>コメント


-   [エラー MSB8020 を表示する場合の対処 (プラットフォーム ツールセット = 'WindowsKernelModeDriver8.0') が見つかりません](#what-to-do-if-you-see-error-msb8020)
-   [WDK 8 プロジェクトを WDK 8.1 に移行した後、Windows Vista のターゲットをビルドできるようにする場合の対処方法](#build-vista-with-wdk-8-1)

### <span id="What_to_do_if_you_see_Error_MSB8020__Platform_Toolset____WindowsKernelModeDriver8.0___cannot_be_found_"></span><span id="what_to_do_if_you_see_error_msb8020__platform_toolset____windowskernelmodedriver8.0___cannot_be_found_"></span><span id="WHAT_TO_DO_IF_YOU_SEE_ERROR_MSB8020__PLATFORM_TOOLSET____WINDOWSKERNELMODEDRIVER8.0___CANNOT_BE_FOUND_"></span><a name="what-to-do-if-you-see-error-msb8020"></a>エラー MSB8020 を表示する場合の対処 (プラットフォーム ツールセット = 'WindowsKernelModeDriver8.0') が見つかりません

WDK 8 で作成されたソリューションまたはプロジェクトを開くしようとした場合、WDK 8.1 を使用してプロジェクトをビルドしようとしたときに、次のエラー メッセージを表示もあります。

```
1>C:\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\V120\Microsoft.Cpp.Platform.targets(54,5): error MSB8020: The builds tools for WindowsKernelModeDriver8.0 (Platform Toolset = 'WindowsKernelModeDriver8.0') cannot be found. To build using the WindowsKernelModeDriver8.0 build tools, please install WindowsKernelModeDriver8.0 build tools. Alternatively, you may update to the current Visual Studio tools by selecting the Project menu or right-click the solution, and then selecting "Update VC++ Projects...".
```

WDK 8 でプラットフォーム ツールセットが**WindowsKernelModeDriver8.0**します。 このエラーを解決するには、実行、ProjectUpgradeTool の説明に従ってここと WDK 8 WDK 8.1 で使用できるツールセットを使用するソリューションをアップグレード

### <span id="build_vista_with_WDK_8.1"></span><span id="build_vista_with_wdk_8.1"></span><span id="BUILD_VISTA_WITH_WDK_8.1"></span><a name="build-vista-with-wdk-8-1"></a>WDK 8 プロジェクトを WDK 8.1 に移行した後、Windows Vista のターゲットをビルドできるようにする場合の対処方法

**問題:** WDK 8 プロジェクトを WDK 8.1 に移行した後、Windows Vista のターゲットをビルドできません。

**シナリオ:** WDK 8 と Visual Studio 2012 を使用してプロジェクトを作成しました。 WDK 8.1 と ProjectUpgradeTool ツールを使用して、Visual Studio 2013 を使用してプロジェクト/ソリューションをアップグレードしました。 これを行う、Windows Vista の構成を保持するために、次のコマンドを使用します。**ProjectUpgradeTool.exe** *PathToProjectFolder* **-KeepObsoleteConfigs.**

WDK 8.1 では、プロジェクトを開きます。 Win32 Windows Vista のターゲットをビルドするときに、次のエラー メッセージを参照してください可能性があります。

```
error MSB6004: The specified task executable location "C:\Program Files (x86)\Windows Kits\8.0\bin\x86\x86\CL.exe" is invalid.   C:\Program Files (x86)\MSBuild\Microsoft.Cpp\v4.0\V110\Microsoft.CppCommon.targets  347 5   KMDF Driver1
```

ビルドする場合は、x64 Windows Vista ターゲットでは、次のエラー メッセージを表示する場合があります。

```
error TRK0002: Failed to execute command: ""C:\Program Files (x86)\Windows Kits\8.0\bin\x64\stampinf.exe" -d * -a amd64 -v * -k 1.11 -u 1.11.0 -f x64\VistaRelease\KMDFDriver1.inf". The operation identifier is not valid.  C:\Users\Administrator\Desktop\KMDF Driver1 - Copy\KMDF Driver1\TRACKER KMDF Driver1
```

```
error : Verification Error: Driver package has no driver version.    C:\Program Files (x86)\Windows Kits\8.0\build\WindowsDriver8.0.common.targets   1338    5   KMDF Driver1 Package
```

**対応策 :** 2 つの変更を加える必要があります。

1.  **WindowsDriver8.0.x64.props と WindowsDriver8.0.Win32.props ファイルを修正します。**

    2 つの条件付きの式では、これらの修正を行う必要があります\*.props ファイル。 ファイルが c: である\\Program Files (x86)\\Windows キット\\8.0\\ビルド ディレクトリ。

    各\*.props ファイルで、式の検索場所`('$(VisualStudioVersion)' != '11.0')`。 たとえば、最初のインスタンスは、次のようになります。

    ```XML
            <When  Condition="&#39;$(VisualStudioVersion)&#39; != &#39;11.0&#39;">
          <PropertyGroup>
            <CLToolPath Condition="&#39;$(CLToolPath)&#39; == &#39;&#39;">$(WDKContentRoot)bin\x86\x64</CLToolPath>
            <CLToolArchitecture>Native32Bit</CLToolArchitecture>
            <LinkToolPath Condition="&#39;$(LinkToolPath)&#39; == &#39;&#39;">$(WDKContentRoot)bin\x86\x64</LinkToolPath>
            <LinkToolArchitecture>Native32Bit</LinkToolArchitecture>
            <MIDLToolPath Condition="&#39;$(MIDLToolPath)&#39; == &#39;&#39;">$(WDKContentRoot)bin\x86</MIDLToolPath>
            <MIDLToolArchitecture>Native32Bit</MIDLToolArchitecture>
            <LibToolPath Condition="&#39;$(LibToolPath)&#39; == &#39;&#39;">$(WDKContentRoot)bin\x86</LibToolPath>
            <LibToolArchitecture>Native32Bit</LibToolArchitecture>
            <ExecutablePath>$(WDKContentRoot)bin\x86\x64;$(WDKContentRoot)bin\x86;$(WDKContentRoot)tools\pfd\bin\bin\AMD64;$(WDKContentRoot)tools\tracing\x64;$(ExecutablePath)</ExecutablePath>      
        </PropertyGroup>
        </When>
    ```

    変更は、不等号 (! =) をより小さい ("&lt;")。

    ```XML
        <When  Condition="&#39;$(VisualStudioVersion)&#39; &lt;&#39;11.0&#39;">
    ```

    式の次のインスタンスを検索する場所 `('$(VisualStudioVersion)' != '11.0')`

    ```XML
        <When Condition="(&#39;$(PlatformToolset)&#39; == &#39;WindowsApplicationForDrivers8.0&#39;) and (&#39;$(VisualStudioVersion)&#39; != &#39;11.0&#39;)">
    ```

    変更は、不等号 (! =) をより小さい ("&lt;")。

    ```XML
        <When Condition="(&#39;$(PlatformToolset)&#39; == &#39;WindowsApplicationForDrivers8.0&#39;) and (&#39;$(VisualStudioVersion)&#39; &lt;&#39;11.0&#39;)">
    ```

    変更を行った後は保存両方\*.props ファイル。

2.  **ドライバーのプロジェクト ファイルを修正します。**

    プロジェクト ファイルを開きます (\*.vcxproj) は、ドライバーの。

    プロジェクト ファイル (リリースおよびデバッグ) では、Vista 対象となる構成を見つけます。 次に、例を示します。

    ```XML
       <PropertyGroup Label="Configuration" Condition="&#39;$(Configuration)|$(Platform)&#39;==&#39;Vista Debug|Win32&#39;">
        <TargetVersion>Vista</TargetVersion>
        <UseDebugLibraries>True</UseDebugLibraries>
        <PlatformToolset>WindowsKernelModeDriver8.0</PlatformToolset>
      </PropertyGroup>
    ```

    追加、 **PackageDir**プロパティを Windows Vista の構成設定にします。 ほとんどの状況では、既定値を使用する必要があります:`<PackageDir>$(OutDir)\$(Intdir)</PackageDir>`します。

    ```XML
       <PropertyGroup Label="Configuration" Condition="&#39;$(Configuration)|$(Platform)&#39;==&#39;Vista Debug|Win32&#39;">
        <TargetVersion>Vista</TargetVersion>
        <PackageDir>$(OutDir)\$(Intdir)</PackageDir>
        <UseDebugLibraries>True</UseDebugLibraries>
        <PlatformToolset>WindowsKernelModeDriver8.0</PlatformToolset>
      </PropertyGroup>
    ```

    その他の構成と同じ変更を加えます。

    ```XML
        <PropertyGroup Label="Configuration" Condition="&#39;$(Configuration)|$(Platform)&#39;==&#39;Vista Release|Win32&#39;">
        <TargetVersion>Vista</TargetVersion>
        <PackageDir>$(OutDir)\$(Intdir)</PackageDir>
        <UseDebugLibraries>False</UseDebugLibraries>
        <PlatformToolset>WindowsKernelModeDriver8.0</PlatformToolset>
      </PropertyGroup>
    ```

    これらを変更して、ファイルを保存した後を開くし、Visual Studio 2013 でプロジェクトをビルドします。 プロジェクトは、Visual Studio 2012 での作業を続ける必要があります。 これらの変更後にする必要があります WDK 8 があるし、コンピューターにインストールされている Visual Studio 2012 に注意してください。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ドライバーの構築](https://msdn.microsoft.com/windows-drivers/develop/building_a_driver)

[WDK と Visual Studio のビルド環境](wdk-and-visual-studio-build-environment.md)










