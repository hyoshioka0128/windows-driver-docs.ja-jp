---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_PHOTOCONFIRMATION
description: Ksk プロパティ\_CAMERACONTROL\_拡張\_PHOTOCONFIRMATION プロパティ ID で定義されている\_CAMERACONTROL\_拡張\_プロパティ列挙を使用して、写真の確認を設定して取得します。ドライバーの設定。
ms.assetid: 3EF6FF15-6805-4D91-B053-1BF6C5D5BEF2
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOCONFIRMATION ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOCONFIRMATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 11c84800d68f581c430166ecfa16be2f5b67ce82
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844773"
---
# <a name="ksproperty_cameracontrol_extended_photoconfirmation"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_PHOTOCONFIRMATION

Ksk プロパティ **\_CAMERACONTROL\_拡張\_PHOTOCONFIRMATION**プロパティ ID\_で定義されています。拡張[ **\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)の列挙を使用して、の設定と取得を行います。ドライバーの写真確認設定。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>適用範囲</th>
<th>コントロール</th>
<th>タスクバーの検索ボックスに</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バージョン 1</p></td>
<td><p>フィルター</p></td>
<td><p>同期</p></td>
</tr>
</tbody>
</table>

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)では、次のフラグ値を使用して、写真の確認をオンまたはオフにします。 既定では、ドライバーは、設定された**photoconfirmation photoconfirmation に Ksk プロパティ**を持つ必要があります。 フラグの値は、次のように定義されます。

```cpp
#define KSCAMERA_EXTENDEDPROP_PHOTOCONFIRMATION_OFF     0x0000000000000000 
#define KSCAMERA_EXTENDEDPROP_PHOTOCONFIRMATION_ON      0x0000000000000001
```

フォト確認が KSCAMERA に設定されている場合 **\_EXTENDEDPROP\_photoconfirmation\_オフ**になっている場合、ドライバーのプレビュー pin はフォトフレームを生成したり、 [**KSCAMERA\_メタデータ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_photoconfirmation)を生成したりすることはできません\_photoconfirmationフォト確認メタデータを格納する構造体。 フォト確認が**KSCAMERA\_EXTENDEDPROP\_photoconfirmation\_** に設定されている場合、driver preview pin はフォトフレームを生成し、 **KSCAMERA\_メタ\_データ**を生成する必要があります。 photoconfirmationフォト確認メタデータを格納する構造体。

次の表には、 **Ksk プロパティ\_CAMERACONTROL\_拡張\_PHOTOCONFIRMATION**を使用する場合の**KSCAMERA\_EXTENDEDPROP\_ヘッダー**構造のフィールドの説明と要件が含まれています。".

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メンバー</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>これは1である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>これは<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0xffffffff) である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>これは sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + Sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>これには、最後の設定操作のエラー結果が含まれます。 設定操作が行われていない場合は、0にする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>0にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 これは、上記で定義されている<strong>KSCAMERA_EXTENDEDPROP_PHOTOCONFIRMATION_Xxx</strong>フラグのいずれかになります。</p></td>
</tr>
</tbody>
</table>

## <a name="requirements"></a>要件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
