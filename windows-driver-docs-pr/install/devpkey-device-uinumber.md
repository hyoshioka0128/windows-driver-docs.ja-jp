---
title: DEVPKEY_Device_UINumber
description: DEVPKEY_Device_UINumber
ms.assetid: 81bd0b71-909d-49c3-8d6c-258c57f80644
keywords:
- DEVPKEY_Device_UINumber デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_UINumber
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 026aa822aab5764c015ca1804db8daff3e357781
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828898"
---
# <a name="devpkey_device_uinumber"></a>DEVPKEY_Device_UINumber


DEVPKEY_Device_UINumber device プロパティは、ユーザーインターフェイス項目に表示できるデバイスインスタンスの番号を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_UINumber</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティアクセス</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPDRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPDRP_UI_NUMBER</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>必須ではない</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Windows は、DEVPKEY_Device_UINumber の値を、デバイスインスタンスの[**DEVICE_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)構造体の uinumber メンバーの値に設定します。 デバイスインスタンスのバスドライバーは、 [**IRP_MN_QUERY_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)要求に応答してこの値を返します。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出して、DEVPKEY_Device_UINumber の値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 では、このプロパティはサポートされていますが、DEVPKEY_Device_UINumber プロパティキーはサポートされていません。 代わりに、対応する SPDRP_UI_NUMBER 識別子を使用して、これらの以前のバージョンの Windows でプロパティの値にアクセスできます。 これらの以前のバージョンの Windows でこのプロパティ値にアクセスする方法の詳細については、「[デバイスインスタンス SPDRP_Xxx のプロパティ](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)へのアクセス」を参照してください。

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
<td align="left"><p>Windows Vista 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey (Devpkey を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DEVICE_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)

[**IRP_MN_QUERY_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






