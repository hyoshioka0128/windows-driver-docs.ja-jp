---
title: コールバック (callback)
description: コールバック拡張機能は、指定されたスレッドのトラップに関連するコールバックデータを表示します。
ms.assetid: afbd7884-d63d-4e37-a437-91bc910a3ae2
keywords:
- システムトラップのコールバックデータ
- コールバック (Windows デバッグ)
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- callback
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c2dae2bb6c84ddea65626f9bc6adeeacaf7b7413
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025282"
---
# <a name="callback"></a>!callback


**! Callback**拡張機能は、指定されたスレッドのトラップに関連するコールバックデータを表示します。

```dbgsyntax
!callback Address [Number]
```

## <a name="span-idddk__callback_dbgspanspan-idddk__callback_dbgspanparameters"></a><span id="ddk__callback_dbg"></span><span id="DDK__CALLBACK_DBG"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
スレッドの16進数のアドレスを指定します。 このが-1 であるか省略されている場合は、現在のスレッドが使用されます。

<span id="_______Number______"></span><span id="_______number______"></span><span id="_______NUMBER______"></span>*番号*   
目的のコールバックフレームの番号を指定します。 このフレームは、画面に表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

この拡張機能コマンドは、x86 ベースのターゲットコンピューターでのみ使用できます。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

システムトラップの詳細については、Windows Driver Kit (WDK) のドキュメントと*Microsoft windows の内部*(Mark Russinovich と David ソロモン) を参照してください。

<a name="remarks"></a>コメント
-------

システムトラップが発生していない場合、この拡張機能は有用なデータを生成しません。

 

 





