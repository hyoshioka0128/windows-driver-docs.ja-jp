---
title: コールバック (callback)
description: コールバックの拡張機能では、指定したスレッドのトラップに関連するコールバック データが表示されます。
ms.assetid: afbd7884-d63d-4e37-a437-91bc910a3ae2
keywords:
- システムのトラップ用のコールバック データ
- Windows デバッグ コールバック
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- callback
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6d8eb5975d8075b68bfbd67bd42965fef24ceae9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336897"
---
# <a name="callback"></a>!callback


**! コールバック**拡張機能には、指定したスレッドのトラップに関連するコールバック データが表示されます。

```dbgsyntax
!callback Address [Number]
```

## <a name="span-idddkcallbackdbgspanspan-idddkcallbackdbgspanparameters"></a><span id="ddk__callback_dbg"></span><span id="DDK__CALLBACK_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
スレッドの 16 進数のアドレスを指定します。 これは、-1 または省略すると、現在のスレッドが使用されます。

<span id="_______Number______"></span><span id="_______number______"></span><span id="_______NUMBER______"></span> *数*   
必要なコールバック フレームの数を指定します。 このフレームは、表示されています。

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

 

この拡張機能のコマンドは、x86 ベースの移行先のコンピューターでのみ使用できます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

システムのトラップについては、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

システムがシステムのトラップが発生しない場合、この拡張機能には、有用なデータは生成されません。

 

 





