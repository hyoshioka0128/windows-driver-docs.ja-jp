---
title: scm
description: Scm 拡張では、指定された共有キャッシュマップが表示されます。
ms.assetid: 4333ee14-ca28-43af-b132-210996328af2
keywords:
- 共有キャッシュマップ
- キャッシュマネージャー
- scm Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- scm
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c4ba38a988d1f1ec92b75fbe05db4b17863dc9b9
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025157"
---
# <a name="scm"></a>!scm


**! Scm**拡張機能は、指定された共有キャッシュマップを表示します。

```dbgcmd
!scm Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
共有キャッシュマップのアドレスを指定します。

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
<td align="left"><p>利用不可</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

キャッシュ管理の詳細については、Microsoft Windows SDK のドキュメントと、Mark Russinovich と David ソロモンを参照してください。

その他のキャッシュ管理拡張機能の詳細については、 [ **! cchelp**](-cchelp.md)拡張機能に関する説明を参照してください。

<a name="remarks"></a>コメント
-------

Windows XP 以降のバージョンの Windows では、dt nt を使用します[ **。\_\_\_** ](dt--display-type-.md) **! Scm**ではなく、共有キャッシュマップのアドレスコマンド。

 

 





