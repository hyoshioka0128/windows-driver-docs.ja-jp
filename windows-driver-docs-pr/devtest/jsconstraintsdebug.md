---
title: JSConstraintsDebug
description: JSConstraintsDebug (JSConstraintsDebug.exe) は、V4 プリンター ドライバーの開発中に JavaScript 制約に対するデバッグのサポートを提供するコマンド ライン ツールです。
ms.assetid: 48C39A2C-7EA6-4BAA-B5E8-3B426C9697B3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d276834e26f7c1fd35d380e3d89f5c990f5e06a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340434"
---
# <a name="jsconstraintsdebug"></a>JSConstraintsDebug


JSConstraintsDebug (JSConstraintsDebug.exe) に対するデバッグのサポートを提供するコマンド ライン ツールは、 [JavaScript 制約](https://msdn.microsoft.com/library/windows/hardware/jj218731)開発中に、 [V4 プリンター ドライバー](https://msdn.microsoft.com/library/windows/hardware/hh706306)します。

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
<td align="left"><p>JSConstraintsDebug.exe には、Microsoft Windows Driver Kit (WDK) が含まれています。 WDK の取得方法の詳細については、次を参照してください。 <a href="https://go.microsoft.com/fwlink/p/?LinkId=808351" data-raw-source="[Windows Driver Kit downloads](https://go.microsoft.com/fwlink/p/?LinkId=808351)">Windows Driver Kit のダウンロード</a>します。</p></td>
</tr>
</tbody>
</table>

 

ツールは、印刷チケットが提供されているユーザーに対して、対象となるドライバーの JavaScript の制約に対して、次の関連するエントリ ポイントの Api の各を実行します。

[**PTGetPrintCapabilities**](https://msdn.microsoft.com/library/windows/desktop/dd162881)

[**PTConvertDevModeToPrintTicket**](https://msdn.microsoft.com/library/windows/desktop/dd162879)

[**TConvertPrintTicketToDevMode**](https://msdn.microsoft.com/library/windows/desktop/dd162880)

[**PTMergeAndValidatePrintTicket**](https://msdn.microsoft.com/library/windows/desktop/dd162884)

実行中に、ツールは Visual Studio など、適切な IDE デバッガー求められます。 選択、制約のソース コードを開くし、する JavaScript デバッガー ステートメントで停止します。

JS 制約ファイルをデバッグするには、次の手順を実行します。

1.  コマンド プロンプト ウィンドウを開きます。

2.  JSConstraintsDebug.exe ツールを実行し、最小値、プリンター名、およびテストへのパスでの印刷チケットを指定します。

3.  使用するデバッグ ツールを選択します。

## <a name="span-idrunningjsconstraintsdebuginusermodespanspan-idrunningjsconstraintsdebuginusermodespanspan-idrunningjsconstraintsdebuginusermodespanrunning-jsconstraintsdebug-in-user-mode"></a><span id="Running_JSConstraintsDebug_in_user_mode"></span><span id="running_jsconstraintsdebug_in_user_mode"></span><span id="RUNNING_JSCONSTRAINTSDEBUG_IN_USER_MODE"></span>ユーザー モードで実行中の JSConstraintsDebug


JS 関数のデバッグを有効にするのには、管理者特権での特権が必要です。 ユーザー モードで実行するには、JSConstraintsDebug.exe を実行する前に、次のレジストリ キーを設定する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>キー名</p></td>
<td align="left"><p>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print</p></td>
</tr>
<tr class="even">
<td align="left"><p>値の名前</p></td>
<td align="left"><p>EnableJavaScriptDebugging</p></td>
</tr>
<tr class="odd">
<td align="left"><p>型</p></td>
<td align="left"><p>DWORD</p></td>
</tr>
<tr class="even">
<td align="left"><p>値</p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idjavascriptdebuggerstatementsspanspan-idjavascriptdebuggerstatementsspanspan-idjavascriptdebuggerstatementsspanjavascript-debugger-statements"></a><span id="JavaScript_debugger_statements"></span><span id="javascript_debugger_statements"></span><span id="JAVASCRIPT_DEBUGGER_STATEMENTS"></span>JavaScript デバッガー ステートメント


ブレークポイントは、デバッガー ステートメントを使用して、JavaScript のソースで作成できます。 これは、ステップ バイ ステップのデバッグは、すべて Visual Studio での操作を一時停止します。 これらのステートメントは、のいずれかに挿入できる、 [JavaScript 制約 Api](https://go.microsoft.com/fwlink/p/?LinkId=808350)します。

例:

```JavaScript
function validatePrintTicket(PrintTicket, scriptContext)
{
    debugger; // debug tool will pause at this breakpoint
    ...
}
```

## <a name="span-idjsconstraintsdebugcommandsyntaxspanspan-idjsconstraintsdebugcommandsyntaxspanspan-idjsconstraintsdebugcommandsyntaxspanjsconstraintsdebug-command-syntax"></a><span id="JSConstraintsDebug_Command_Syntax"></span><span id="jsconstraintsdebug_command_syntax"></span><span id="JSCONSTRAINTSDEBUG_COMMAND_SYNTAX"></span>JSConstraintsDebug コマンドの構文


```
JSConstraintsDebug <PrinterName> <PrintTicket> [MergePrintTicket] [Constraints]
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
<td align="left"><p><span id="PrinterName"></span><span id="printername"></span><span id="PRINTERNAME"></span>プリンター名</p></td>
<td align="left"><p>必須。 JS 制約のソース ファイルを含む印刷ドライバーの文字列名を指定します。 このドライバーは、すべてのデバッグ操作に使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="PrintTicket"></span><span id="printticket"></span><span id="PRINTTICKET"></span>PrintTicket</p></td>
<td align="left"><p>必須。 検証する印刷チケットの XML ファイルの名前とパスを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="MergePrintTicket"></span><span id="mergeprintticket"></span><span id="MERGEPRINTTICKET"></span>MergePrintTicket</p></td>
<td align="left"><p>任意。 マージ操作を検証するために使用する印刷チケットの XML ファイルの名前とパスを指定します。</p>
<p>このパラメーターは、マージ変換および検証 API を既定の DevMode 印刷チケットに変換され、渡されるを設定されていません。 場合、</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Constraints"></span><span id="constraints"></span><span id="CONSTRAINTS"></span>制約</p></td>
<td align="left"><p>任意。 デバッグする前に対象となるプリンター ドライバーにある既存の制約のソース ファイルを置換する JavaScript 制約ファイルの名前とパスを指定します。</p></td>
</tr>
</tbody>
</table>

 

**注**  制約パラメーターを使用して制約ファイルを指定すると、対象となるドライバーに既存のソース コードが上書きされます。

 

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例


既知のテストの印刷チケットに対して印刷ドライバーをデバッグします。

```
JSConstraintsDebug “Contoso Printer” PrintTicket.xml
```

既知のテストの印刷チケットに対する新しい制約ソース ファイルでは、印刷ドライバーをデバッグします。

```
JSConstraintsDebug “Contoso Printer” PrintTicket.xml Constraints.js
```

マージをテストし、2 つのカスタム印刷チケットの間での操作を検証します。

```
JSConstraintsDebug “Contoso Printer” PrintTicket.xml PrintTicket2.xml
```

 

 





