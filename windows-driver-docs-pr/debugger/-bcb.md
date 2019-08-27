---
title: bcb
description: Bcb 拡張機能は、指定されたバッファー制御ブロックを表示します。
ms.assetid: 4e98e900-5e9d-40a4-9c39-4dc3611d8ea3
keywords:
- キャッシュマネージャー
- bcb Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bcb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 01dc65c9f4f8860c5ca7e43e312373d7b848f176
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025286"
---
# <a name="bcb"></a>!bcb


**! Bcb**拡張機能では、指定されたバッファー制御ブロックが表示されます。

```dbgcmd
!bcb Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
バッファー制御ブロックのアドレスを指定します。

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
<td align="left"><p>使用できません (「解説」を参照してください)</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

キャッシュ管理の詳細については、Microsoft Windows SDK のドキュメントと、Mark Russinovich と David ソロモンを参照してください。

その他のキャッシュ管理拡張機能については、 [ **! cchelp**](-cchelp.md)拡張機能を使用してください。

<a name="remarks"></a>コメント
-------

この拡張機能は、Windows 2000 でのみ使用できます。 Windows XP 以降では、dt nt を使用します[ **。\_** ](dt--display-type-.md)バッファー制御ブロックを直接表示する BCB Address コマンド。

 

 





