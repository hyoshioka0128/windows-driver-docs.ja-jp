---
title: DEVPKEY_Device_SafeRemovalRequiredOverride
description: DEVPKEY_Device_SafeRemovalRequiredOverride
ms.assetid: 8289effe-3849-41bf-b870-69e3d8cb8850
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_SafeRemovalRequiredOverride
topic_type:
- apiref
api_name:
- DEVPKEY_Device_SafeRemovalRequiredOverride
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: debf67c3e3b03604448ab9e8ced10e0fdbdeb969
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418417"
---
# <a name="devpkey_device_saferemovalrequiredoverride"></a>DEVPKEY_Device_SafeRemovalRequiredOverride


DEVPKEY_Device_SafeRemovalRequiredOverride デバイスプロパティは、デバイスインスタンスの安全な削除の上書きを表します。

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
<td align="left"><p>DEVPKEY_Device_SafeRemovalRequiredOverride</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>インストールアプリケーションとインストーラーによる読み取りおよび書き込みアクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

このデバイスプロパティを使用して、Windows プラグアンドプレイ (PnP) が[**DEVPKEY_Device_SafeRemovalRequired**](devpkey-device-saferemovalrequired.md)デバイスプロパティの値を計算するために使用するヒューリスティックの結果をオーバーライドできます。 このオーバーライドは次のように実行されます。

-   デバイスの DEVPKEY_Device_SafeRemovalRequiredOverride プロパティが DEVPROP_TRUE に設定されていて、デバイスインスタンスがリムーバブルであるか、またはリムーバブルの先祖を持っている場合、PnP は DEVPKEY_Device_SafeRemovalRequired デバイスプロパティを DEVPROP_TRUE に設定し、ヒューリスティックを使用しません。

    **メモ**   デバイスインスタンスは、リムーバブルデバイスの機能が設定されている場合は、リムーバブルと見なされます。 詳細については、「[リムーバブルデバイスの機能の概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-the-removable-device-capability)」を参照してください。

     

-   DEVPKEY_Device_SafeRemovalRequiredOverride デバイスプロパティが DEVPROP_TRUE に設定されていて、デバイスインスタンス (または先祖) がリムーバブルでない場合、PnP は DEVPKEY_Device_SafeRemovalRequired を DEVPROP_FALSE に設定し、ヒューリスティックを使用しません。

-   DEVPKEY_Device_SafeRemovalRequiredOverride デバイスプロパティが設定されていないか、または DEVPROP_FALSE に設定されている場合、PnP は DEVPKEY_Device_SafeRemovalRequired デバイスプロパティをヒューリスティックを使用して決定された値に設定します。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出すことによって DEVPKEY_Device_SafeRemovalRequiredOverride の値を取得できます。 この値は、 [**Setupdisetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)を呼び出すことによって設定することもできます。

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


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

 

 






