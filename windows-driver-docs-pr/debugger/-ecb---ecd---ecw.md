---
title: ecb ecd、ecw
description: Ecb、ecd、および ecw 拡張機能は、PCI 構成領域に書き込みます。
ms.assetid: ab5f5164-7666-48ac-aeba-5f238c2625f6
keywords:
- ecb ecd、ecw Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ecb, ecd, ecw
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 07fb432e992f16690b2bdc9ab70914bd32f9f355
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336867"
---
# <a name="ecb-ecd-ecw"></a>!ecb、!ecd、!ecw


**。 Ecb**、 **! ecd**、および **! ecw** PCI 構成の領域に拡張機能を記述します。

```dbgcmd
!ec Bus.Device.Function Offset Data 
```

## <a name="span-idddkecdbgspanspan-idddkecdbgspanparameters"></a><span id="ddk__ec__dbg"></span><span id="DDK__EC__DBG"></span>パラメーター


<span id="_______Bus______"></span><span id="_______bus______"></span><span id="_______BUS______"></span> *バス*   
バスを指定します。 *バス*0 xff までの範囲のことができます。

<span id="_______Device______"></span><span id="_______device______"></span><span id="_______DEVICE______"></span> *デバイス*   
デバイスのデバイスのスロット番号を指定します。

<span id="_______Function______"></span><span id="_______function______"></span><span id="_______FUNCTION______"></span> *関数*   
デバイスのスロットの関数の数を指定します。

<span id="_______Offset______"></span><span id="_______offset______"></span><span id="_______OFFSET______"></span> *オフセット*   
書き込み先のアドレスを指定します。

<span id="_______Data______"></span><span id="_______data______"></span><span id="_______DATA______"></span> *データ*   
書き込まれる値を指定します。 **。 Ecb**拡張機能、*データ*1 バイト (2 桁の 16 進数) である必要があります。 **! Ecw**拡張機能、*データ*(4 桁の 16 進数) の 1 つの単語にする必要があります。 **! Ecd**拡張機能、*データ*1 つの DWORD (16 進数 8) にする必要があります。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kext.dll</p></td>
</tr>
</tbody>
</table>

 

これらの拡張機能のコマンドは、x86 ベースの移行先のコンピューターでのみ使用できます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

参照してください[プラグ アンド プレイ デバッグ](plug-and-play-debugging.md)この拡張機能コマンドとその他の例のアプリケーション。 PCI バスについては、Windows Driver Kit (WDK) ドキュメントを参照してください。

<a name="remarks"></a>注釈
-------

これらの拡張機能のコマンドを使用してのシーケンスを記述することはできません*データ*値。 これは、この拡張機能の繰り返しの使用によってのみ実行できます。

PCI の構成領域を表示する使用[ **! pci 100**](-pci.md)*Bus デバイス関数*します。

 

 





