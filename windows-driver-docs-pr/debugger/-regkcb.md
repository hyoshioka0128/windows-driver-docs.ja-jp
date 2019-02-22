---
title: regkcb
description: Regkcb 拡張機能では、レジストリ キーの制御ブロックが表示されます。
ms.assetid: d6898025-9ba2-4b3b-819b-d7b23d8ee525
keywords:
- Windows デバッグ regkcb
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- regkcb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d775c6c0caa7826c8a81dd198c0bf2f9e14be128
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560408"
---
# <a name="regkcb"></a>! regkcb


**! Regkcb**拡張機能には、レジストリ キーの制御ブロックが表示されます。

```dbgcmd
!regkcb Address 
```

## <a name="span-idddkregkcbdbgspanspan-idddkregkcbdbgspanparameters"></a><span id="ddk__regkcb_dbg"></span><span id="DDK__REGKCB_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
キーの制御ブロックのアドレスを指定します。

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
<td align="left"><p>利用不可</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

レジストリとそのコンポーネントについては、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。

<a name="remarks"></a>注釈
-------

Windows 2000 で **! regkcb**特定のレジストリ キーの制御ブロックが表示されます。

Windows XP および Windows での以降のバージョンで、 [ **! reg** ](-reg.md)拡張機能のコマンドを代わりに使用する必要があります。

すべてのレジストリ キーには、そのアクセス許可などのプロパティを含む制御ブロックがあります。

 

 





