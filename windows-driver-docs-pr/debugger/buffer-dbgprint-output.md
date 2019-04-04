---
title: Buffer DbgPrint Output
description: Buffer DbgPrint Output
ms.assetid: af97c484-3a37-4c86-8828-12a0ea1c8c0e
keywords:
- バッファーによる DbgPrint の出力 (グローバル フラグ)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: db5634202fcb99544309cf2304aebdc3ddad9aa9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570689"
---
# <a name="buffer-dbgprint-output"></a>Buffer DbgPrint Output


## <span id="ddk_buffer_dbgprint_output_dtools"></span><span id="DDK_BUFFER_DBGPRINT_OUTPUT_DTOOLS"></span>


**バッファーによる DbgPrint 出力**フラグは、デバッガーからの出力を抑制します**による DbgPrint**、 **DbgPrintEx**、 **KdPrint**、および **。KdPrintEx**呼び出し。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>省略形</strong></p></td>
<td align="left"><p>ddp</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>16 進数の値</strong></p></td>
<td align="left"><p>0x08000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>シンボリック名</strong></p></td>
<td align="left"><p>FLG_DISABLE_DBGPRINT</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Destination (公開先)</strong></p></td>
<td align="left"><p>システム全体のレジストリ エントリ、カーネル フラグ</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

デバッガーの出力を抑制、ときに、カーネル デバッガーで自動的に表示されません。 ただし、メッセージは常に送信、による DbgPrint バッファーを使用してアクセスできる、 [ **! による dbgprint** ](-dbgprint.md)デバッガー拡張機能。

デバッガーと通信する関数については、[デバッガーに送信する出力](sending-output-to-the-debugger.md)を参照してください。

 

 





