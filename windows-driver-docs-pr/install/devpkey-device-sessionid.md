---
title: DEVPKEY_Device_SessionId
description: DEVPKEY_Device_SessionId
ms.assetid: 0e5815b3-0427-4f07-9ec1-a21976d5d933
keywords:
- デバイスとドライバーのインストールの DEVPKEY_Device_SessionId
topic_type:
- apiref
api_name:
- DEVPKEY_Device_SessionId
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 25b3459514199b3c06ff0105b3ae4bcfa42812e7
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418527"
---
# <a name="devpkey_device_sessionid"></a>DEVPKEY_Device_SessionId


DEVPKEY_Device_SessionId デバイスプロパティは、デバイスインスタンスにアクセスできるターミナルサービスセッションを示す値を表します。

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
<td align="left"><p>DEVPKEY_Device_SessionId</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-uint32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_UINT32&lt;/strong&gt;](devprop-type-uint32.md)"><strong>DEVPROP_TYPE_UINT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>アプリケーションとサービスによる読み取りおよび書き込みアクセス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

ターミナルサーバー機能は、プラグアンドプレイ (PnP) デバイスリダイレクトをサポートしています。 デバイスリダイレクトは、すべてのターミナルサービスセッション内のアプリケーションとサービスがデバイスにアクセスできるかどうか、または特定のターミナルサービスセッション内でのみデバイスにアクセスできるかどうかを決定します。 ターミナルサービスセッション内のデバイスのユーザー補助は、デバイスの DEVPKEY_Device_SessionId の設定によって決定されます。次に例を示します。

-   DEVPKEY_Device_SessionId プロパティが存在しない場合、またはプロパティが存在していても、プロパティの値が設定されていない場合は、すべてのアクティブなターミナルサービスセッションでデバイスにアクセスできます。

-   DEVPKEY_Device_SessionId プロパティが存在し、プロパティの値が0以外のターミナルサービスのセッション識別子に設定されている場合、ターミナルサービスのセッション識別子で示されているターミナルサービスセッションでのみ、デバイスにアクセスできます。

-   DEVPKEY_Device_SessionId プロパティが存在し、プロパティの値が0に設定されている場合、デバイスにはサービスによってのみアクセスできます。 セッション0は、サービスのみを実行できる特殊なセッションです。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)と[**setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)を呼び出すことによって、DEVPKEY_Device_SessionId プロパティにアクセスできます。

Windows Server 2003、Windows XP、および Windows 2000 では、このプロパティはサポートされていません。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

 

 






