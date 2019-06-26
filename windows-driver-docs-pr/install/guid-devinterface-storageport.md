---
title: GUID_DEVINTERFACE_STORAGEPORT
description: GUID_DEVINTERFACE_STORAGEPORT
ms.assetid: 58146169-102b-4355-82d0-ea60979bf901
keywords:
- GUID_DEVINTERFACE_STORAGEPORT デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_STORAGEPORT
api_location:
- Ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 030a8a2227b4487d42cb0b84f2da8b303df710c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386421"
---
# <a name="guiddevinterfacestorageport"></a>GUID_DEVINTERFACE_STORAGEPORT


GUID_DEVINTERFACE_STORAGEPORT[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている[記憶装置ポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-port-drivers)します。

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
<td align="left"><p>GUID_DEVINTERFACE_STORAGEPORT</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{2ACCFE60-C130-11D2-B082-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ポートのデバイスの記憶域用のシステムが指定したドライバーは、オペレーティング システムと記憶域デバイス アダプターの存在をアプリケーションに通知する GUID_DEVINTERFACE_STORAGEPORT のインスタンスを登録します。

記憶装置ドライバーの詳細については、次を参照してください。[記憶装置ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-drivers)します。

[**StoragePortClassGuid** ](storageportclassguid.md) GUID_DEVINTERFACE_STORAGEPORT デバイス インターフェイスのクラスの古い識別子です。 このクラスの新しいインスタンスは、代わりに GUID_DEVINTERFACE_STORAGEPORT を使用します。

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


[**StoragePortClassGuid**](storageportclassguid.md)

 

 






