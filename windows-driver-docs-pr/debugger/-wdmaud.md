---
title: wdmaud
description: さまざまな WDM オーディオ (WDMAud) 構造体を表示します。
ms.assetid: fa41e3e2-a767-4c8c-9604-e3ea924ac571
keywords:
- Windows デバッグ wdmaud
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdmaud
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aca91133acf2c075587b69fe8666b0d68be915c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327953"
---
# <a name="wdmaud"></a>!wdmaud


さまざまな WDM オーディオ (WDMAud) 構造体を表示します。

```dbgcmd
!wdmaud Address Flags
```

## <a name="span-idddkwdmauddbgspanspan-idddkwdmauddbgspanparameters"></a><span id="ddk__wdmaud_dbg"></span><span id="DDK__WDMAUD_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
表示される構造体のアドレスを指定します。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
表示する情報を指定します。 これは 0x1、0x2、0x4、および 0x8 ビットの 1 つだけ含める必要があります。 0x100 ビットは、これらのいずれかに追加できます。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
Wdmaud.sys に送信されたすべての Ioctl の一覧を表示します。 これを使用する場合*アドレス*のアドレスを指定する必要があります、 **WdmaIoctlHistoryListHead**します。 0x100 ビットが設定されている場合、表示も含まれています、 **pContext**で送信された各 IOCTL します。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
保留中として WDMAud がマークされているすべての Irp の一覧を表示します。 これを使用する場合*アドレス*のアドレスを指定する必要があります、 **WdmaPendingIrpListHead**します。 0x100 ビットが設定されている場合、表示には各 IRP が割り当てられているコンテキストも含まれています。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
WDMAud が割り当てられているすべての MDLs の一覧を表示します。 これを使用する場合*アドレス*のアドレスを指定する必要があります、 **WdmaAllocatedMdlListHead**します。 0x100 ビットが設定されている場合、表示には各 MDL が割り当てられているコンテキストも含まれています。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
Wdmaud.sys にアタッチされているすべてのアクティブなコンテキストの一覧を表示します。 これを使用する場合*アドレス*のアドレスを指定する必要があります、 **WdmaContextListHead**します。 0x100 ビットが設定されている場合、表示には各コンテキストの構造体のデータ メンバーも含まれています。

<span id="Bit_8__0x100_"></span><span id="bit_8__0x100_"></span><span id="BIT_8__0X100_"></span>ビット 8 (0x100)  
詳細な情報が追加ディスプレイをによりします。

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
<td align="left"><p>利用不可</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

WDM オーディオ アーキテクチャとオーディオ ドライバーについては、Windows Driver Kit (WDK) ドキュメントを参照してください。

<a name="remarks"></a>注釈
-------

Wdmaud.sys にアタッチされているコンテキスト (**pContext**) 各デバイスの状態データの大部分が含まれています。 Wdmaud.drv は新しいプロセスに読み込まれる、たびに wdmaud.sys 到着が通知されます。 Wdmaud.drv がアンロードされるたびに、wdmaud.sys はそのコンテキストで行われたすべての割り当てをクリーンアップします。

 

 





