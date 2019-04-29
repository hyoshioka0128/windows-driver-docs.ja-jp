---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOCONFIRMATION
description: KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOCONFIRMATION プロパティ ID、KSPROPERTY で定義されている\_CAMERACONTROL\_拡張\_プロパティの列挙を使用する設定し、ドライバーで、写真の確認の設定を取得します。
ms.assetid: 3EF6FF15-6805-4D91-B053-1BF6C5D5BEF2
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOCONFIRMATION ストリーミング メディア デバイス
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
ms.openlocfilehash: 0c3f94e81fc2036cca1b359d211764f33b9f8f2f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327135"
---
# <a name="kspropertycameracontrolextendedphotoconfirmation"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOCONFIRMATION

**KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOCONFIRMATION**で定義されているプロパティ ID、 [ **KSPROPERTY\_CAMERACONTROL\_拡張\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/dn917962)列挙型が使用して設定し、ドライバーで、写真の確認の設定を取得します。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Scope</th>
<th>コントロール</th>
<th>種類</th>
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

[ **KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)、次のフラグ値を使用して、写真の確認を有効または無効にします。 既定では、ドライバーが必要**KSPROPERTY\_PHOTOCONFIRMATION\_ON**を設定します。 フラグの値の定義は次のとおりです。

```cpp
#define KSCAMERA_EXTENDEDPROP_PHOTOCONFIRMATION_OFF     0x0000000000000000 
#define KSCAMERA_EXTENDEDPROP_PHOTOCONFIRMATION_ON      0x0000000000000001
```

写真の確認に設定されている場合**KSCAMERA\_EXTENDEDPROP\_PHOTOCONFIRMATION\_OFF**、ドライバーのプレビュー暗証番号 (pin) のフォト フレームを生成または生成する必要がありますいない、 [ **KSCAMERA\_メタデータ\_PHOTOCONFIRMATION** ](https://msdn.microsoft.com/library/windows/hardware/dn925187)確認の写真のメタデータを含む構造体。 写真の確認に設定されている場合**KSCAMERA\_EXTENDEDPROP\_PHOTOCONFIRMATION\_ON**、ドライバーのプレビューのピン留めする必要がありますフォト フレームを生成および生成、 **KSCAMERA\_メタデータ\_PHOTOCONFIRMATION**確認の写真のメタデータを含む構造体。

次の表には、説明と要件が含まれています、 **KSCAMERA\_EXTENDEDPROP\_ヘッダー**フィールドを構造体を使用する場合、 **KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOCONFIRMATION**プロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Member</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>これは、1、</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>これでなければなりません<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0 xffffffff)</p></td>
</tr>
<tr class="odd">
<td><p>サイズ</p></td>
<td><p>Sizeof 必要があります (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>)。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>これには、最後の設定操作のエラーの結果が含まれています。 設定操作が行われていない場合は必ず 0。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>これは、0 でなければなりません。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 いずれかになります、 <strong>KSCAMERA_EXTENDEDPROP_PHOTOCONFIRMATION_Xxx</strong>上記で定義されたフラグ。</p></td>
</tr>
</tbody>
</table>

## <a name="requirements"></a>必要条件

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
