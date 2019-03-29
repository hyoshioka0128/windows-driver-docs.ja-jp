---
title: Nmake2MsBuild
description: Nmake2MsBuild ユーティリティでは、ドライバーがドライバーのソース コード ファイル、および変換元、ディレクトリ、および makefile.inc ファイルから以前のバージョンの WDK を使用して構築された Visual Studio プロジェクトが生成されます。
ms.assetid: D6E1C124-9A5F-486B-865E-45A0BC58A5A3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b896b9147b2e5470c27992cad01a6fd1d766952
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349425"
---
# <a name="nmake2msbuild"></a>Nmake2MsBuild


**注**Nmake2MsBuild ツールは、Windows 10、バージョン 1511 以降、WDK から削除されました。



Nmake2MsBuild ユーティリティとドライバーのソース コード ファイルから以前のバージョンの WDK を使用して構築されたドライバー用の Visual Studio プロジェクトの生成、*ソース*、*ディレクトリ*、および*makefile.inc*ファイル。 ユーティリティでは、Visual Studio のプロジェクト ファイルを作成、既存のと同じディレクトリに*ソース*ファイル。 このユーティリティは、ソース コードや、以前のビルド ファイルには変更されません。

ユーティリティの使用方法の詳細については、次を参照してください。 [、WDK を変換するファイルを Visual Studio プロジェクトをソース](converting-a-wdk-sources-file-to-a-visual-studio-project.md)します。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文


Nmake2MsBuild.exe ユーティリティには、次の構文があります。

```
NMake2MSBuild.exe  < sources [<sources>...] | dirs >
                          [-Name:<Name of output project>]
                          [-Package:<Path to package project file to generate>]
                          [-Solution:<Path to Solution file to generate>]
                          [-Log:[<LogFile>]:[<Verbosity>]]
                          [-ConsoleLog:<Verbosity>]
                          [-NoPackageProject]
                          [-NoSolution]
                          [-SafeMode]
```

変換ツールは、%programfiles% 内にある\\Windows キット\\8.0\\ツール\\x86\\ディレクトリ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><em>ソース</em></td>
<td align="left"><p>パスを指定します、<em>ソース</em>WDK の以前のバージョンでビルドされたドライバーのファイル。 指定した場合、<em>ソース</em>ユーティリティ ファイルを解析する<em>ソース</em>ファイルと、対応する<em>makefile.inc</em>し、Visual Studio のプロジェクト ファイルを生成します。 Visual Studio のプロジェクト ファイルと同じディレクトリに配置、<em>ソース</em>ファイル。</p>
<p>1 つ以上指定できます<em>ソース</em>一度にファイル。 結果として得られるすべてのプロジェクトは、同じソリューションとプロジェクトのパッケージ共有します。</p></td>
</tr>
<tr class="even">
<td align="left"><em>ディレクトリ</em></td>
<td align="left"><p>パスを指定します、<em>ディレクトリ</em>WDK の以前のバージョンでビルドされたドライバーのファイル。 指定した場合、<em>ディレクトリ</em>ファイルをユーティリティはディレクトリ ツリー内のすべての<em>ソース</em>ファイルおよび対応する makefile.inc ファイルし、それぞれの Visual Studio プロジェクト ファイルが生成されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>パッケージ:</strong><em>&lt;を生成するパッケージ ファイルへのパス&gt;</em></td>
<td align="left">ドライバー パッケージのプロジェクト ファイルのカスタム名を指定します。</td>
</tr>
<tr class="even">
<td align="left"><strong>-解決方法:</strong><em>&lt;を生成するソリューション ファイルへのパス&gt;</em></td>
<td align="left">ドライバーのソリューション ファイル (.sln) のカスタム名を指定します。</td>
</tr>
<tr class="odd">
<td align="left">-<strong>Log:[</strong><em>&lt;LogFile&gt;</em><strong>]:[</strong><em>&lt;Verbosity&gt;</em><strong>]</strong></td>
<td align="left">ログ ファイルの名前を指定し、ログ記録のレベルを指定します (を参照してください<em>詳細度</em>)。</td>
</tr>
<tr class="even">
<td align="left"><strong>-ConsoleLog:</strong><em>&lt;詳細度&gt;</em></td>
<td align="left">コンソールのログ ファイルの名前を指定し、ログ記録のレベルを指定します (を参照してください<em>詳細度</em>)。</td>
</tr>
<tr class="odd">
<td align="left"><p><strong>名前:</strong><em>&lt;出力プロジェクトの名前&gt;</em></p></td>
<td align="left"><p>生成される VcxProj ファイルのカスタム名を指定します。 また場合、<em>ディレクトリ</em>ファイルが変換される、生成されたソリューションの名前を指定するこのパラメーターを使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><em>詳細度</em></td>
<td align="left">ログ ファイルとコンソールのログ記録の既定のログ記録レベルは<strong>Verbose</strong>と<strong>情報</strong>それぞれします。 <em>詳細度</em>の 1 つ<strong>System.Diagnostics.SourceLevels</strong>します。</td>
</tr>
<tr class="odd">
<td align="left"><strong>-セーフ モード</strong></td>
<td align="left">セーフ モードでは、NMAKE のターゲットの IDE/UI サポートは提供されませんが、(nmake の) ターゲットをより正確な変換を提供できます。 プロジェクトの (nmake の) ターゲットで実行されていたビルド ステップ中に問題が発生した場合のみ、セーフ モードを指定します。</td>
</tr>
</tbody>
</table>



## <a name="span-idcommentsspanspan-idcommentsspanspan-idcommentsspancomments"></a><span id="Comments"></span><span id="comments"></span><span id="COMMENTS"></span>コメント


変換ツールは、%programfiles% 内にある\\Windows キット\\8.0\\ツール\\x86\\ディレクトリ。

応答 (します。Rsp) ファイルは、コマンド ライン パラメーターを指定するためにサポートされます。 別の行には、各パラメーターを指定する必要があります。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


(Build.exe とソースとディレクトリのファイルを使用)、WDK の以前のバージョンで構築されたドライバーのプロジェクトをビルドする必要があります最初に変換して、します。Nmake2MsBuild.exe 変換ユーティリティを使用して VcxProj プロジェクトです。

たとえば、MyDriver と呼ばれる、Windows 7 WDK で以前に構築されているドライバーの変換を初めて開く、 **Visual Studio コマンド プロンプト**ウィンドウ。 ディレクトリに移動またはを含むディレクトリへのパスを指定、*ソース*または*ディレクトリ*構成ファイルを構築します。 たとえば、次のコマンドと同じフォルダーに MyDriver.Vcxproj ファイルを生成、*ソース*ファイル。

```
nmake2msbuild.exe  .\myDriver\sources
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WDK のソース ファイルを Visual Studio プロジェクトに変換します。](converting-a-wdk-sources-file-to-a-visual-studio-project.md)

[既にあるソース ファイルからのドライバーの作成](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_from_existing_source_files)










