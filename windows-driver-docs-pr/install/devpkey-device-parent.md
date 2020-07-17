---
title: DEVPKEY_Device_Parent
description: DEVPKEY_Device_Parent
ms.assetid: 3d56ee87-cbf8-49d7-86ab-30e3862a1a1d
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_Parent
topic_type:
- apiref
api_name:
- DEVPKEY_Device_Parent
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dc7b8d0d5fa1334dcd84ea17ad3dd5d8036177e6
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418468"
---
# <a name="devpkey_device_parent"></a>DEVPKEY_Device_Parent


DEVPKEY_Device_Parent デバイスプロパティは、デバイスインスタンスの親のデバイスインスタンス識別子を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr>
<th>属性</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_Parent</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>適用なし</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出して、DEVPKEY_Device_Parent プロパティの値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 では、このプロパティは直接サポートされていません。 これらの以前のバージョンの Windows でデバイスの関係プロパティを取得する方法については、「[デバイスの関係の取得](https://docs.microsoft.com/windows-hardware/drivers/install/retrieving-device-relations)」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






