---
title: DEVPKEY_DeviceClass_Icon
description: DEVPKEY_DeviceClass_Icon
ms.assetid: 036b6daf-b5de-4aa0-b7e3-ba0430107938
keywords:
- デバイスとドライバーのインストールの DEVPKEY_DeviceClass_Icon
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_Icon
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 89dba30cbe839f002d29830f1c397dba6ddb7b3d
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418543"
---
# <a name="devpkey_deviceclass_icon"></a>DEVPKEY_DeviceClass_Icon


DEVPKEY_DeviceClass_Icon デバイスプロパティは、[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)のアイコンを表します。

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
<td align="left"><p>DEVPKEY_DeviceClass_Icon</p></td>
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

DEVPKEY_DeviceClass_Icon の値は、クラスをインストールする[**Inf ClassInstall32 セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)に含まれている[**inf AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)によって設定されます。 DEVPKEY_DeviceClass_Icon の値を設定するには、 **AddReg**ディレクティブを使用して、クラスの**Icon**レジストリエントリの値を設定します。

**アイコン**エントリの値は、文字列形式の整数値です。 数値が負の値の場合、数値の絶対値は setupapi.dll 内のアイコンのリソース識別子になります。 数値が正の値の場合は、クラスインストーラー DLL 内のアイコンのリソース識別子 (クラスインストーラーがある場合)、またはクラスのプロパティページプロバイダー (クラスインストーラーがなく、プロパティページプロバイダーがある場合) が表示されます。 0の値は無効です。

[**Setupdigetclassproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)または[**Setupdigetclasspropertyex**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)を呼び出して、DEVPKEY_DeviceClass_Icon の値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートしていますが、DEVPKEY_DeviceClass_Icon プロパティキーをサポートしていません。 Windows Server 2003、Windows XP、および Windows 2000 でデバイスセットアップクラスのミニアイコンにアクセスする方法の詳細については、「[デバイスセットアップクラスのアイコンプロパティへの](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-icon-properties-of-a-device-setup-class)アクセス」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)

[**INF ClassInstall32 セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)

[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

[**SetupDiDrawMiniIcon**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidrawminiicon)

[**SetupDiLoadClassIcon**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiloadclassicon)

 

 






