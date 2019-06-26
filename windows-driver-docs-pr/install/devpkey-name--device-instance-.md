---
title: DEVPKEY_NAME (デバイス インスタンス)
description: DEVPKEY_NAME (デバイス インスタンス)
ms.assetid: 4968a215-7e22-4d17-938c-4aa5289b2803
keywords:
- DEVPKEY_NAME (デバイス インスタンス) のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_NAME (Device Instance)
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e7c9e7875f65acf4fc691b2d7b111b18a83664e8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377260"
---
# <a name="devpkeyname-device-instance"></a>DEVPKEY_NAME (デバイス インスタンス)


DEVPKEY_NAME デバイス プロパティは、デバイスのインスタンスの名前を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_NAME</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>〇</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

DEVPKEY_NAME デバイスの値は、ユーザー インターフェイスの項目で、エンドユーザーにデバイスのインスタンスを識別するために使用する必要があります。

取得したプロパティ値は、の値として同じ、 [ **DEVPKEY_Device_FriendlyName** ](devpkey-device-friendlyname.md)デバイス プロパティ場合、 **DEVPKEY_Device_FriendlyName**設定されます。 それ以外の場合、DEVPKEY_NAME の値が同じの値として、 [ **DEVPKEY_Device_DeviceDesc** ](devpkey-device-devicedesc.md)デバイス プロパティ。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) DEVPKEY_NAME プロパティの値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、対応する名前プロパティを直接サポートされません。 ただし、以前のバージョンの Windows では、DEVPKEY_Device_FriendlyName および DEVPKEY_Device_DeviceDesc に対応するプロパティをサポートしています。

<a name="requirements"></a>必要条件
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


[**DEVPKEY_Device_DeviceDesc**](devpkey-device-devicedesc.md)

[**DEVPKEY_Device_FriendlyName**](devpkey-device-friendlyname.md)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






