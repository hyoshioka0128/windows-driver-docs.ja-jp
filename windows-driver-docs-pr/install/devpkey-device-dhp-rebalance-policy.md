---
title: DEVPKEY_Device_DHP_Rebalance_Policy
description: DEVPKEY_Device_DHP_Rebalance_Policy
ms.assetid: a882a114-9d1b-41ca-ab24-c2cdda952177
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_DHP_Rebalance_Policy
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DHP_Rebalance_Policy
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e4d271cec462f2e2b286f6056837412eefaddd4e
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418352"
---
# <a name="devpkey_device_dhp_rebalance_policy"></a>DEVPKEY_Device_DHP_Rebalance_Policy


DEVPKEY_Device_DHP_Rebalance_Policy デバイスプロパティは、[動的ハードウェアパーティション分割 (DHP)](https://docs.microsoft.com/windows-hardware/drivers/kernel/dynamic-hardware-partitioning-techniques)プロセッサのホット追加操作に従って、デバイスがリソースの再調整に参加するかどうかを示す値を表します。

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
<td align="left"><p>DEVPKEY_Device_DHP_Rebalance_Policy</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>アプリケーションとサービスによる読み取りおよび書き込みアクセス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

Windows Server 2008 以降のバージョンの Windows Server を実行している動的にパーティション分割されたサーバーでは、新しいプロセッサがシステムに動的に追加されるたびに、オペレーティングシステムによってシステム全体のリソース調整が開始されます。 デバイスの DEVPKEY_Device_DHP_Rebalance_Policy プロパティは、デバイスがリソースの再調整に参加するかどうかを決定します。 デバイスは、次のような場合にリソースの再調整に参加します。

-   DEVPKEY_Device_DHP_Rebalance_Policy デバイスのプロパティが存在しません。

-   デバイスプロパティが存在し、デバイスプロパティの値が設定されていません。

-   デバイスプロパティは存在し、デバイスプロパティの値は2に設定されています。

[デバイスの DEVPKEY_Device_DHP_Rebalance_Policy] プロパティが存在し、プロパティの値が1に設定されている場合、新しいプロセッサがシステムに動的に追加されるときに、デバイスはリソースの再バランシングに関与しません。

デバイスの[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)は、デバイスの inf ファイルの [ [**Inf バージョン] セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)で指定します。

ネットワークアダプター (Class = Net) デバイスセットアップクラスでのデバイスの既定の動作では、新しいプロセッサがシステムに動的に追加されるときに、クラスのメンバーはリソースの再配分に関与しません。 他のすべてのデバイスセットアップクラスでのデバイスの既定の動作では、新しいプロセッサがシステムに動的に追加されるときに、メンバーはリソースの再調整に関与します。

このデバイスプロパティは、デバイスが他の理由で開始されるリソース再調整に参加するかどうかには影響しません。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)と[**setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)を呼び出すことによって、DEVPKEY_Device_DHP_Rebalance_Policy プロパティにアクセスできます。

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
<td align="left"><p>Windows server 2008 以降のバージョンの Windows Server で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Devpkey (Devpkey を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

 

 






