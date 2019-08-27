---
title: tzinfo
description: Tzinfo 拡張機能は、指定された温度ゾーン情報構造の内容を表示します。
ms.assetid: a30826d8-b7c5-4fbc-a3c3-b7a994eaf7fe
keywords:
- サーマルゾーン情報
- tzinfo Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tzinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6af9551157a543c2fe8dc5b51aa53e38a876e481
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025154"
---
# <a name="tzinfo"></a>!tzinfo


**! Tzinfo**拡張機能は、指定された温度ゾーン情報構造の内容を表示します。

```dbgcmd
!tzinfo Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
表示するサーマルゾーン情報構造のアドレス。

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

 

 





