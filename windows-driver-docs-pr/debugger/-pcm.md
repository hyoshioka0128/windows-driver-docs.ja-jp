---
title: pcm
description: 指定したプライベートキャッシュマップが pcm 拡張機能に表示されます。 この拡張機能は、Windows 2000 でのみ使用できます。
ms.assetid: a6880ad0-5326-4bea-ac84-3311a2ec01da
keywords:
- プライベートキャッシュマップ
- キャッシュマネージャー
- pcm Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pcm
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f1c151f67bfdc65d9e8e3abc2f08939b8f745b9a
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025197"
---
# <a name="pcm"></a>!pcm


**! Pcm**拡張機能は、指定されたプライベートキャッシュマップを表示します。 この拡張機能は、Windows 2000 でのみ使用できます。

```dbgcmd
!pcm Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
プライベートキャッシュマップのアドレスを指定します。

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

その他のキャッシュ管理拡張機能の詳細については、 [ **! cchelp**](-cchelp.md)拡張機能のリファレンスを参照してください。

<a name="remarks"></a>コメント
-------

この拡張機能は、Windows 2000 でのみサポートされています。 Windows XP 以降のバージョンの Windows では、dt nt を使用します[ **。\_プライベート\_キャッシュ\_マップアドレス**](dt--display-type-.md)コマンド。

 

 





