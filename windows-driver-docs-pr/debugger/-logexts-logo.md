---
title: logexts.logo
description: Logexts.logo 拡張機能を設定またはロガーの出力オプションが表示されます。
ms.assetid: b094cf4b-1d01-4b84-9032-aa865d680df4
keywords:
- デバッグ logexts.logo Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- logexts.logo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 686db814fb70116f5c10a04621c4df263aaa058d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529802"
---
# <a name="logextslogo"></a>!logexts.logo


**! Logexts.logo**拡張機能を設定またはロガーの出力オプションが表示されます。

```dbgcmd
!logexts.logo {e|d} {d|t|v} 
!logexts.logo 
```

## <a name="span-idddklogextslogodbgspanspan-idddklogextslogodbgspanparameters"></a><span id="ddk__logexts_logo_dbg"></span><span id="DDK__LOGEXTS_LOGO_DBG"></span>パラメーター


<span id="_______e_d"></span><span id="_______E_D"></span> **e|d**  
指定された出力の種類 (e) を有効にするか、(d) を無効にするかどうかを指定します。

<span id="_______d_t_v"></span><span id="_______D_T_V"></span> **d | t | v**  
出力の種類を指定します。 ロガーの出力の 3 つの種類もあります。 メッセージは、テキスト ファイル (t)、または詳細 .lgv ファイル (v) (d) のデバッガーに直接送信します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>logexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>logexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[Logger と LogViewer](logger-and-logviewer.md)を参照してください。

<a name="remarks"></a>注釈
-------

場合 **! logexts.logo**ログの現在の状態、出力ディレクトリ、およびデバッガー、テキスト ファイル、および詳細なログの現在の設定を表示し、パラメーターなしで使用します。

```dbgcmd
0:000> !logo
Logging currently enabled.

Output directory: MyLogs\LogExts\

Output settings:
  Debugger            Disabled
  Text file           Enabled
  Verbose log         Enabled
```

デバッガーが開始されたディレクトリに対して相対的な配置されているために、前の例では、出力ディレクトリは相対パスでは、です。

詳細ログ記録を無効にするのには、次のコマンドを使用します。

```dbgcmd
0:000> !logo d v
  Debugger            Disabled
  Text file           Enabled
  Verbose log         Disabled
```

テキスト ファイルと .lgv ファイルは現在の出力ディレクトリに配置されます。 .Lgv ファイルを読み取り、LogViewer を使用します。

 

 





