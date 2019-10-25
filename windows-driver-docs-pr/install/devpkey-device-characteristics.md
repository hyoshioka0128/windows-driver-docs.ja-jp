---
title: DEVPKEY_Device_Characteristics
description: DEVPKEY_Device_Characteristics
ms.assetid: 148557aa-2246-4cd9-9008-d920ffb64845
keywords:
- DEVPKEY_Device_Characteristics デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_Characteristics
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cc7179627086209df9f6d6f476f34bc7d601249a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828908"
---
# <a name="devpkey_device_characteristics"></a>DEVPKEY_Device_Characteristics


DEVPKEY_Device_Characteristics device プロパティは、デバイスインスタンスの特性を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_Characteristics</p></td>
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
<td align="left"><p>SPDRP_CHARACTERISTICS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>必須ではない</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

DEVPKEY_Device_Characteristics の値は、Wdm および Ntddk で定義されている FILE_*Xxx*ファイル特性フラグのビットごとの or です。 デバイスの特性フラグの詳細については、 [**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)の*DeviceCharacteristics*パラメーターと[デバイスの特性の指定](https://docs.microsoft.com/windows-hardware/drivers/kernel/specifying-device-characteristics)に関する説明を参照してください。

DEVPKEY_Device_Characteristics の値は、デバイスをインストールする[**Inf DDInstall. HW セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)に含まれている[**inf AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を使用して設定できます。

DEVPKEY_Device_Characteristics の値を取得するには、 [**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出します。

Windows Server 2003、Windows XP、および Windows 2000 では、このプロパティはサポートされていますが、DEVPKEY_Device_Characteristics プロパティキーはサポートされていません。 代わりに、対応する SPDRP_CHARACTERISTICS 識別子を使用して、これらの以前のバージョンの Windows でプロパティの値にアクセスできます。 これらの以前のバージョンの Windows でこのプロパティ値にアクセスする方法の詳細については、「[デバイスインスタンス SPDRP_Xxx のプロパティ](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)へのアクセス」を参照してください。

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


[**INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)

[**INF DDInstall. HW セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)

[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

 

 






