---
title: GUID_DEVINTERFACE_PARTITION
description: GUID_DEVINTERFACE_PARTITION
ms.assetid: c489b62a-167d-47a9-bfeb-fdd40cc8dece
keywords:
- GUID_DEVINTERFACE_PARTITION デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_PARTITION
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8ae3d375364af04c44885430f53ea11c30213b9a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532752"
---
# <a name="guiddevinterfacepartition"></a>GUID_DEVINTERFACE_PARTITION


GUID_DEVINTERFACE_PARTITION[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)パーティション デバイス用に定義されます。

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
<td align="left"><p>GUID_DEVINTERFACE_PARTITION</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{53F5630A-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

システム提供[記憶装置ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff566976) GUID_DEVINTERFACE_PARTITION の子デバイスではパーティションのインスタンスを登録、[記憶装置](https://msdn.microsoft.com/library/windows/hardware/ff566969)します。

[**PartitionClassGuid** ](partitionclassguid.md) GUID_DEVINTERFACE_PARTITION デバイス インターフェイスのクラスの古い識別子です。 このクラスの新しいインスタンスは、代わりに GUID_DEVINTERFACE_PARTITION を使用します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Microsoft Windows 2000 および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddstor.h (include Ntddstor.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**PartitionClassGuid**](partitionclassguid.md)

 

 






