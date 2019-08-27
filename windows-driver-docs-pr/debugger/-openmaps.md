---
title: openmaps
description: Openmaps 拡張機能は、指定された共有キャッシュマップの参照バッファー制御ブロック (BCBs) と仮想アドレス制御ブロック (VACBs) を表示します。
ms.assetid: 4ecce331-c18e-462a-807a-b8929059b897
keywords:
- BCB (バッファー制御ブロック)
- VACB (仮想アドレス制御ブロック)
- 共有キャッシュマップ
- キャッシュマネージャー
- openmaps の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- openmaps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 35ed5b7cc429e3bdc2505171b642aad0a7970598
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025200"
---
# <a name="openmaps"></a>!openmaps


**! Openmaps**拡張機能は、指定された共有キャッシュマップの参照バッファー制御ブロック (bcbs) と仮想アドレス制御ブロック (VACBs) を表示します。

```dbgcmd
!openmaps Address [Flag]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
共有キャッシュマップのアドレスを指定します。

<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span>*フラグ*   
表示するコントロールブロックを決定します。 *フラグ*が**1**の場合、デバッガーはすべてのコントロールブロックを表示します。 *フラグ*が**0**の場合は、参照されているコントロールブロックだけが表示されます。 既定値は **0**です。

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

キャッシュ管理の詳細については、Microsoft Windows SDK のドキュメントと、Mark Russinovich と David ソロモンを参照してください。

その他のキャッシュ管理拡張機能の詳細については、 [ **! cchelp**](-cchelp.md)拡張機能に関する説明を参照してください。

 

 





