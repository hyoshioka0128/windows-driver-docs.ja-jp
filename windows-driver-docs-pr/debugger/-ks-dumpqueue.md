---
title: ks.dumpqueue
description: Ks.dumpqueue 拡張機能では、指定した AVStream オブジェクトに関連付けられているキューまたはポートのクラス オブジェクトに関連付けられたストリーム情報が表示されます。
ms.assetid: d641b4e6-73d9-4c44-b2c6-0b6c688da368
keywords:
- デバッグ ks.dumpqueue Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.dumpqueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed7a37d652f4b91abec804e45a75ee91a46dac7f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336303"
---
# <a name="ksdumpqueue"></a>!ks.dumpqueue


**! Ks.dumpqueue**拡張機能が、指定した AVStream オブジェクトに関連付けられているキューまたはポートのクラス オブジェクトに関連付けられたストリームに関する情報を表示します。

```dbgcmd
!ks.dumpqueue Object [Level] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *オブジェクト*   
キューを表示するオブジェクトへのポインターを指定します。 *オブジェクト*CKsPin PKSPIN、PKSFILTER の型でなければなりません\*、CKsFilter\*、CKsQueue\*、CPortPin\*、または CPortFilter\*します。

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

詳細については、次を参照してください。[ストリーミングのカーネル デバッグ](kernel-streaming-debugging.md)します。

<a name="remarks"></a>注釈
-------

*オブジェクト*フィルターまたは pin である必要があります。 暗証番号 (pin)、1 つのキューが表示されます。 フィルターの場合は、複数のキューが表示されます。

このコマンドを実行する時間がかかることができます。

次の例に示します、 **! ks.dumpqueue**表示。

```dbgcmd
kd> !dumpqueue 829493c4
Filter 829493c4: Output Queue 82990e20:
 Queue 82990e20:
        Frames Received  : 1889
        Frames Waiting   : 3
        Frames Cancelled : 0
        And Gate 82949464 : count = 1, next = 00000000
    Frame Gate NULL
        Frame Header 82aaef78:
 NextFrameHeaderInIrp = 00000000
            OriginalIrp = 82169e48
            Mdl = 8292e358
            Irp = 82169e48
 StreamHeader = 8298dea0
            FrameBuffer = edba3000
            StreamHeaderSize = 00000000
            FrameBufferSize = 00025800
            Context = 00000000
            Refcount = 1
```

 

 





