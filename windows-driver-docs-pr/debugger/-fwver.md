---
title: fwver
description: Fwver 拡張機能には、Itanium のファームウェア バージョンが表示されます。
ms.assetid: 0b1a2fb2-9df6-45b4-bd5b-cbcdde38ddad
keywords:
- Windows デバッグ fwver
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- fwver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b70059e40e3e30233eb1900849181607d0a5cb10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574923"
---
# <a name="fwver"></a>!fwver


**! Fwver**拡張機能には、Itanium のファームウェア バージョンが表示されます。

```dbgcmd
!fwver 
```

**重要な**  このコマンドが 10.0.14257 Windows デバッガーのバージョンでは非推奨以降されてし、は現在利用できません。

 

## <span id="ddk__fwver_dbg"></span><span id="DDK__FWVER_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

この拡張機能のコマンドは、Itanium のターゲット コンピューターでのみ使用できます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、Intel アーキテクチャ マニュアルを参照してください。

<a name="remarks"></a>コメント
-------

この拡張機能からの出力の例を次に示します。

```dbgcmd
kd> !fwver

Firmware Version

   Sal Revision:        0
   SAL_A_VERSION:       0
   SAL_B_VERSION:       0
   PAL_A_VERSION:       6623
   PAL_B_VERSION:       6625
   smbiosString:        W460GXBS2.86E.0117A.P08.200107261041
```

 

 





