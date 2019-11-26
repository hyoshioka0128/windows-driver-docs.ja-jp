---
title: Nmake2MsBuild
description: Nmake2MsBuild ユーティリティは、以前のバージョンの WDK を使用して作成されたドライバーの Visual Studio プロジェクトを、ドライバーのソースコードファイル、および source、dirs、および makefile ファイルから生成します。
ms.assetid: D6E1C124-9A5F-486B-865E-45A0BC58A5A3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 633294c2ae1067ed3a5c597b9fcbb42d7d4c9b04
ms.sourcegitcommit: fc7e9b273277a91076b914095f4ee6f1eef7014a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2019
ms.locfileid: "74196985"
---
# <a name="nmake2msbuild"></a>Nmake2MsBuild


**メモ** Nmake2MsBuild ツールは、Windows 10 バージョン1511以降の WDK から削除されました。



Nmake2MsBuild ユーティリティは、以前のバージョンの WDK を使用して作成されたドライバーの Visual Studio プロジェクトを、ドライバーのソースコード*ファイル、および source、* *dirs*、および*makefile*ファイルから生成します。 このユーティリティでは、既存の*ソース*ファイルと同じディレクトリに Visual Studio プロジェクトファイルが作成されます。 このユーティリティでは、ソースコードまたは以前のビルドファイルは変更されません。

ユーティリティの使用方法の詳細については、「 [WDK ソースファイルを Visual Studio プロジェクトに変換](converting-a-wdk-sources-file-to-a-visual-studio-project.md)する」を参照してください。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>文


Nmake2MsBuild ユーティリティには、次の構文があります。

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

変換ツールは、% PROGRAMFILES%\\Windows Kit\\8.0\\tools\\x86\\ directory にあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><em>文書</em></td>
<td align="left"><p>以前のバージョンの WDK でビルドされたドライバーの<em>ソース</em>ファイルへのパスを指定します。 <em>ソース</em>ファイルを指定すると、ユーティリティによってその<em>ソース</em>ファイルおよび対応する<em>makefile</em>が解析され、Visual Studio プロジェクトファイルが生成されます。 Visual Studio プロジェクトファイルは、<em>ソース</em>ファイルと同じディレクトリに配置されます。</p>
<p>複数の<em>ソース</em>ファイルを同時に指定できます。 結果として得られるすべてのプロジェクトは、同じソリューションとパッケージプロジェクトを共有します。</p></td>
</tr>
<tr class="even">
<td align="left"><em>dirs</em></td>
<td align="left"><p>以前のバージョンの WDK でビルドされたドライバーの<em>ディレクトリ</em>ファイルへのパスを指定します。 <em>Dirs</em>ファイルを指定した場合、ユーティリティは、すべての<em>ソース</em>ファイルとそれに対応する makefile ファイルのディレクトリツリー内を検索し、それぞれに対して Visual Studio プロジェクトファイルを生成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>-Package:</strong> <em>&lt;生成するパッケージファイルへのパス&gt;</em></td>
<td align="left">ドライバーパッケージプロジェクトファイルのカスタム名を指定します。</td>
</tr>
<tr class="even">
<td align="left"><strong>-Solution:</strong> <em>&lt;生成するソリューションファイルへのパス&gt;</em></td>
<td align="left">ドライバーソリューションファイル (.sln) のカスタム名を指定します。</td>
</tr>
<tr class="odd">
<td align="left">-<strong>ログ: [</strong> <em>&lt;LogFile&gt;</em> <strong>]: [</strong> <em>&lt;詳細&gt;</em> <strong>]</strong></td>
<td align="left">ログファイルの名前を指定し、ログ記録のレベルを指定します (詳細については、「<em>詳細</em>」を参照してください)。</td>
</tr>
<tr class="even">
<td align="left"><strong>-Consolelog:</strong> <em>&lt;詳細度&gt;</em></td>
<td align="left">コンソールログファイルの名前を指定し、ログ記録のレベルを指定します (詳細については、「<em>詳細</em>」を参照してください)。</td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-Name:</strong> <em>&lt;出力プロジェクトの名前&gt;</em></p></td>
<td align="left"><p>生成される .Vcxproj ファイルのカスタム名を指定します。 また、<em>ディレクトリ</em>ファイルが変換されている場合は、このパラメーターを使用して、生成されたソリューションの名前を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><em>出力</em></td>
<td align="left">ログファイルとコンソールログの既定のログ記録レベルは、それぞれ、<strong>詳細</strong><strong>情報と情報</strong>です。 <em>詳細</em>度は<strong>SourceLevels</strong>のいずれかです。</td>
</tr>
<tr class="odd">
<td align="left"><strong>-セーフ</strong></td>
<td align="left">セーフモードでは、NMAKE ターゲットに対する IDE/UI のサポートは提供されませんが、NMAKE のターゲットに対してより正確な変換を行うことができます。 以前にプロジェクトの NMAKE ターゲットで実行されたビルドステップで問題が発生した場合にのみ、-セーフを指定します。</td>
</tr>
</tbody>
</table>



## <a name="span-idcommentsspanspan-idcommentsspanspan-idcommentsspancomments"></a><span id="Comments"></span><span id="comments"></span><span id="COMMENTS"></span>Comments


変換ツールは、% PROGRAMFILES%\\Windows Kit\\8.0\\tools\\x86\\ directory にあります。

応答 (。Rsp) ファイルは、コマンドラインパラメーターを指定するためにサポートされています。 各パラメーターは個別の行に指定する必要があります。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>よう


以前のバージョンの WDK を使用してビルドされたドライバープロジェクトをビルドするには (Build .exe および sources と dirs ファイルを使用)、まずそれをに変換する必要があります。Nmake2MsBuild 変換ユーティリティを使用する .Vcxproj プロジェクト。

たとえば、以前に Windows 7 WDK でビルドされたドライバー (MyDriver) を変換するには、最初に**Visual Studio のコマンドプロンプト**ウィンドウを開きます。 ディレクトリを参照するか、*ソース*または*dirs*ビルド構成ファイルが格納されているディレクトリへのパスを指定します。 たとえば、次のコマンドでは、*ソース*ファイルと同じフォルダーに Mydriver .vcxproj ファイルが生成されます。

```
nmake2msbuild.exe  .\myDriver\sources
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WDK ソースファイルを Visual Studio プロジェクトに変換する](converting-a-wdk-sources-file-to-a-visual-studio-project.md)

[既にあるソース ファイルからのドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/develop/creating-a-driver-from-existing-source-files)










