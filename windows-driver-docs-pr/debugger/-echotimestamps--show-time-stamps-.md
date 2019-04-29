---
title: .echotimestamps (タイム スタンプの表示)
description: .Echotimestamps コマンドは、オンまたはタイムスタンプ情報の表示をオフにします。
ms.assetid: c70dc71b-83c2-41de-90f3-638e231c0476
keywords:
- タイムスタンプ (.echotimestamps) コマンドを表示します。
- タイムスタンプ
- による DbgPrint のタイムスタンプ
- .echotimestamps (Show タイムスタンプ) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .echotimestamps (Show Time Stamps)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8a3351684dc4188c654286079f5bfddfab03a590
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336802"
---
# <a name="echotimestamps-show-time-stamps"></a>.echotimestamps (タイム スタンプの表示)


**.Echotimestamps**コマンドは、オンまたはタイムスタンプ情報の表示をオフにします。

```dbgcmd
.echotimestamps 0 
.echotimestamps 1 
.echotimestamps 
```

## <a name="span-idddkmetashowtimestampsdbgspanspan-idddkmetashowtimestampsdbgspanparameters"></a><span id="ddk_meta_show_time_stamps_dbg"></span><span id="DDK_META_SHOW_TIME_STAMPS_DBG"></span>パラメーター


<span id="_______0______"></span> **0**   
タイムスタンプ情報の表示をオフにします。 これは、デバッガーの既定の動作です。

<span id="_______1______"></span> **1**   
タイムスタンプ情報の表示をオンにします。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については**による DbgPrint**、 **KdPrint**、 **DbgPrintEx**、および**KdPrintEx**を参照してください[による DbgPrint バッファー](reading-and-filtering-debugging-messages.md#the-dbgprint-buffer)または Microsoft Windows Driver Kit (WDK) ドキュメントを参照してください。

<a name="remarks"></a>注釈
-------

使用すると、 **.echotimestamps**パラメーターを指定せずコマンド タイムスタンプの表示がオンまたはオフになっているし、新しい状態が表示されます。

この表示を有効にする場合、デバッガーには、モジュールの読み込み、スレッドの作成、例外、およびその他のイベントのタイムスタンプが表示されます。

**による DbgPrint**、 **KdPrint**、 **DbgPrintEx**、および**KdPrintEx**カーネル モードのルーチンは、ホスト上のバッファーに書式設定された文字列を送信コンピューター。 文字列を表示、[デバッガー コマンド ウィンドウ](debugger-command-window.md)(このような印刷を無効にした) 場合を除き、します。 使用して、書式設定された文字列を表示することも、 [ **! による dbgprint** ](-dbgprint.md)拡張機能コマンド。

使用すると **.echotimestamps**タイムスタンプの各コメントの日付と時刻の表示を有効にする、**による DbgPrint**バッファーが表示されます。

 

 





