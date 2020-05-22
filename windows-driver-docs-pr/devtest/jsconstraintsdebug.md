---
title: JSConstraintsDebug
description: JSConstraintsDebug (JSConstraintsDebug) は、V4 プリンタードライバーの開発中に JavaScript の制約のデバッグサポートを提供するコマンドラインツールです。
ms.assetid: 48C39A2C-7EA6-4BAA-B5E8-3B426C9697B3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 723202417f7d8e763313e4ce03d4072635b20e63
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769436"
---
# <a name="jsconstraintsdebug"></a>JSConstraintsDebug


JSConstraintsDebug (JSConstraintsDebug) は、 [V4 プリンタードライバー](https://docs.microsoft.com/windows-hardware/drivers/print/v4-printer-driver)の開発中に[JavaScript の制約](https://docs.microsoft.com/windows-hardware/drivers/print/javascript-constraints)のデバッグサポートを提供するコマンドラインツールです。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">JSConstraintsDebug はどこでダウンロードできますか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>JSConstraintsDebug は、Microsoft Windows Driver Kit (WDK) に含まれています。 WDK の入手方法については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk" data-raw-source="[Windows Driver Kit downloads](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)">Windows Driver Kit のダウンロード</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

ツールは、次の関連するエントリポイント Api を、対象となるドライバーの JavaScript 制約に対して、ユーザーが指定した印刷チケットに対して実行します。

[**PTGetPrintCapabilities**](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptgetprintcapabilities)

[**PTConvertDevModeToPrintTicket**](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptconvertdevmodetoprintticket)

[**TConvertPrintTicketToDevMode**](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptconvertprinttickettodevmode)

[**PTMergeAndValidatePrintTicket**](https://docs.microsoft.com/windows/desktop/api/prntvpt/nf-prntvpt-ptmergeandvalidateprintticket)

実行時に、Visual Studio などの適切な IDE デバッガーを入力するように求められます。 選択すると、制約のソースコードが JavaScript デバッガーステートメントで開かれ、停止されます。

JS 制約ファイルをデバッグするには、次の手順を実行します。

1.  コマンド プロンプト ウィンドウを開きます。

2.  JSConstraintsDebug ツールを実行し、少なくともプリンター名とテスト印刷チケットへのパスを指定します。

3.  使用するデバッグツールを選択します。

## <a name="span-idrunning_jsconstraintsdebug_in_user_modespanspan-idrunning_jsconstraintsdebug_in_user_modespanspan-idrunning_jsconstraintsdebug_in_user_modespanrunning-jsconstraintsdebug-in-user-mode"></a><span id="Running_JSConstraintsDebug_in_user_mode"></span><span id="running_jsconstraintsdebug_in_user_mode"></span><span id="RUNNING_JSCONSTRAINTSDEBUG_IN_USER_MODE"></span>ユーザーモードで JSConstraintsDebug を実行しています


JS 関数のデバッグを有効にするには、昇格された特権が必要です。 ユーザーモードで実行するには、JSConstraintsDebug を実行する前に次のレジストリキーを設定する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>キー名</p></td>
<td align="left"><p>HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\Print</p></td>
</tr>
<tr class="even">
<td align="left"><p>値の名前</p></td>
<td align="left"><p>EnableJavaScriptDebugging</p></td>
</tr>
<tr class="odd">
<td align="left"><p>種類</p></td>
<td align="left"><p>DWORD</p></td>
</tr>
<tr class="even">
<td align="left"><p>値</p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idjavascript_debugger_statementsspanspan-idjavascript_debugger_statementsspanspan-idjavascript_debugger_statementsspanjavascript-debugger-statements"></a><span id="JavaScript_debugger_statements"></span><span id="javascript_debugger_statements"></span><span id="JAVASCRIPT_DEBUGGER_STATEMENTS"></span>JavaScript デバッガーステートメント


デバッガーステートメントを使用して、JavaScript ソースでブレークポイントを作成できます。 これにより、Visual Studio での操作が一時停止され、ステップバイステップのデバッグが可能になります。 これらのステートメントは、任意の[JavaScript 制約 api](https://docs.microsoft.com/windows-hardware/drivers/print/javascript-constraints)に挿入できます。

次に例を示します。

```JavaScript
function validatePrintTicket(PrintTicket, scriptContext)
{
    debugger; // debug tool will pause at this breakpoint
    ...
}
```

## <a name="span-idjsconstraintsdebug_command_syntaxspanspan-idjsconstraintsdebug_command_syntaxspanspan-idjsconstraintsdebug_command_syntaxspanjsconstraintsdebug-command-syntax"></a><span id="JSConstraintsDebug_Command_Syntax"></span><span id="jsconstraintsdebug_command_syntax"></span><span id="JSCONSTRAINTSDEBUG_COMMAND_SYNTAX"></span>JSConstraintsDebug コマンドの構文


```
JSConstraintsDebug <PrinterName> <PrintTicket> [MergePrintTicket] [Constraints]
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
<td align="left"><p><span id="PrinterName"></span><span id="printername"></span><span id="PRINTERNAME"></span>PrinterName</p></td>
<td align="left"><p>必須。 JS 制約のソースファイルを含む印刷ドライバーの文字列名を指定します。 このドライバーは、すべてのデバッグ操作に使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PrintTicket"></span><span id="printticket"></span><span id="PRINTTICKET"></span>PrintTicket</p></td>
<td align="left"><p>必須。 検証する印刷チケット XML ファイルのパスと名前を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MergePrintTicket"></span><span id="mergeprintticket"></span><span id="MERGEPRINTTICKET"></span>MergePrintTicket</p></td>
<td align="left"><p>省略可能。 マージ操作の検証に使用される、印刷チケットの XML ファイルのパスと名前を指定します。</p>
<p>このパラメーターが設定されていない場合、既定の DevMode は印刷チケットに変換され、Merge and Validate API に渡されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Constraints"></span><span id="constraints"></span><span id="CONSTRAINTS"></span>Constraints</p></td>
<td align="left"><p>省略可能。 デバッグする前に、対象となるプリンタードライバーで見つかった既存の制約ソースファイルを置き換える JavaScript 制約ファイルのパスと名前を指定します。</p></td>
</tr>
</tbody>
</table>

 

**メモ**   制約パラメーターを使用して制約ファイルを指定すると、対象のドライバーの既存のソースコードが上書きされます。

 

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例


既知のテスト印刷チケットに対して、印刷ドライバーをデバッグします。

```
JSConstraintsDebug “Contoso Printer” PrintTicket.xml
```

既知のテスト印刷チケットに対して新しい制約ソースファイルを使用して、印刷ドライバーをデバッグします。

```
JSConstraintsDebug “Contoso Printer” PrintTicket.xml Constraints.js
```

2つのカスタム印刷チケット間でマージと検証の操作をテストします。

```
JSConstraintsDebug “Contoso Printer” PrintTicket.xml PrintTicket2.xml
```

 

 





