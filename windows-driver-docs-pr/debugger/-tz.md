---
title: tz
description: 指定された電源温度のゾーン構造は、tz 拡張機能によって表示されます。
ms.assetid: f3cc9e54-a0db-4095-b707-380ec1dacf59
keywords:
- 温度ゾーン
- tz Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tz
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2f413108c5e30712958efd5cbabe9e46842c33b0
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025163"
---
# <a name="tz"></a>!tz


**! Tz**拡張機能には、指定された電源温度のゾーン構造が表示されます。

```dbgcmd
!tz [Address]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
表示するパワーサーマルゾーンのアドレス。 このパラメーターを省略すると、対象のコンピューター上のすべてのサーマルゾーンが表示されます。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

システムの電源機能を表示するには、 [ **! pocaps**](-pocaps.md) extension コマンドを使用します。 システムの電源ポリシーを表示するには、 [ **! popolicy**](-popolicy.md)拡張コマンドを使用します。 電源機能と電源ポリシーの詳細については、Windows Driver Kit (WDK) のドキュメントと*Microsoft windows の内部構造*を参照してください。これには、Mark Russinovich と David ソロモンが使用されます。

<a name="remarks"></a>コメント
-------

いつでも実行を停止するには、CTRL + BREAK (WinDbg の場合) または CTRL + C (KD の場合) を押します。

 

 





