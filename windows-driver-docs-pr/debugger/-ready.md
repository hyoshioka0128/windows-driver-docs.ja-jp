---
title: 準備
description: 準備ができて、拡張機能は、システムの準備完了状態に各スレッドについての概要情報を表示します。
ms.assetid: 1dc94ceb-7d06-4874-999c-059c86f51ea0
keywords:
- 読み取りスレッドのスレッド
- 準備が Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ready
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 096c3cf2b89b08b56345c245f888bb35e8a3b507
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330812"
---
# <a name="ready"></a>!ready


**! 準備**拡張機能が準備完了状態でシステムの各スレッドについての概要情報を表示します。

```dbgcmd
!ready [Flags]
```

## <a name="span-idddkreadydbgspanspan-idddkreadydbgspanparameters"></a><span id="ddk__ready_dbg"></span><span id="DDK__READY_DBG"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
表示する詳細レベルを指定します。 *フラグ*次のビットの組み合わせにすることができます。 場合*フラグ*は 0、最小限の情報のみが表示されます。 既定では 0x6 です。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
スレッドの待機状態が表示をによりします。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
このビット 1 (0x2) なしで含まれる場合、この影響を与えません。 これは、ビット 1 と共に含まれていますが場合、スレッドにスタック トレースが表示されます。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
戻り値のアドレスでは、スタック ポインターを追加するには、各関数と (Itanium システム) 上の表示、 **bsp**値を登録します。 関数の引数の表示は表示されません。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
リターン アドレスのみを含めるには、各関数の表示します。引数とスタック ポインターが抑制されます。

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

スレッドのスケジューリングと準備完了の状態については、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 

<a name="remarks"></a>注釈
-------

この拡張機能からの出力は以下のこと[ **! スレッド**](-thread.md)準備スレッドのみが表示されます、および優先順位が高い順に並べ替えのことを除いて、します。

 

 





