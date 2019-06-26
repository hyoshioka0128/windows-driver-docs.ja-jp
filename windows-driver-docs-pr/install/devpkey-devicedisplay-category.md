---
title: DEVPKEY_DeviceDisplay_Category
description: DEVPKEY_DeviceDisplay_Category
ms.assetid: 4f1999cd-e3b7-4755-ab48-1feabbc9d245
keywords:
- DEVPKEY_DeviceDisplay_Category デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceDisplay_Category
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d77e358b158540f392fdf811dc9ac7471ccf8954
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378042"
---
# <a name="devpkeydevicedisplaycategory"></a>DEVPKEY_DeviceDisplay_Category


DEVPKEY_DeviceDisplay_Category デバイス プロパティは、デバイスのインスタンスに適用される 1 つまたは複数の機能カテゴリを表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceDisplay_Category</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって読み取り専用アクセス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

物理デバイスのデバイス カテゴリを使用して指定、 [ **DeviceCategory** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541101(v=vs.85))内の XML 要素を[デバイス メタデータ パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)します。 システムでは、そのデバイスの各インスタンスは、その物理デバイスのデバイス カテゴリを継承します。

各物理デバイスには 1 つまたはより機能的なカテゴリがで指定された、[デバイス メタデータ パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)します。 各カテゴリは、認識されているデバイスのカテゴリのいずれかにデバイスのインスタンスをグループ化する Windows デバイスとプリンターによって使用されます。

多機能デバイスは通常デバイスをサポートするハードウェア関数ごとに複数の機能カテゴリを特定します。 たとえば、多機能デバイスには、プリンター、fax、スキャナー、およびリムーバブル記憶域デバイスの機能の機能のカテゴリを識別できます。

最初の機能のカテゴリの文字列で、 [ **DEVPROP_TYPE_STRING_LIST** ](devprop-type-string-list.md)物理デバイスの主な機能のカテゴリを指定します。 主な機能のカテゴリは、独立系ハードウェア ベンダー (IHV) デバイスを提供する方法を指定して定義されている、パッケージ化、販売、および最終的にユーザーによって識別されるは。

DEVPKEY_DeviceDisplay_Category デバイスのプロパティは、1 つ以上の機能のカテゴリ文字列を指定する場合、最初の文字列に続くの残りの文字列はセカンダリ機能の物理デバイスのカテゴリを指定します。

**デバイスとプリンター**コントロール パネルの ユーザー インターフェイスには、デバイスのインスタンスのプライマリとセカンダリ機能カテゴリが表示されます。 DEVPKEY_DeviceDisplay_Category デバイス プロパティで指定されている順序では、これらのカテゴリが表示されます。

DEVPKEY_DeviceDisplay_Category プロパティを呼び出すことによってアクセスできる[ **SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)します。

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
<td align="left"><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h (Devpkey.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DeviceCategory**](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541101(v=vs.85))

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






