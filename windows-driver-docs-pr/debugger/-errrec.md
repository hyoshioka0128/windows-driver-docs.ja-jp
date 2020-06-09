---
title: errrec
description: Errrec 拡張機能には、Windows ハードウェアエラーアーキテクチャ (WHEA) のエラーレコードの内容が表示されます。
ms.assetid: 372e4700-0cd7-468d-98e8-b0ead4ebc92f
keywords:
- errrec Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- errrec
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ef3e272f68bb29fa8851f6f82123653ff54000a1
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534837"
---
# <a name="errrec"></a>!errrec


**! Errrec**拡張機能には、Windows ハードウェアエラーアーキテクチャ (WHEA) のエラーレコードの内容が表示されます。

```dbgcmd
!errrec Address 
```

## <a name="span-idddk__ubp_dbgspanspan-idddk__ubp_dbgspanparameters"></a><span id="ddk__ubp_dbg"></span><span id="DDK__UBP_DBG"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
エラーレコードのアドレスを指定します。

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

[**! Whea**](-whea.md)および[**! errpkt**](-errpkt.md)拡張機能を使用して、追加の whea 情報を表示できます。 WHEA に関する一般的な情報については、Windows Driver Kit (WDK) のドキュメントの「 [Windows ハードウェアエラーアーキテクチャ (WHEA)](https://docs.microsoft.com/windows-hardware/drivers/whea/) 」を参照してください。

<a name="remarks"></a>注釈
-------

次の例では、 [**! whea**](-whea.md)拡張を使用してエラーレコードのアドレスを取得する方法を示しています。このレコードの内容は、 **! errrec**拡張機能によって表示できます。

```dbgcmd
3: kd> !whea 
Error Source Table @ fffff800019ca250
13 Error Sources
Error Source 0 @ fffffa80064132c0
   Notify Type      : Machine Check Exception
   Type             : 0x0 (MCE)
   Error Count      : 8
   Record Count     : 10
   Record Length    : c3e
   Error Records    : wrapper @ fffffa8007cf4000  record @ fffffa8007cf4030

. . . . 

# 3: kd> !errrec fffffa8007cf4030 
===============================================================================
## Common Platform Error Record @ fffffa8007cf4030
-------------------------------------------------------------------------------
Revision      : 2.1
Record Id     : 01c9c7ff04e0ff7d
Severity      : Fatal (1)
Length        : 1730
Creator       : Microsoft
Notify Type   : Machine Check Exception
Timestamp     : 4/28/2009 12:54:47
Flags         : 0x00000000
# 
===============================================================================
## Section 0     : Processor Generic
-------------------------------------------------------------------------------
Descriptor    @ fffffa8007cf40b0
Section       @ fffffa8007cf4188
Offset        : 344
Length        : 192
Flags         : 0x00000001 Primary
Severity      : Fatal

No valid data fields are present.
# 
===============================================================================
## Section 1     : {390f56d5-ca86-4649-95c4-73a408ae5834}
-------------------------------------------------------------------------------
Descriptor    @ fffffa8007cf40f8
Section       @ fffffa8007cf4248
Offset        : 536
Length        : 658
Flags         : 0x00000000
Severity      : Fatal

*** Unknown section format ***
# 
===============================================================================
## Section 2     : Error Packet
-------------------------------------------------------------------------------
Descriptor    @ fffffa8007cf4140
Section       @ fffffa8007cf44da
Offset        : 1194
Length        : 536
Flags         : 0x00000000
Severity      : Fatal

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

 

 





