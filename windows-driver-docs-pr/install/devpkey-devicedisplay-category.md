---
title: DEVPKEY_DeviceDisplay_Category
description: DEVPKEY_DeviceDisplay_Category
ms.assetid: 4f1999cd-e3b7-4755-ab48-1feabbc9d245
keywords:
- デバイスとドライバーのインストールの DEVPKEY_DeviceDisplay_Category
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
ms.openlocfilehash: bfd0af0d8bcc3b1ad202e04a8291f2ff75e1ec28
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418242"
---
# <a name="devpkey_devicedisplay_category"></a>DEVPKEY_DeviceDisplay_Category


DEVPKEY_DeviceDisplay_Category デバイスプロパティは、デバイスインスタンスに適用される1つ以上の機能カテゴリを表します。

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
<td align="left"><p>DEVPKEY_DeviceDisplay_Category</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティ-データ型識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>「プロパティ アクセス」</strong></p></td>
<td align="left"><p>インストールアプリケーションおよびインストーラーによる読み取り専用アクセス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>た?</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

物理デバイスのデバイスカテゴリは、[デバイスメタデータパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)の[**device.devicecategory**](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541101(v=vs.85)) XML 要素によって指定されます。 システム内のデバイスの各インスタンスは、その物理デバイスのデバイスカテゴリを継承します。

各物理デバイスは、[デバイスメタデータパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)に指定された1つまたは複数の機能カテゴリを持つことができます。 各カテゴリは、デバイスインスタンスを、認識されているデバイスカテゴリの1つにグループ化するために、Windows のデバイスとプリンターによって使用されます。

多機能なデバイスは、通常、デバイスがサポートするハードウェア機能ごとに複数の機能カテゴリを識別します。 たとえば、多機能なデバイスは、プリンター、fax、スキャナー、リムーバブル記憶装置の機能の機能カテゴリを識別できます。

[**DEVPROP_TYPE_STRING_LIST**](devprop-type-string-list.md)の最初の機能カテゴリ文字列は、物理デバイスのプライマリ機能カテゴリを指定します。 プライマリ機能カテゴリは、独立系ハードウェアベンダー (IHV) によって定義され、デバイスのアドバタイズ、パッケージ化、販売、および最終的にユーザーによって識別される方法を指定します。

DEVPKEY_DeviceDisplay_Category デバイスプロパティに複数の機能カテゴリ文字列が指定されている場合、最初の文字列に続く残りの文字列では、物理デバイスのセカンダリ機能カテゴリが指定されます。

コントロールパネルの [**デバイスとプリンター** ] のユーザーインターフェイスには、デバイスインスタンスのプライマリおよびセカンダリの機能カテゴリが表示されます。 これらのカテゴリは、DEVPKEY_DeviceDisplay_Category デバイスプロパティで指定されている順序で表示されます。

[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を呼び出すことによって、DEVPKEY_DeviceDisplay_Category プロパティにアクセスできます。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Devpkey (Devpkey を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**Device.devicecategory**](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541101(v=vs.85))

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






