---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FOCUSPRIORITY
description: Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_FOCUSPRIORITY プロパティ ID で定義されている\_CAMERACONTROL\_拡張\_プロパティ列挙を使用して、フォーカスの優先度を構成します。
ms.assetid: 7E3558A1-0D0D-4470-B9C9-61EA359E92C5
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSPRIORITY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSPRIORITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 07718af15399fa6c3a1e0950236467a811dd4ef9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841602"
---
# <a name="ksproperty_cameracontrol_extended_focuspriority"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FOCUSPRIORITY


Ksk プロパティ **\_CAMERACONTROL\_extended\_FOCUSPRIORITY**プロパティ ID で定義されている[ **\_CAMERACONTROL\_拡張\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)列挙を使用して、フォーカスの優先度を構成します。 フォーカスの優先度を設定すると、撮影した画像が常にフォーカスされていることを確認するために、撮影した画像よりもフォーカスが優先されます。 そうしないと、画像がフォーカスされているかどうかにかかわらず、画像は直ちに取得されます。 失敗したフォーカスを処理するときの動作と、タイムアウトが必要かどうかは、ドライバーの内部と OEM までの間にあります。

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

 

フォーカスの優先順位を構成するには、 **CAMERACONTROL\_拡張\_FOCUSPRIORITY**プロパティ ID の ksk プロパティを使用する必要があり\_。 フォーカスの優先度が設定されている場合、撮影した画像が常にフォーカスされていることを確認するために、フォーカスは画像よりも優先されます。 フォーカスの優先度が設定されていない場合、画像がフォーカスされているかどうかに関係なく、すぐに画像が取得されます。 失敗したフォーカスの処理の動作は失敗し、タイムアウトは OEM によって決定され、ドライバーの内部にあります。

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)では、次のフラグが値として定義されます。 Get 呼び出しでは、カメラドライバーは、これらのフラグのいずれかを使用して、現在の優先順位の構成を返します。 セット呼び出しでは、カメラドライバーは、これらのフラグのいずれかを使用して、新しい優先順位の構成を設定します。

```cpp
#define KSCAMERA_EXTENDEDPROP_FOCUSPRIORITY_OFF     0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_FOCUSPRIORITY_ON      0x0000000000000001
```

これは同期コントロールであり、このコントロールには機能が定義されていない   に**注意**してください。

 

次の表には、フォーカス優先度コントロールを使用する場合の**KSCAMERA\_EXTENDEDPROP\_ヘッダー**構造のフィールドの説明と要件が含まれています。

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
<td><p>これは KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF) である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>これは sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + Sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>これは、エラーの結果を示します。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>0にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 これには、上記で定義されている KSCAMERA_EXTENDEDPROP_FOCUSPRIORITY_Xxx フラグのいずれかを指定できます。</p></td>
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
