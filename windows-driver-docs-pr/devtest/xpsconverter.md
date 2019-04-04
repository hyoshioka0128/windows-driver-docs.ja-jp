---
title: XpsConverter
description: XPS Converter (XpsConverter.exe) は、標準化された OpenXPS に Microsoft XPS (MSXPS) から XML Paper Specification (XPS) ドキュメントを変換するためのコマンド ライン ツールです。
ms.assetid: A51F818E-AECD-4EBD-99AC-F3BD026C19D6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b974e968a6f8967ff1c79c4c304f0834f7bc9a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573132"
---
# <a name="xpsconverter"></a>XpsConverter


XPS Converter (XpsConverter.exe) から Microsoft XPS (MSXPS) に標準化の OpenXPS と OpenXPS Microsoft XPS (MSXPS) から、XML Paper Specification (XPS) ドキュメントを変換するためのコマンド ライン ツールです。 このツールは、他の 1 つの XPS 形式から、XPS テスト関連資料の変換をします。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">XpsConverter はどこでダウンロードできますか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>XpsConverter.exe には、Microsoft Windows Driver Kit (WDK) が含まれています。 WDK の取得方法の詳細については、<a href="https://go.microsoft.com/fwlink/p/?linkid=290798" data-raw-source="[Windows Driver Kit Downloads]( https://go.microsoft.com/fwlink/p/?linkid=290798)">Windows Driver Kit のダウンロード</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

XpsConverter はで、その他の容量よりもスタンドアロン ツールとして使用するものではありません。 その他の使用はサポートされません。 部分的に使用されていないまたは全体で、アプリケーションまたはドライバー、およびコンパイル解除またはツールの変更が禁じられています。 Microsoft では、すべての権限を保持し、XpsConverter.exe とそのすべての関連ドキュメントの著作権を保持します。

**XPS ドキュメントを変換するには**

1.  Visual Studio のコマンド プロンプト ウィンドウを開きます。

2.  実行、 **XpsConverter.exe**ツールし、ソースと宛先のファイルまたはフォルダーの名前を指定するファイルを変換する形式を指定します。

    たとえば、次のコマンドでは、text.xps OpenXPS 形式と呼ばれる MSXPS ファイルに変換します。

    ```
    XpsConverter /OpenXPS /InputFile=Text.xps /OutputFile=Test.oxps
    ```

    XpsConverter.exe ファイルを %programfiles% に配置は、WDK をインストールするときに\\Windows キット\\8.1\\bin\\*&lt;arch&gt;* または %programfiles(86) %\\Windows キット\\8.1\\bin\\*&lt;arch&gt;* ディレクトリ。

## <a name="span-idxpsconvertercommandsyntaxspanspan-idxpsconvertercommandsyntaxspanspan-idxpsconvertercommandsyntaxspanxpsconverter-command-syntax"></a><span id="XpsConverter_Command_Syntax"></span><span id="xpsconverter_command_syntax"></span><span id="XPSCONVERTER_COMMAND_SYNTAX"></span>XpsConverter コマンドの構文


```
  XpsConverter  <format>  
  [/InputFile=<inputfile> /OutputFile=<outputfile>  | /InputFolder=<inputfolder> /OutputFolder=<outputfolder>]  

  [-logger:<LoggerType>]
  [-logfile:<LogFile>  ]
  [ -device:<DeviceString> ]
  [ /? ]
```

## <a name="span-idcommandparametersspanspan-idcommandparametersspanspan-idcommandparametersspancommand-parameters"></a><span id="Command_parameters"></span><span id="command_parameters"></span><span id="COMMAND_PARAMETERS"></span>コマンドのパラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_format_"></span><span id="_FORMAT_"></span><em>&lt;書式設定&gt;</em></p></td>
<td align="left"><p>ソース ファイルを変換後の形式を指定します。 <em>&lt;形式&gt;</em>が必要です。 指定<strong>/OpenXPS</strong> OpenXPS ドキュメントに変換するか、 <strong>/XPS</strong> Microsoft XPS (MSXPS) ドキュメントを変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_InputFile__inputfile___OutputFile__outputfile_"></span><span id="_inputfile__inputfile___outputfile__outputfile_"></span><span id="_INPUTFILE__INPUTFILE___OUTPUTFILE__OUTPUTFILE_"></span><strong>/InputFile=</strong><em>&lt;inputfile&gt;</em> <strong>/OutputFile=</strong><em>&lt;outputfile&gt;</em></p></td>
<td align="left"><p>このオプションを使用して変換<em>&lt;inputfile&gt;</em>に保存して <em>&lt;outputfile&gt;</em>します。 <em>&lt;Inputfile&gt;</em> .xps または .oxps ファイル名拡張子が必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="_InputFolder__inputfolder____OutputFolder__outputfolder_"></span><span id="_inputfolder__inputfolder____outputfolder__outputfolder_"></span><span id="_INPUTFOLDER__INPUTFOLDER____OUTPUTFOLDER__OUTPUTFOLDER_"></span><strong>/InputFolder=</strong><em>&lt;inputfolder&gt;</em> <strong>/OutputFolder=</strong><em>&lt;outputfolder&gt;</em></p></td>
<td align="left"><p>このオプションを使用してすべてのファイルの変換<em>&lt;inputfolder&gt;</em>に保存し、  <em>&lt;outputfolder&gt;</em>します。 内のファイル<em>&lt;inputfolder&gt;</em> .xps または .oxps ファイル名拡張子をいる必要があります。</p>
<div class="alert">
<strong>注</strong>再帰的な操作は、フォルダーを変換します。 S は、指定したすべてのファイルが変換されます<em>&lt;inputfolder&gt;</em> およびすべてのサブディレクトリ。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p><span id="__-logger__LoggerType_"></span><span id="__-logger__loggertype_"></span><span id="__-LOGGER__LOGGERTYPE_"></span> <strong>-ロガー:</strong><em>&lt;LoggerType&gt;</em></p></td>
<td align="left"><p>任意。 <em>&lt;LoggerType&gt;</em> を生成するログの種類を示します (<strong>ファイル</strong>、<strong>コンソール</strong>または<strong>WTT</strong>)、変換中に使用します。 既定のロガーは<strong>コンソール</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="-logfile__LogFile_"></span><span id="-logfile__logfile_"></span><span id="-LOGFILE__LOGFILE_"></span><strong>-logfile:</strong><em>&lt;LogFile&gt;</em></p></td>
<td align="left"><p>任意。 指定します、 <em>&lt;LogFile&gt;</em>ときに使用する、 <strong>-ロガー</strong>オプションは<strong>ファイル</strong>します。 指定しない場合、  <em>&lt;LogFile&gt;</em>既定のログ ファイルは XpsConverter.txt します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="-device__DeviceString_"></span><span id="-device__devicestring_"></span><span id="-DEVICE__DEVICESTRING_"></span><strong>-デバイス:</strong><em>&lt;DeviceString&gt;</em></p></td>
<td align="left"><p>任意。 指定します、<em>&lt;DeviceString&gt;</em> ときに使用する、 <strong>-ロガー</strong>オプションは<strong>WTT</strong>します。 既定のデバイスは<strong>$LogFile:file=XpsConverter.wtl,WriteMode=append</strong>します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


使用することができます、 **isXPS.exe (isxps 適合性ツール)** XPS と Open Packaging Conventions (OPC) 仕様に、ファイルの適合性をテストするのには。

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例


```
XpsConverter /OpenXPS /InputFile=Text.xps /OutputFile=Test.oxps
XpsConverter /XPS /InputFolder=c:\OpenXPS /OutputFolder=c:\MSXPS
XpsConverter /OpenXPS /InputFile=MyDoc.xps /OutputFile=ConvertedMyDoc.oxps  logger:file  logfile:MyLog.txt
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


**isXPS.exe (isxps 適合性ツール)**

 

 






