---
title: DEVPKEY_Device_HardwareIds
description: DEVPKEY_Device_HardwareIds
ms.assetid: 4bfd50b3-027f-4f79-8bff-d0c92c1b2386
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_HardwareIds
topic_type:
- apiref
api_name:
- DEVPKEY_Device_HardwareIds
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 310e744d9b6505c3c8fb46a3776de79a62b1c3f2
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418293"
---
# <a name="devpkey_device_hardwareids"></a>DEVPKEY_Device_HardwareIds


DEVPKEY_DEVICE_HardwareIds デバイスプロパティは、デバイスインスタンスのハードウェア識別子の一覧を表します。

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
<td align="left"><p>DEVPKEY_Device_HardwareIds</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>データ形式</strong></p></td>
<td align="left">"<em>id1</em>\ 0<em>hw id</em>2 \ 0...<em>hw-idn</em>\ 0 \ 0 "</td>
</tr>
<tr class="even">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>対応する SPDRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPDRP_HARDWAREID</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

DEVPKEY_DEVICE_HardwareIds の値は、デバイスをインストールする INF ファイルの [ [**Inf*モデル*] セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-models-section)によって提供されるデバイスの*hw id*エントリ値によって設定されます。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出して、DEVPKEY_DEVICE_HardwareIds の値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートしていますが、DEVPKEY_DEVICE_HardwareIds プロパティキーをサポートしていません。 代わりに、対応する SPDRP_HARDWAREID 識別子を使用して、これらの以前のバージョンの Windows でプロパティの値にアクセスできます。 以前のバージョンの Windows でこのプロパティ値にアクセスする方法の詳細については、「[デバイスインスタンス](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)へのアクセス SPDRP_Xxx のプロパティ」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**INF*モデル*セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-models-section)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






