---
title: DEVPKEY_Device_InstallState
description: DEVPKEY_Device_InstallState
ms.assetid: 3bebb3d6-96bb-4c7c-8a7a-c5bf29cb3a2a
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_InstallState
topic_type:
- apiref
api_name:
- DEVPKEY_Device_InstallState
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4fabf1b03bb475a98d916f401e9310c52a65e6b4
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418282"
---
# <a name="devpkey_device_installstate"></a>DEVPKEY_Device_InstallState


DEVPKEY_Device_InstallState デバイスプロパティは、デバイスインスタンスのインストール状態を表します。

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
<td align="left"><p>DEVPKEY_Device_InstallState</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-uint32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_UINT32&lt;/strong&gt;](devprop-type-uint32.md)"><strong>DEVPROP_TYPE_UINT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPDRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPDRP_INSTALL_STATE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

Windows は、DEVPKEY_Device_InstallState の値を、Cfgmgr32 で定義されている CM_INSTALL_STATE_*Xxx*値のいずれかに設定します。 CM_INSTALL_STATE_*Xxx*の値は、 [**DEVICE_INSTALL_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_device_install_state)列挙値に対応します。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出して、DEVPKEY_Device_InstallState の値を取得できます。

Windows Server 2003 および Windows XP では、このプロパティはサポートされていますが、DEVPKEY_Device_InstallState のプロパティキーはサポートされていません。 代わりに、対応する SPDRP_INSTALL_STATE 識別子を使用して、これらの以前のバージョンの Windows でプロパティの値にアクセスできます。 以前のバージョンの Windows でこのプロパティ値にアクセスする方法の詳細については、「[デバイスインスタンス](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)へのアクセス SPDRP_Xxx のプロパティ」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






