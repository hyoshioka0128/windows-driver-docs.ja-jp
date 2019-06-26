---
title: DEVPKEY_Device_EjectionRelations
description: DEVPKEY_Device_EjectionRelations
ms.assetid: 3b3a0d6f-4163-40a8-817d-924f63871e51
keywords:
- DEVPKEY_Device_EjectionRelations デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_EjectionRelations
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e01b03b1c89e578f4f6c3069cb060e9f8a42071f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378262"
---
# <a name="devpkeydeviceejectionrelations"></a>DEVPKEY_Device_EjectionRelations


DEVPKEY_Device_EjectionRelations デバイス プロパティを表します、 [**取り出し関係**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)デバイス インスタンス。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_EjectionRelations</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>該当なし</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) DEVPKEY_Device_EjectionRelations の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティを直接サポートされません。 以前のバージョンの Windows でのデバイスのリレーションのプロパティを取得する方法については、次を参照してください。[デバイス関係の取得](https://docs.microsoft.com/windows-hardware/drivers/install/retrieving-device-relations)します。

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

 

 






