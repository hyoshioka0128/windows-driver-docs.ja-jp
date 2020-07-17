---
title: DEVPKEY_Device_DeviceDesc
description: DEVPKEY_Device_DeviceDesc
ms.assetid: 02b88ee7-d825-48d9-99ef-aac8e6748141
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_DeviceDesc
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DeviceDesc
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fb8a5e39c63dae087401769e11d4d521f2897d20
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418358"
---
# <a name="devpkey_device_devicedesc"></a>DEVPKEY_Device_DeviceDesc


DEVPKEY_Device_DeviceDesc デバイスプロパティは、デバイスインスタンスの説明を表します。

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
<td align="left"><p>DEVPKEY_Device_DeviceDesc</p></td>
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
<td align="left"><p><strong>対応する SPDRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPDRP_DEVICEDESC</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>はい</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

DEVPKEY_Device_DeviceDesc の値は、デバイスをインストールする INF ファイルの [ [**Inf モデル] セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-models-section)によって指定された*デバイスの説明*のエントリ値によって設定されます。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出して、DEVPKEY_DEVICE_DeviceDesc の値を取得できます。

[デバイスインスタンスの[**DEVPKEY_NAME**](devpkey-name--device-instance-.md) ] プロパティの値を取得して、ユーザーインターフェイス項目に表示されるデバイスの名前を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートしていますが、DEVPKEY_Device_DeviceDesc プロパティキーをサポートしていません。 代わりに、これらの以前のバージョンの Windows では、対応する SPDRP_DEVICEDESC 識別子を使用してプロパティの値にアクセスします。 以前のバージョンの Windows でこのプロパティ値にアクセスする方法の詳細については、「[デバイスインスタンス](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)へのアクセス SPDRP_Xxx のプロパティ」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**DEVPKEY_NAME (デバイス インスタンス)**](devpkey-name--device-instance-.md)

[**INF Models セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-models-section)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






