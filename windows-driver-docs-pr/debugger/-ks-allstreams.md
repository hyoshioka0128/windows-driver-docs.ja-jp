---
title: ks.allstreams
description: Ks.allstreams 拡張機能では、デバイス全体のツリー、システムでデバイスをストリーミングするすべてのカーネルを検索します。
ms.assetid: 3a9f4ad4-a3aa-46dc-887d-c83296bc8f84
keywords:
- デバッグ ks.allstreams Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.allstreams
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f91666c28cdbe5560c7a2583027e5cfbe101b00a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550146"
---
# <a name="ksallstreams"></a>!ks.allstreams


**! Ks.allstreams**拡張機能で、デバイス全体のツリーについて説明し、システムでデバイスをストリーミングするすべてのカーネルを検索します。

```dbgcmd
!ks.allstreams [Flags] [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
(省略可能)。 表示される情報の種類を指定します。 *フラグ*次のビットの組み合わせにすることができます。 既定値は 0x1 です。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
ストリームが表示をによりします。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
プロキシ インスタンスの表示をによりします。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
キューに置かれた Irp が表示をによりします。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
すべてのストリームの書式設定されていない表示が表示をによりします。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>Bit 5 (0x20)  
すべてのストリームの形式の書式設定されていない表示が表示をによりします。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *レベル*   
(省略可能)。 0 ~ 7 で表示する詳細のレベルを指定の値を大きく表示徐々 に詳細なスケールします。 使用可能なすべての詳細を表示するには、7 の値を指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[ストリーミングのカーネル デバッグ](kernel-streaming-debugging.md)を参照してください。

<a name="remarks"></a>注釈
-------

このコマンドは実行に時間がかかることができます (1 分間は珍しくありません)。

次の例に示します、 **! ks.allstreams**表示。

```dbgcmd
kd> !allstreams 
6 Kernel Streaming FDOs found:
    Functional Device 82a17690 [\Driver\smwdm]
    Functional Device 8296eb08 [\Driver\wdmaud]
    Functional Device 82490388 [\Driver\sysaudio]
    Functional Device 82970cb8 [\Driver\MSPQM]
    Functional Device 824661b8 [\Driver\MSPCLOCK]
    Functional Device 8241c020 [\Driver\avssamp]
```

 

 





