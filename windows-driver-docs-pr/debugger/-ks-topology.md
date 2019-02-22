---
title: ks.topology
description: Ks.topology 拡張機能は、フィルター オブジェクトに最も近いは、内部のトポロジの並べ替えられたグラフを表示します。
ms.assetid: 04ef6920-c022-4136-a42a-800679fe7ff4
keywords:
- デバッグ ks.topology Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.topology
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aea4718827c4d81d26e5a88d4c874cd469012faa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558880"
---
# <a name="kstopology"></a>!ks.topology


**! Ks.topology**拡張機能には、フィルターに最も近いは、内部のトポロジの並べ替えられたグラフが表示されます。*オブジェクト*します。

```dbgcmd
!ks.topology Object [Level] [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *オブジェクト*   
グラフのベースとして使用するオブジェクトへのポインターを指定します。 ファイル オブジェクト、IRP、暗証番号 (pin)、フィルター、またはその他の KS オブジェクトへのポインターを指定できます。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *レベル*   
(省略可能)。 0 ~ 7 で表示する詳細のレベルを指定の値を大きく表示徐々 に詳細なスケールします。 使用可能なすべての詳細を表示するには、7 の値を指定します。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
現在使用できません。

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

ヘルプについては、発行、 **! ks.topology**引数なしでコマンド。

このコマンドが実行するしばらく時間がかかることに注意してください。

 

 





