---
title: DEVPKEY_Device_Legacy
description: DEVPKEY_Device_Legacy
ms.assetid: a2af9881-3aa3-45a7-9b80-cb507460957e
keywords:
- DEVPKEY_Device_Legacy デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_Legacy
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cfd560ba0fc661fa803fc40119776b9bf2692e23
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378202"
---
# <a name="devpkeydevicelegacy"></a>DEVPKEY_Device_Legacy


DEVPKEY_Device_Legacy デバイス プロパティは、デバイスがデバイスの非 PnP ドライバーが読み込まれるときに、プラグ アンド プレイ (PnP) マネージャーが自動的に作成されるルート列挙のデバイスであるかどうかを示すブール値を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_Legacy</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

PnP マネージャーでは、PnP マネージャーがデバイスの非 PnP ドライバーが読み込まれるときに、ルート列挙デバイスとして、デバイスが自動作成された場合に、DEVPROP_TRUE に DEVPKEY_Device_Reported の値を設定します。 それ以外の場合、PnP マネージャーでは、DEVPROP_FALSE にプロパティの値を設定します。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) DEVPKEY_Device_Legacy の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 では、このプロパティはサポートされません。

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


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






