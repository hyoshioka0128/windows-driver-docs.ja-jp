---
title: GUID_DEVINTERFACE_I2C
description: GUID_DEVINTERFACE_I2C
ms.assetid: 765cecb7-b8ea-48ef-bdab-742da722e169
keywords:
- GUID_DEVINTERFACE_I2C デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_I2C
api_location:
- Dispmprt.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 89e950f8c734fb491a204b5a383ac21e87a1bdbe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840631"
---
# <a name="guid_devinterface_i2c"></a>GUID_DEVINTERFACE_I2C


GUID_DEVINTERFACE_I2C [device インターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)は、 [Windows Vista の表示ドライバーモデル](https://docs.microsoft.com/windows-hardware/drivers/display/windows-vista-display-driver-model-design-guide)のコンテキストで動作し、子デバイスを監視するために I2C トランザクションを実行するディスプレイアダプタードライバー用に定義されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ID</p></td>
<td align="left"><p>GUID_DEVINTERFACE_I2C</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{2564AA4F-DDDB-4495-B497-6AD4A84 163D7}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

ドライバーは、このデバイスインターフェイスクラスのインスタンスを登録して、オペレーティングシステムと、監視子デバイスでトランザクションを実行する I2C インターフェイスの存在をアプリケーションに通知します。

ディスプレイミニポートドライバーがこの[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)に対して直接呼び出し I2C インターフェイスをサポートしている場合、カーネルモードコンポーネントは、ミニポートドライバーの[**DxgkDdiQueryInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)関数を呼び出し、GUID_DEVINTERFACE_I2C インターフェイスの種類を指定します。

I2C バスの詳細については、「[ディスプレイアダプターの I2c バスおよび子デバイス](https://docs.microsoft.com/windows-hardware/drivers/display/i2c-bus-and-child-devices-of-the-display-adapter)」を参照してください。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Dispmprt (Dispmprt. h を含む)</td>
</tr>
</tbody>
</table>

 

 





