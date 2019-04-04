---
title: dbgprint
description: による dbgprint の拡張機能では、による DbgPrint のバッファーに送信されていた文字列が表示されます。
ms.assetid: bf25ac2a-5a07-43df-946b-3b2237b1816b
keywords:
- Windows デバッグによる dbgprint
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dbgprint
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 00281b2d5f6a389d1dd15c02d9015e4fddabfc79
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556714"
---
# <a name="dbgprint"></a>!dbgprint


**! による dbgprint**拡張機能には、以前に送信された文字列が表示されます、**による DbgPrint**バッファー。

```dbgcmd
!dbgprint
```

## <span id="ddk__dbgprint_dbg"></span><span id="DDK__DBGPRINT_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

について**による DbgPrint**、 **KdPrint**、 **DbgPrintEx**と**KdPrintEx**を参照してください[出力を送信しますデバッガー](sending-output-to-the-debugger.md)します。

<a name="remarks"></a>注釈
-------

カーネル モード ルーチン**による DbgPrint**、 **KdPrint**、 **DbgPrintEx**、および**KdPrintEx**ターゲット上のバッファーに書式設定された文字列を送信コンピューター。 文字列は、このような印刷が無効になっている場合を除きに自動的にホスト コンピューター上のデバッガー コマンド ウィンドウに表示されます。

一般に、このバッファーに送信されるメッセージは、デバッガー コマンド ウィンドウで自動的に表示されます。 ただし、この表示は、グローバル フラグ (gflags.exe) ユーティリティを無効にできます。 さらに、この表示は自動的にないローカル カーネル デバッグ中に。 詳細については、[、による DbgPrint バッファー](reading-and-filtering-debugging-messages.md#the-dbgprint-buffer)を参照してください。

**! による dbgprint**拡張子 (かどうか自動印刷を無効になっています) に関係なく表示するには、このバッファーの内容が原因です。 フィルターで除外されたコンポーネントと重要度レベルに基づいてメッセージは表示されません。 (このフィルター処理の詳細については、「[読み取りとデバッグ メッセージのフィルタ リング](reading-and-filtering-debugging-messages.md)。)

 

 





