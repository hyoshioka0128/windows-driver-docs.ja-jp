---
title: DEVPKEY_Device_Reported
description: DEVPKEY_Device_Reported
ms.assetid: dfec9e24-4d4e-42e4-a229-ad3d060fb1b5
keywords:
- DEVPKEY_Device_Reported デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_Reported
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 587bd00bdc6be1ea72dc8beff6446468825fec6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840642"
---
# <a name="devpkey_device_reported"></a>DEVPKEY_Device_Reported


DEVPKEY_Device_Reported device プロパティは、デバイスインスタンスがルートで列挙されたデバイスであるかどうかを示すブール値を表します。これは、デバイスのドライバーが[**IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)を呼び出すことによってプラグアンドプレイ (PnP) マネージャーに報告したものです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_Reported</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティアクセス</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>必須ではない</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

デバイスがルートで列挙されたデバイスである場合、PnP マネージャーは DEVPKEY_Device_Reported の値を DEVPROP_TRUE に設定します。これは、デバイスのドライバーが IoReportDetectedDevice を呼び出して PnP マネージャーに報告したものです。 それ以外の場合は、PnP マネージャーによってプロパティの値が DEVPROP_FALSE に設定されます。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出して、DEVPKEY_Device_Reported の値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 では、このプロパティはサポートされていません。

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


[**IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






