---
title: DEVPKEY_DeviceClass_LowerFilters
description: DEVPKEY_DeviceClass_LowerFilters
ms.assetid: 39bc784e-a8be-4921-9a12-f423fe502019
keywords:
- デバイスとドライバーのインストールの DEVPKEY_DeviceClass_LowerFilters
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_LowerFilters
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 73d17071508f61fc9b19b565c54ae80e1b31baaf
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418534"
---
# <a name="devpkey_deviceclass_lowerfilters"></a>DEVPKEY_DeviceClass_LowerFilters


DEVPKEY_DeviceClass_LowerFilters デバイスプロパティは、[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)用にインストールされている下位レベルのフィルタードライバーのサービス名の一覧を表します。

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
<td align="left"><p>DEVPKEY_DeviceClass_LowerFilters</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>データ形式</strong></p></td>
<td align="left"><p>"<em>service-name1</em>\ 0<em>サービス-name2</em>\ 0...<em>サービス-nameN</em>\ 0 \ 0 "</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>クラスフィルターがインストールされた後のインストールアプリケーションおよびインストーラーによる読み取り専用アクセス</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>対応する SPCRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPCRP_LOWERFILTERS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応するレジストリ値の名前</strong></p></td>
<td align="left"><p><strong>LowerFilters</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

DEVPKEY_DeviceClass_LowerFilters の値は、クラスフィルタードライバーがインストールされているときに設定されます。 クラスフィルタードライバーをインストールする方法の詳細については、「[フィルタードライバー](https://docs.microsoft.com/windows-hardware/drivers/install/installing-a-filter-driver)と[**INF ClassInstall32 のインストール」セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)を参照してください。

[**Setupdigetclassproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)または[**Setupdigetclasspropertyex**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)を呼び出して、DEVPKEY_DeviceClass_LowerFilters の値を取得できます。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートしていますが、DEVPKEY_DeviceClass_LowerFilters プロパティキーをサポートしていません。 以前のバージョンの Windows では、クラスレジストリキーの下にある対応する**LowerFilters**レジストリ値にアクセスすることによって、このプロパティの値にアクセスできます。 これらの以前のバージョンの Windows でこのプロパティ値にアクセスする方法の詳細については、「[クラスレジストリキー」の「レジストリエントリ値](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-registry-entry-values-under-the-class-registry-key)へのアクセス」を参照してください。

<a name="requirements"></a>必要条件
------------

**バージョン**: windows Vista 以降のバージョンの windows**ヘッダー**: Devpkey (Devpkey を含む)


## <a name="see-also"></a>関連項目


[**INF ClassInstall32 セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)

[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

[**SetupDiOpenClassRegKeyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)

 

 






