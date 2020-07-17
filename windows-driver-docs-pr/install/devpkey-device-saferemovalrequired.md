---
title: DEVPKEY_Device_SafeRemovalRequired
description: DEVPKEY_Device_SafeRemovalRequired
ms.assetid: a162e259-21aa-40d9-a65a-af175a59df6a
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_SafeRemovalRequired
topic_type:
- apiref
api_name:
- DEVPKEY_Device_SafeRemovalRequired
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ef7906313cc671605a1e20ad970f8c2917643765
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418416"
---
# <a name="devpkey_device_saferemovalrequired"></a>DEVPKEY_Device_SafeRemovalRequired


DEVPKEY_Device_SafeRemovalRequired デバイスプロパティは、ホットプラグデバイスインスタンスでコンピューターからの安全な削除が必要かどうかを示すブール値を表します。

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
<td align="left"><p>DEVPKEY_Device_SafeRemovalRequired</p></td>
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

ホットプラグデバイスインスタンスのこのプロパティの値が DEVPROP_TRUE の場合、デバイスインスタンスはコンピューターからの安全な削除を必要とします。 この場合、Windows では、タスクバーの右側の通知領域に [**ハードウェアの安全な削除**] アイコンが表示されます。 ユーザーがこのアイコンをクリックすると、システムによって**ハードウェアの安全な削除**が開始されます。 このプログラムを使用すると、ユーザーは、デバイスインスタンスをコンピューターから削除する前に、そのデバイスインスタンスを削除するための準備を行うようにシステムに指示できます。

**メモ**   デバイスインスタンスが光学ディスクドライブなどのリムーバブルメディアデバイスの場合、デバイスインスタンスにメディアを挿入し、[DEVPKEY_Device_SafeRemovalRequired] プロパティの値を [DEVPROP_TRUE] に設定する必要があります。 両方が true の場合、デバイスインスタンスは、ハードウェアの**安全な削除**プログラムに表示されます。

 

Windows プラグアンドプレイ (PnP) は、次の条件に当てはまる場合に、ホットプラグデバイスインスタンスがシステムからの安全な削除を必要とすることを決定します。

-   デバイスインスタンスは、現在システムに接続されています。

-   デバイスインスタンスは起動されているか、システムによって自動的に取り出すことができます。

-   デバイスインスタンスの CM_DEVCAP_SURPRISEREMOVALOK デバイス機能ビットが設定されていません。 デバイスの機能の詳細については、「 [**SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)」を参照してください。

-   デバイスインスタンスの[**DEVPKEY_Device_SafeRemovalRequiredOverride**](devpkey-device-saferemovalrequiredoverride.md)デバイスプロパティが DEVPROP_FALSE に設定されていません。

    **メモ**   PnP は、DEVPKEY_Device_SafeRemovalRequiredOverride デバイスプロパティが DEVPROP_TRUE に設定されている場合に、ホットプラグデバイスで安全な削除が必要であることを無条件に判断します。

     

-   デバイスインスタンスは、その親デバイスインスタンスから直接取り外しられているか、デバイスツリーにリムーバブルの先祖があります。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出して、DEVPKEY_Device_SafeRemovalRequired の値を取得できます。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Devpkey (Devpkey を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DEVPKEY_Device_SafeRemovalRequiredOverride**](devpkey-device-saferemovalrequiredoverride.md)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)

 

 






