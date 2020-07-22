---
title: dbgprint
description: Dbgprint 拡張機能では、以前に DbgPrint バッファーに送信された文字列が表示されます。
ms.assetid: bf25ac2a-5a07-43df-946b-3b2237b1816b
keywords:
- dbgprint の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dbgprint
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 609e4f68f38d5c7a56d25b43c0ffd21544b485f4
ms.sourcegitcommit: 3ec971f54122b77408433f7f1e59c467099fb4de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86873833"
---
# <a name="dbgprint"></a>!dbgprint


**! Dbgprint**拡張機能には、以前に**dbgprint**バッファーに送信された文字列が表示されます。

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
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

**Dbgprint**、 **KdPrint**、 **dbgprintex**、 **KdPrintEx**の詳細については、「[出力をデバッガーに送信する](sending-output-to-the-debugger.md)」を参照してください。

<a name="remarks"></a>解説
-------

カーネルモードルーチン**Dbgprint**、 **KdPrint**、 **Dbgprintex**、および**KdPrintEx**は、ターゲットコンピューター上のバッファーに書式設定された文字列を送信します。 この文字列は、このような印刷機能が無効になっていない限り、ホストコンピューター上のデバッガーコマンドウィンドウに自動的に表示されます。

一般に、このバッファーに送信されたメッセージは、デバッガーのコマンドウィンドウに自動的に表示されます。 ただし、この表示は、グローバルフラグ (gflags.exe) ユーティリティを使用して無効にすることができます。 また、この表示はローカルカーネルデバッグ中に自動的には表示されません。 詳細については、「[デバッグメッセージの読み取りとフィルター処理](reading-and-filtering-debugging-messages.md)」の「Dbgprint Buffer」を参照してください。

**! Dbgprint**拡張機能を使用すると、このバッファーの内容が表示されます (自動印刷が無効になっているかどうかに関係なく)。 コンポーネントと重要度レベルに基づいてフィルターで除外されたメッセージは表示されません。 (このフィルター処理の詳細については、「[デバッグメッセージの読み取りとフィルター処理](reading-and-filtering-debugging-messages.md)」を参照してください)。

 

 





