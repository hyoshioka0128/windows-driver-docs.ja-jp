---
title: DEVPKEY_Device_RemovalPolicyOverride
description: DEVPKEY_Device_RemovalPolicyOverride
ms.assetid: 74b90422-9187-4bbb-9be6-cf2d11e29686
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_RemovalPolicyOverride
topic_type:
- apiref
api_name:
- DEVPKEY_Device_RemovalPolicyOverride
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5797bdbcfb8ff0594e2c7212437175a4d8e4d476
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418449"
---
# <a name="devpkey_device_removalpolicyoverride"></a>DEVPKEY_Device_RemovalPolicyOverride


DEVPKEY_Device_RemovalPolicyOverride デバイスプロパティは、デバイスインスタンスの削除ポリシーのオーバーライドを表します。

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
<td align="left"><p>DEVPKEY_Device_RemovalPolicyOverride</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>インストールアプリケーションとインストーラーによる読み取りおよび書き込みアクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPDRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPDRP_REMOVAL_POLICY_OVERRIDE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

DEVPKEY_Device_RemovalPolicyOverride の値は、Cfgmgr32 で定義されている CM_REMOVAL_POLICY_*Xxx*値の1つです。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出すことによって DEVPKEY_Device_RemovalPolicyOverride の値を取得できます。また、 [**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)を呼び出すことによって、この値を設定することもできます。

Windows Server 2003 および Windows XP では、このプロパティはサポートされていますが、DEVPKEY_Device_RemovalPolicyOverride のプロパティキーはサポートされていません。 代わりに、対応する SPDRP_REMOVAL_POLICY_OVERRIDE 識別子を使用して、これらの以前のバージョンの Windows でプロパティの値にアクセスできます。 以前のバージョンの Windows でこのプロパティ値にアクセスする方法の詳細については、「[デバイスインスタンス](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)へのアクセス SPDRP_Xxx のプロパティ」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

 

 






