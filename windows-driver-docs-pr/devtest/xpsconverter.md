---
title: XpsConverter
description: XPS コンバーター (XpsConverter) は、XML Paper Specification (XPS) ドキュメントを Microsoft XPS (MSXPS) から標準化された OpenXPS に変換するためのコマンドラインツールです。
ms.assetid: A51F818E-AECD-4EBD-99AC-F3BD026C19D6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6cd2015fcb7a36158bdf1caadcf49dbab53b4cf
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769344"
---
# <a name="xpsconverter"></a>XpsConverter


XPS コンバーター (XpsConverter) は、XML Paper Specification (XPS) ドキュメントを Microsoft XPS (MSXPS) から標準化された OpenXPS に、また OpenXPS から Microsoft XPS (MSXPS) に変換するためのコマンドラインツールです。 このツールは、xps のテスト資料を XPS 形式間で変換することを支援することを目的としています。

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
<td align="left"><p>XpsConverter は、Microsoft Windows Driver Kit (WDK) に含まれています。 WDK の入手方法については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk" data-raw-source="[Windows Driver Kit Downloads](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)">Windows Driver Kit のダウンロード</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

XpsConverter は、スタンドアロンツールとは別の容量で使用するためのものではありません。 他の用途ではサポートされていません。 アプリケーションやドライバーの一部または全体で使用することはできません。また、ツールを逆コンパイルしたり変更したりすることは、厳密には禁止されています。 Microsoft はすべての権利を保持し、XpsConverter およびすべてのサポートドキュメントに著作権を保持します。

**XPS ドキュメントを変換するには**

1.  Visual Studio のコマンド プロンプト ウィンドウを開きます。

2.  **XpsConverter**ツールを実行し、コピー元とコピー先のファイルまたはフォルダーの名前を指定して、ファイルを変換する形式を指定します。

    たとえば、次のコマンドは、OpenXPS という名前の MSXPS ファイルを形式に変換します。

    ```
    XpsConverter /OpenXPS /InputFile=Text.xps /OutputFile=Test.oxps
    ```

    WDK をインストールすると、XpsConverter ファイルは% programfiles% \\ windows kit \\ 8.1 \\ bin \\ * &lt; arch &gt; *または% programfiles (86)% \\ windows kit \\ 8.1 \\ bin \\ * &lt; arch &gt; *ディレクトリに配置されます。

## <a name="span-idxpsconverter_command_syntaxspanspan-idxpsconverter_command_syntaxspanspan-idxpsconverter_command_syntaxspanxpsconverter-command-syntax"></a><span id="XpsConverter_Command_Syntax"></span><span id="xpsconverter_command_syntax"></span><span id="XPSCONVERTER_COMMAND_SYNTAX"></span>XpsConverter コマンドの構文


```
  XpsConverter  <format>  
  [/InputFile=<inputfile> /OutputFile=<outputfile>  | /InputFolder=<inputfolder> /OutputFolder=<outputfolder>]  

  [-logger:<LoggerType>]
  [-logfile:<LogFile>  ]
  [ -device:<DeviceString> ]
  [ /? ]
```

## <a name="span-idcommand_parametersspanspan-idcommand_parametersspanspan-idcommand_parametersspancommand-parameters"></a><span id="Command_parameters"></span><span id="command_parameters"></span><span id="COMMAND_PARAMETERS"></span>コマンドパラメーター


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
<td align="left"><p><span id="_format_"></span><span id="_FORMAT_"></span><em>&lt;形式&gt;</em></p></td>
<td align="left"><p>ソースファイルを変換する形式を指定します。 <em> &lt; 形式 &gt; </em>が必要です。 ドキュメントを OpenXPS または/OpenXPS に変換して、ドキュメントを Microsoft XPS (MSXPS) に変換する<strong>には、</strong> [ <strong>/OpenXPS</strong> ] を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_InputFile__inputfile___OutputFile__outputfile_"></span><span id="_inputfile__inputfile___outputfile__outputfile_"></span><span id="_INPUTFILE__INPUTFILE___OUTPUTFILE__OUTPUTFILE_"></span><strong>/InputFile =</strong><em> &lt; InputFile &gt; </em> <strong>/OutputFile =</strong><em> &lt; OutputFile &gt; </em></p></td>
<td align="left"><p>このオプションを使用して<em> &lt; inputfile &gt; </em>を変換し、 <em> &lt; outputfile &gt; </em>に保存します。 <em> &lt; Inputfile &gt; </em>のファイル名拡張子は、.xps または oxps である必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="_InputFolder__inputfolder____OutputFolder__outputfolder_"></span><span id="_inputfolder__inputfolder____outputfolder__outputfolder_"></span><span id="_INPUTFOLDER__INPUTFOLDER____OUTPUTFOLDER__OUTPUTFOLDER_"></span><strong>/InputFolder =</strong><em> &lt; InputFolder &gt; </em> <strong>/OutputFolder=</strong>/OutputFolder =<em>OutputFolder &lt; &gt; </em></p></td>
<td align="left"><p>このオプションを使用して、 <em> &lt; inputfolder &gt; </em>内のすべてのファイルを変換し、 <em> &lt; outputfolder &gt; </em>に保存します。 <em> &lt; Inputfolder &gt; </em>内のファイルのファイル名拡張子は、.xps または oxps である必要があります。</p>
<div class="alert">
<strong>メモ</strong>  フォルダーの変換は再帰的な操作です。 このツールは、指定された s<em> &lt; inputfolder &gt; </em>とすべてのサブディレクトリ内のすべてのファイルを変換します。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p><span id="__-logger__LoggerType_"></span><span id="__-logger__loggertype_"></span><span id="__-LOGGER__LOGGERTYPE_"></span><strong>-logger:</strong><em> &lt; LoggerType &gt; </em></p></td>
<td align="left"><p>省略可能。 <em> &lt; LoggerType &gt; </em>は、変換中に使用するログの種類 (<strong>ファイル</strong>、<strong>コンソール</strong>、または<strong>wtt</strong>) を示します。 既定のロガーは<strong>Console</strong>です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="-logfile__LogFile_"></span><span id="-logfile__logfile_"></span><span id="-LOGFILE__LOGFILE_"></span><strong>-logfile:</strong><em> &lt; ログ &gt; ファイル</em></p></td>
<td align="left"><p>省略可能。 <strong>-Logger</strong>オプションが<strong>FILE</strong>の場合に使用する<em> &lt; &gt; ログファイル</em>を指定します。 ログ<em> &lt; &gt; ファイルを指定</em>しない場合、既定のログファイルは XpsConverter になります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="-device__DeviceString_"></span><span id="-device__devicestring_"></span><span id="-DEVICE__DEVICESTRING_"></span><strong>-デバイス:</strong><em> &lt; devicestring &gt; </em></p></td>
<td align="left"><p>省略可能。 <strong>-Logger</strong>オプションが<strong>wtt</strong>の場合に使用する<em> &lt; devicestring &gt; </em>を指定します。 既定のデバイスは<strong>$LogFile: file = XpsConverter、WriteMode = append</strong>です。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


**Isxps (Isxps 適合性ツール)** を使用すると、ファイルが XPS および Open パッケージング規則 (OPC) の仕様に準拠しているかどうかをテストできます。

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例


```
XpsConverter /OpenXPS /InputFile=Text.xps /OutputFile=Test.oxps
XpsConverter /XPS /InputFolder=c:\OpenXPS /OutputFolder=c:\MSXPS
XpsConverter /OpenXPS /InputFile=MyDoc.xps /OutputFile=ConvertedMyDoc.oxps  logger:file  logfile:MyLog.txt
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


**isXPS.exe (isXPS 適合性ツール)**

 

 






