---
title: ks.pciaudio
description: Ks.pciaudio 拡張機能は、PortCls に現在接続されている Fdo の一覧を表示します。
ms.assetid: 30d74f14-1cff-4b18-996a-8c91c20edebe
keywords:
- デバッグ ks.pciaudio Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.pciaudio
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b73db84e86a5829cb22b763fd79cceb31f620887
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336223"
---
# <a name="kspciaudio"></a>!ks.pciaudio


**! Ks.pciaudio**拡張機能の Fdo PortCls に現在接続されている一覧を表示します。

```dbgcmd
!ks.pciaudio [Options] [Level]  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
(省略可能)。 表示される情報の種類を指定します。 *オプション*次のビットの組み合わせにすることができます。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
ストリームの実行の一覧を表示します。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
すべてのストリームの一覧を表示します。

<span id="Bit_3__0x4_"></span><span id="bit_3__0x4_"></span><span id="BIT_3__0X4_"></span>ビット 3 (0x4)  
出力には、ストリームが表示されます。 *レベル*このビットを設定するとにのみ意味を持ちます。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *レベル*   
省略可能であり、ビット 3 設定されている場合にのみ適用可能な*オプション*します。 レベルは、の場合と同じ[ **! ks.dump**](-ks-dump.md)します。

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

詳細については、次を参照してください。[ストリーミングのカーネル デバッグ](kernel-streaming-debugging.md)します。

<a name="remarks"></a>注釈
-------

出力の例を次に示します **! ks.pciaudio**:

```dbgcmd
kd> !ks.pciaudio
1 Audio FDOs found:
 Functional Device 8299be18 [\Driver\smwdm]
```

 

 





