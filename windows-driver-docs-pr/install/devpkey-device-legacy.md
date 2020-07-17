---
title: DEVPKEY_Device_Legacy
description: DEVPKEY_Device_Legacy
ms.assetid: a2af9881-3aa3-45a7-9b80-cb507460957e
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_Legacy
topic_type:
- apiref
api_name:
- DEVPKEY_Device_Legacy
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b3a105c79c64c1ecff6946c4015bc705a8b0ac5c
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418332"
---
# <a name="devpkey_device_legacy"></a>DEVPKEY_Device_Legacy


DEVPKEY_Device_Legacy デバイスプロパティは、デバイスが、デバイスの PnP 以外のドライバーが読み込まれたときに、プラグアンドプレイ (PnP) マネージャーによって自動的に作成された、ルートで列挙されたデバイスかどうかを示すブール値を表します。

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
<td align="left"><p>DEVPKEY_Device_Legacy</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

Pnp マネージャは、デバイスの PnP 以外のドライバーが読み込まれたときに、ルートで列挙されたデバイスとしてデバイスを自動的に作成した場合、DEVPKEY_Device_Reported の値を DEVPROP_TRUE に設定します。 それ以外の場合は、PnP マネージャーによってプロパティの値が DEVPROP_FALSE に設定されます。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出して、DEVPKEY_Device_Legacy の値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 では、このプロパティはサポートされていません。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






