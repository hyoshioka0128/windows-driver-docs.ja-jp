---
title: DEVPKEY_Device_RemovalPolicyOverride
description: DEVPKEY_Device_RemovalPolicyOverride
ms.assetid: 74b90422-9187-4bbb-9be6-cf2d11e29686
keywords:
- DEVPKEY_Device_RemovalPolicyOverride デバイスとドライバーのインストール
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
ms.openlocfilehash: c9b7d2cfb5002f3a1a7764efeaad35de645e6952
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378129"
---
# <a name="devpkeydeviceremovalpolicyoverride"></a>DEVPKEY_Device_RemovalPolicyOverride


DEVPKEY_Device_RemovalPolicyOverride デバイス プロパティは、デバイスのインスタンスの削除ポリシーの上書きを表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_RemovalPolicyOverride</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>読み取りおよび書き込みアクセス アプリケーションをインストールしてインストーラー</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPDRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPDRP_REMOVAL_POLICY_OVERRIDE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

DEVPKEY_Device_RemovalPolicyOverride の値がいずれか、CM_REMOVAL_POLICY_*Xxx* Cfgmgr32.h で定義されている値。

DEVPKEY_Device_RemovalPolicyOverride の値を取得するには呼び出すことによって[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)呼び出すことによってこの値を設定することもできますまたは[  **。SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)します。

Windows Server 2003 および Windows XP は、このプロパティをサポートは DEVPKEY_Device_RemovalPolicyOverride プロパティのキーをサポートしていません。 代わりに、Windows の以前のバージョンのプロパティの値へのアクセスに対応する SPDRP_REMOVAL_POLICY_OVERRIDE 識別子を使用することができます。 Windows の以前のバージョンでこのプロパティの値にアクセスする方法については、次を参照してください。[デバイス インスタンス SPDRP_Xxx プロパティへのアクセス](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h (Devpkey.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

 

 






