---
title: DEVPKEY_DeviceClass_ClassName
description: DEVPKEY_DeviceClass_ClassName
ms.assetid: dc085e27-06c7-49ca-808f-3d1952cb8aa9
keywords:
- デバイスとドライバーのインストールの DEVPKEY_DeviceClass_ClassName
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_ClassName
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5ca098e1695c7efc6bc0928b29665049b32aefb9
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418315"
---
# <a name="devpkey_deviceclass_classname"></a>DEVPKEY_DeviceClass_ClassName


DEVPKEY_DeviceClass_ClassName デバイスプロパティは、[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)のクラス名を表します。

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
<td align="left"><p>DEVPKEY_DeviceClass_ClassName</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

DEVPKEY_DeviceClass_ClassName の値は、device setup クラスをインストールする[**INF バージョンセクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)に含まれている**class**ディレクティブによって設定されます。

[**Setupdigetclassproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)または[**Setupdigetclasspropertyex**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)を呼び出して、DEVPKEY_DeviceClass_ClassName の値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートしていますが、DEVPKEY_DeviceClass_ClassName プロパティキーをサポートしていません。 Windows Server 2003、Windows XP、および Windows 2000 でデバイスセットアップクラスの名前にアクセスする方法の詳細については、「[デバイスセットアップクラスのフレンドリ名とクラス名](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-the-friendly-name-and-class-name-of-a-device-setup-class)へのアクセス」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**INF Version セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)

[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

[**SetupDiClassNameFromGuid**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiclassnamefromguida)

 

 






