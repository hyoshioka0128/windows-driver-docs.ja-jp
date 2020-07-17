---
title: DEVPKEY_DeviceClass_DHPRebalanceOptOut
description: DEVPKEY_DeviceClass_DHPRebalanceOptOut デバイスプロパティは、動的ハードウェアパーティション分割 (DHP) プロセッサのホットアド操作が発生した後に、デバイスクラス全体がリソースの再バランシングに参加するかどうかを示す値を表します。プロパティ keyDEVPKEY_DeviceClass_DHPRebalanceOptOutProperty-アプリケーションとサービスによるデータ型 identifierDEVPROP_TYPE_BOOLEANProperty accessRead および write アクセス。ローカライズされていません。 Windows Server 2008 以降のバージョンの Windows Server を実行している動的にパーティション分割されたサーバーでは、新しいプロセッサがシステムに動的に追加されるたびに、オペレーティングシステムによってシステム全体のリソース調整が開始されます。 デバイスクラスは、次の状況では、DEVPKEY_DeviceClass_DHPRebalanceOptOut デバイスプロパティが存在しない場合に、リソースの再調整に関与します。デバイスプロパティが存在し、デバイスプロパティの値が設定されていません。デバイスプロパティが存在し、デバイスプロパティの値が FALSE に設定されています。[デバイスの DEVPKEY_DeviceClass_DHPRebalanceOptOut] プロパティが存在し、プロパティの値が TRUE に設定されている場合、新しいプロセッサがシステムに動的に追加されるときに、デバイスクラスはリソースの再配分に関与しません。デバイスのデバイスセットアップクラスは、デバイスの INF ファイルの [INF バージョン] セクションで指定します。ネットワークアダプター (クラス Net) のこのプロパティの既定値は TRUE です。 他のすべてのデバイスセットアップクラスに対するこのプロパティの既定値は FALSE です。このデバイスプロパティは、デバイスクラスが他の理由で開始されるリソース再調整に参加するかどうかには影響しません。DEVPKEY_DeviceClass_DHPRebalanceOptOut プロパティにアクセスするには、SetupDiGetClassProperty プロパティと Setupdigetclassproperty を呼び出します。
ms.assetid: e620ef24-b65d-4cf6-a21d-ffecad5804b4
keywords:
- デバイスとドライバーのインストールの DEVPKEY_DeviceClass_DHPRebalanceOptOut
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_DHPRebalanceOptOut
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9d5e51ecd60206e6a54364743c32cddeda44bbf4
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418538"
---
# <a name="devpkey_deviceclass_dhprebalanceoptout"></a>DEVPKEY_DeviceClass_DHPRebalanceOptOut


DEVPKEY_DeviceClass_DHPRebalanceOptOut デバイスプロパティは、[動的ハードウェアパーティション分割 (DHP)](https://docs.microsoft.com/windows-hardware/drivers/kernel/dynamic-hardware-partitioning-techniques)プロセッサのホットアド操作が発生した後に、デバイスクラス全体がリソースの再バランシングに参加するかどうかを示す値を表します。

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
<td align="left"><p>DEVPKEY_DeviceClass_DHPRebalanceOptOut</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
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

 

**解説**

Windows Server 2008 以降のバージョンの Windows Server を実行している動的にパーティション分割されたサーバーでは、新しいプロセッサがシステムに動的に追加されるたびに、オペレーティングシステムによってシステム全体のリソース調整が開始されます。 デバイスクラスは、次のような場合にリソースの再調整に関与します。

-   DEVPKEY_DeviceClass_DHPRebalanceOptOut デバイスのプロパティが存在しません。

-   デバイスプロパティが存在し、デバイスプロパティの値が設定されていません。

-   デバイスプロパティが存在し、デバイスプロパティの値が**FALSE**に設定されています。

[デバイスの DEVPKEY_DeviceClass_DHPRebalanceOptOut] プロパティが存在し、プロパティの値が**TRUE**に設定されている場合、新しいプロセッサがシステムに動的に追加されるときに、デバイスクラスはリソースの再配分に関与しません。

デバイスの[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)は、デバイスの inf ファイルの [ [**Inf バージョン] セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)で指定します。

ネットワークアダプター (クラス = Net) のこのプロパティの既定値は**TRUE**です。 他のすべてのデバイスセットアップクラスに対するこのプロパティの既定値は**FALSE**です。

このデバイスプロパティは、デバイスクラスが他の理由で開始されるリソース再調整に参加するかどうかには影響しません。

DEVPKEY_DeviceClass_DHPRebalanceOptOut プロパティにアクセスするには、 [**Setupdigetclassproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)プロパティと[**setupdigetclassproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw)を呼び出します。

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


[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiSetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw)

 

 






