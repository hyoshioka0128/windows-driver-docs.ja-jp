---
title: DEVPKEY_DeviceClass_PropPageProvider
description: DEVPKEY_DeviceClass_PropPageProvider
ms.assetid: 467a050e-9dd4-4b3b-a942-ee29667ac264
keywords:
- デバイスとドライバーのインストールの DEVPKEY_DeviceClass_PropPageProvider
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_PropPageProvider
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bd640ad19a5d84237cdcfcd57b748e041ad383d7
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418387"
---
# <a name="devpkey_deviceclass_proppageprovider"></a>DEVPKEY_DeviceClass_PropPageProvider


DEVPKEY_DeviceClass_PropPageProvider デバイスプロパティは、[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)のプロパティページプロバイダーを表します。

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
<td align="left"><p>DEVPKEY_DeviceClass_PropPageProvider</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>データ形式</strong></p></td>
<td align="left"><p>"<em>prop-provider</em>,<em>provider-entry</em>"</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>対応するレジストリ値の名前</strong></p></td>
<td align="left"><p><strong>EnumPropPages32</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

DEVPKEY_DeviceClass_PropPageProvider の値は、クラスレジストリキーの下にある**EnumPropPages32**レジストリ値の値です。 この値には、クラスプロパティページプロバイダー DLL の名前と、デバイスセットアップクラスのプロバイダーのエントリポイントが含まれます。

デバイスセットアップクラスの**EnumPropPages32**レジストリ値は、クラスをインストールする inf ファイルの[**inf ClassInstall32 セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)に含まれている[**inf AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)によって設定できます。

[**Setupdigetclassproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)または[**Setupdigetclasspropertyex**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)を呼び出して、DEVPKEY_DeviceClass_PropPageProvider の値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートしていますが、DEVPKEY_DeviceClass_PropPageProvider プロパティキーをサポートしていません。 このプロパティの値にアクセスするには、クラスレジストリキーの下にある対応する**EnumPropPages32**レジストリ値にアクセスします。 クラスレジストリキーの値エントリにアクセスする方法の詳細については、「[クラスレジストリキー」の「レジストリエントリ値](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-registry-entry-values-under-the-class-registry-key)へのアクセス」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)

[**INF ClassInstall32 セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)

[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

 

 






