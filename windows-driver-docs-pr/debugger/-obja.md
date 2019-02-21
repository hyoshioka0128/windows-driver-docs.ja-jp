---
title: obja
description: Obja 拡張機能は、オブジェクト マネージャーで、オブジェクトの属性を表示します。
ms.assetid: dc263ec2-72bf-4cb1-8583-4e9142d0bbdb
keywords:
- オブジェクト マネージャー
- Windows デバッグ obja
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- obja
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ca660e5a95b68af9766bb8c9c1e2e9ddb484161f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538871"
---
# <a name="obja"></a>! obja


**! Obja**拡張機能オブジェクト マネージャーで、オブジェクトの属性を表示します。

```dbgcmd
!obja Address
```

## <a name="span-idddkobjadbgspanspan-idddkobjadbgspanparameters"></a><span id="ddk__obja_dbg"></span><span id="DDK__OBJA_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
確認するオブジェクトのヘッダーの 16 進数のアドレスを指定します。

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
Ext.dll Kdextx86.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

オブジェクトとオブジェクト マネージャーについては、Microsoft Windows SDK ドキュメントに、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

指定したオブジェクトに関連する属性の一覧が表示されます。 有効な属性は次のとおりです。

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

 

 





