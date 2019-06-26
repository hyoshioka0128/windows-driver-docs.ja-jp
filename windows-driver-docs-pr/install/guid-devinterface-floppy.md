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
ms.openlocfilehash: 4bfc07403d03e979fcd243a70bed3fee16085c85
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372718"
---
# <a name="guiddevinterfacefloppy"></a>GUID_DEVINTERFACE_FLOPPY


GUID_DEVINTERFACE_FLOPPY[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)フロッピー ディスクが定義されている[記憶装置](https://docs.microsoft.com/windows-hardware/drivers/storage/index)します。

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

ストレージ ドライバーについては、次を参照してください。[記憶装置ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-drivers)します。

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

 

 






