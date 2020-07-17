---
title: DEVPKEY_DeviceClass_Security
description: DEVPKEY_DeviceClass_Security
ms.assetid: e23fd11b-07ee-4375-841d-1fa9c42d5a28
keywords:
- デバイスとドライバーのインストールの DEVPKEY_DeviceClass_Security
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_Security
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f2218fa5cb800499582277696d00ce3cabce8484
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418382"
---
# <a name="devpkey_deviceclass_security"></a>DEVPKEY_DeviceClass_Security


DEVPKEY_DeviceClass_Security デバイスプロパティは、[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)のセキュリティ記述子構造体を表します。

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
<td align="left"><p>DEVPKEY_DeviceClass_Security</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-security-descriptor.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_SECURITY_DESCRIPTOR&lt;/strong&gt;](devprop-type-security-descriptor.md)"><strong>DEVPROP_TYPE_SECURITY_DESCRIPTOR</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>インストールアプリケーションとインストーラーによる読み取りおよび書き込みアクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPCRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPCRP_SECURITY</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

DEVPKEY_DeviceClass_Security の値は、インストールアプリケーションによってデバイスセットアップクラスがインストールされるか、インストール後に設定できます。 このプロパティを設定する方法の詳細については、「[セキュリティで保護されたデバイスのインストールの作成](https://docs.microsoft.com/windows-hardware/drivers/install/creating-secure-device-installations)」を参照してください。

DEVPKEY_DeviceClass_Security の値を取得するには、 [**Setupdigetclassproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)または[**Setupdigetclasspropertyex**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)を呼び出します。 [**Setupdisetclassproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw)または[**Setupdisetclasspropertyex**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyexw)を呼び出すことによって、DEVPKEY_DeviceClass_Security を設定できます。

Windows Server 2003 および Windows XP では、このプロパティはサポートされていますが、DEVPKEY_DeviceClass_Security のプロパティキーはサポートされていません。 以前のバージョンの Windows では、SPCRP_SECURITY 識別子を使用して、このプロパティの値にアクセスできます。 このプロパティの値にアクセスする方法の詳細については、「[デバイスセットアップクラスの取得 SPCRP_Xxx プロパティ](https://docs.microsoft.com/windows-hardware/drivers/install/retrieving-spcrp-xxx-properties)」および「[デバイスセットアップクラス SPCRP_Xxx プロパティの設定](https://docs.microsoft.com/windows-hardware/drivers/install/setting-spcrp-xxx-properties)」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

[**SetupDiSetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw)

[**SetupDiSetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyexw)

 

 






