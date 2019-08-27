---
title: obja
description: Obja 拡張では、オブジェクトマネージャー内のオブジェクトの属性が表示されます。
ms.assetid: dc263ec2-72bf-4cb1-8583-4e9142d0bbdb
keywords:
- オブジェクトマネージャー
- obja Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- obja
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 56afcda226e8e242a5b61aa96df777ecd1815f91
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025202"
---
# <a name="obja"></a>!obja


**! Obja**拡張では、オブジェクトマネージャー内のオブジェクトの属性が表示されます。

```dbgcmd
!obja Address
```

## <a name="span-idddk__obja_dbgspanspan-idddk__obja_dbgspanparameters"></a><span id="ddk__obja_dbg"></span><span id="DDK__OBJA_DBG"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
確認するオブジェクトヘッダーの16進数のアドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Ext .dll Kdextx86</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

オブジェクトとオブジェクトマネージャーの詳細については、Microsoft Windows SDK のドキュメント、Windows Driver Kit (WDK) のドキュメント、および Mark Russinovich と David ソロモンによる*Microsoft windows の内部構造*に関するドキュメントを参照してください。

<a name="remarks"></a>コメント
-------

指定したオブジェクトに関連する属性が一覧表示されます。 有効な属性は次のとおりです。

```cpp
#define OBJ_INHERIT             0x00000002L
#define OBJ_PERMANENT           0x00000010L
#define OBJ_EXCLUSIVE           0x00000020L
#define OBJ_CASE_INSENSITIVE    0x00000040L
#define OBJ_OPENIF              0x00000080L
#define OBJ_OPENLINK            0x00000100L
#define OBJ_VALID_ATTRIBUTES    0x000001F2L
```

以下に例を示します。

```dbgcmd
kd> !obja 80967768
Obja +80967768 at 80967768:
        OBJ_INHERIT
        OBJ_PERMANENT
        OBJ_EXCLUSIVE
```

 

 





