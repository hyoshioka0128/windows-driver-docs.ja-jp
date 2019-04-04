---
title: GUID_DEVINTERFACE_FLOPPY
description: GUID_DEVINTERFACE_FLOPPY
ms.assetid: 07d47168-a179-40ef-843b-c1efa6acb395
keywords:
- GUID_DEVINTERFACE_FLOPPY デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_FLOPPY
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2816980d0a469f18048dda8769254b3be7a4c049
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574154"
---
# <a name="guiddevinterfacefloppy"></a>GUID_DEVINTERFACE_FLOPPY


GUID_DEVINTERFACE_FLOPPY[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)フロッピー ディスクが定義されている[記憶装置](https://msdn.microsoft.com/library/windows/hardware/ff566969)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>GUID_DEVINTERFACE_FLOPPY</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{53F56311-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

フロッピー ディスク記憶域デバイスの場合、システムが指定したストレージ クラス ドライバーは、フロッピー ディスクの記憶域デバイスに対する GUID_DEVINTERFACE_FLOPPY のインスタンスを登録します。

記憶域[サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)WDK に含める、[フロッピー ドライバー](https://go.microsoft.com/fwlink/p/?linkid=256192)古い形式の識別子を使用するサンプル[ **FloppyClassGuid** ](floppyclassguid.md)にGUID_DEVINTERFACE_FLOPPY デバイス インターフェイスのクラスのインスタンスを登録します。

ストレージ ドライバーについては、[記憶装置ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff566976)を参照してください。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntddstor.h (include Ntddstor.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FloppyClassGuid**](floppyclassguid.md)

 

 






