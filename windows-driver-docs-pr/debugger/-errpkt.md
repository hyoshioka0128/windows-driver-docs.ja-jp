---
title: errpkt
description: Errpkt 拡張機能には、Windows Hardware Error Architecture (WHEA) ハードウェアエラーパケットの内容が表示されます。
ms.assetid: cf4b1dfa-3b15-45d4-b5e2-1da7cdbca350
keywords:
- errpkt Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- errpkt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4e9fbcc06b5cd8db3d3cc14c19640c00ef92be9e
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534839"
---
# <a name="errpkt"></a>!errpkt


**! Errpkt**拡張機能には、Windows ハードウェアエラーアーキテクチャ (WHEA) ハードウェアエラーパケットの内容が表示されます。

```dbgcmd
!errpkt Address 
```

## <a name="span-idddk__ubp_dbgspanspan-idddk__ubp_dbgspanparameters"></a><span id="ddk__ubp_dbg"></span><span id="DDK__UBP_DBG"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
ハードウェアエラーパケットのアドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows Server 2003</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows Vista 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

この拡張機能は、Windows Vista 以降のバージョンの Windows でのみ使用できます。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

[**! Whea**](-whea.md)および[**! errrec**](-errrec.md)拡張機能を使用して、追加の whea 情報を表示できます。 WHEA に関する一般的な情報については、Windows Driver Kit (WDK) のドキュメントの「 [Windows ハードウェアエラーアーキテクチャ (WHEA)](https://docs.microsoft.com/windows-hardware/drivers/whea/) 」を参照してください。

<a name="remarks"></a>注釈
-------

次の例は、 **! errpkt**拡張機能の出力を示しています。

```dbgcmd
3: kd> !errpkt fffffa8007cf44da 
   WHEA Error Packet Info Section (@ fffffa8007cf44da)
   Flags            : 0x00000000
   Size             : 0x218
   RawDataLength    : 0x392
   Context          : 0x0000000000000000
   ErrorType        : 0x0 - Processor
   ErrorSeverity    : 0x1 - Fatal
   ErrorSourceId    : 0x0
   ErrorSourceType  : 0x0 - MCE
   Version          : 00000002
   Cpu              : 0000000000000002
   RawDataFormat    : 0x2 - Intel64 MCA

   Raw Data         : Located @ FFFFFA8007CF45F2

Processor Error: (Internal processor error)
This error means either the processor is damaged or perhaps
voltage and/or temperature thresholds have been exceeded.
If the problem continues to occur, replace the processor.
Processor Number : 2
Bank Number      : 0
   Status  :                0
   Address : 0000000000000000 (I)
   Misc    : 0000000000000000 (I)
```

 

 





