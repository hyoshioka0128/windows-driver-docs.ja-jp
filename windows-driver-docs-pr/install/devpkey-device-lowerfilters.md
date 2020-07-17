---
title: DEVPKEY_Device_LowerFilters
description: DEVPKEY_Device_LowerFilters
ms.assetid: 7ee0421f-7c4e-463a-ab79-1616c6837bdc
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_LowerFilters
topic_type:
- apiref
api_name:
- DEVPKEY_Device_LowerFilters
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 50a4e1b2c853692c6c27c89e5101ed58e6d03e8f
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418554"
---
# <a name="devpkey_device_lowerfilters"></a>DEVPKEY_Device_LowerFilters


DEVPKEY_Device_LowerFilters デバイスプロパティは、デバイスインスタンスにインストールされている下位レベルのフィルタードライバーのサービス名の一覧を表します。

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
<td align="left"><p>DEVPKEY_Device_LowerFilters</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>インストールアプリケーションとインストーラーによる読み取りおよび書き込みアクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPDRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPDRP_LOWERFILTERS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

DEVPKEY_Device_LowerFilters プロパティの値は、デバイスに対して下位レベルのデバイスフィルタードライバーがインストールされている場合に設定されます。 デバイスフィルタードライバーをインストールする方法の詳細については、「[フィルタードライバーのインストール](https://docs.microsoft.com/windows-hardware/drivers/install/installing-a-filter-driver)」を参照してください。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)と[**setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)を呼び出して、DEVPKEY_Device_LowerFilters の値を取得および設定できます。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートしていますが、DEVPKEY_Device_LowerFilters プロパティキーをサポートしていません。 代わりに、対応する SPDRP_LOWERFILTERS 識別子を使用して、これらの以前のバージョンの Windows でプロパティの値にアクセスできます。 以前のバージョンの Windows でこのプロパティ値にアクセスする方法の詳細については、「[デバイスインスタンス](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)へのアクセス SPDRP_Xxx のプロパティ」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

 

 






