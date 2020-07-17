---
title: DEVPKEY_DeviceClass_Exclusive
description: DEVPKEY_DeviceClass_Exclusive
ms.assetid: a05ada91-6a6f-4253-aca5-0740294a5c24
keywords:
- デバイスとドライバーのインストールの DEVPKEY_DeviceClass_Exclusive
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_Exclusive
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 64e28615bc6008a20130f1f28d9e8399e9df0fdb
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418541"
---
# <a name="devpkey_deviceclass_exclusive"></a>DEVPKEY_DeviceClass_Exclusive


DEVPKEY_DeviceClass_Exclusive デバイスプロパティは、[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)のメンバーであるデバイスが専用デバイスかどうかを示すブールフラグを表します。

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
<td align="left"><p>DEVPKEY_DeviceClass_Exclusive</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>デバイスセットアップクラスがインストールされた後のインストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPCRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPCRP_EXCLUSIVE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

インストールアプリケーションがデバイスセットアップクラスをインストールするときに DEVPKEY_DeviceClass_Exclusive の値を設定できます。 デバイスセットアップクラスをインストールし、このプロパティを設定する方法の詳細については、「 [**Inf ClassInstall32」セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)と、「 [**inf AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)」の「特別な*値-エントリ名*キーワード」に記載さ**れているレジストリ値に**関する情報を参照してください。

[**Setupdigetclassproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)または[**Setupdigetclasspropertyex**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)を呼び出して、DEVPKEY_DeviceClass_Exclusive の値を取得できます。

Windows Server 2003 および Windows XP では、このプロパティはサポートされていますが、DEVPKEY_DeviceClass_Exclusive のプロパティキーはサポートされていません。 以前のバージョンの Windows では、SPCRP_EXCLUSIVE 識別子を使用して、このプロパティの値にアクセスできます。 このプロパティの値にアクセスする方法の詳細については、「[デバイスのセットアップクラス SPCRP_Xxx のプロパティの取得](https://docs.microsoft.com/windows-hardware/drivers/install/retrieving-spcrp-xxx-properties)」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)

[**INF ClassInstall32 セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)

[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

 

 






