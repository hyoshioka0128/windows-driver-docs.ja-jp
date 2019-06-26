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
ms.openlocfilehash: 77d7b4c575ed8d69940dddeb77f24fe2eb615539
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386426"
---
# <a name="guiddevinterfacepartition"></a>GUID_DEVINTERFACE_PARTITION


GUID_DEVINTERFACE_PARTITION[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)パーティション デバイス用に定義されます。

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

システム提供[記憶装置ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-drivers) GUID_DEVINTERFACE_PARTITION の子デバイスではパーティションのインスタンスを登録、[記憶装置](https://docs.microsoft.com/windows-hardware/drivers/storage/index)します。

[**PartitionClassGuid** ](partitionclassguid.md) GUID_DEVINTERFACE_PARTITION デバイス インターフェイスのクラスの古い識別子です。 このクラスの新しいインスタンスは、代わりに GUID_DEVINTERFACE_PARTITION を使用します。

<a name="requirements"></a>必要条件
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

 

 






