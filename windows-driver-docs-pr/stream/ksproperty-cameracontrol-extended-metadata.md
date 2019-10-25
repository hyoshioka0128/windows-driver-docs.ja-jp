---
title: KSK プロパティ\_CAMERACONTROL\_拡張\_メタデータ
description: この拡張プロパティコントロールは、メタデータバッファー要件をドライバーに照会するためにクライアントによって使用されます。
ms.assetid: 6196DFF6-050A-4916-A188-70A89B60B5EA
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_METADATA ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_METADATA
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 79ffe0217b76c22106a16b61cd66a76c24d767f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841592"
---
# <a name="ksproperty_cameracontrol_extended_metadata"></a>KSK プロパティ\_CAMERACONTROL\_拡張\_メタデータ

この拡張プロパティコントロールは、メタデータバッファー要件をドライバーに照会するためにクライアントによって使用されます。 これは、標準の[**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と共にドライバーに送信され、その後に[**KSCAMERA\_EXTENDEDPROP\_METADATAINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo)構造体が続きます。

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
<td><p>Pin</p></td>
<td><p>同期</p></td>
</tr>
</tbody>
</table>

次に示すのは、 **KSCAMERA\_EXTENDEDPROP\_ヘッダーに配置できるメタデータフラグです。Flags**フィールド。

```cpp
#define KSCAMERA_EXTENDEDPROP_METADATA_SYSTEMMEMORY                     0x0000000000000001  
#define KSCAMERA_EXTENDEDPROP_METADATA_ALIGNMENTREQUIRED                0x0000000000000100
```

**Get**呼び出しでは、ドライバーは次のことを行います。

1.  **KSCAMERA\_EXTENDEDPROP\_ヘッダーに塗りつぶします。** 0 の機能。

2.  Fill KSCAMERA\_EXTENDEDPROP\_ヘッダーを入力します。上のいずれかの KSCAMERA\_EXTENDEDPROP\_METADATA\_*XXX*フラグを組み合わせたフラグを使用して、メタデータのメモリ要件を示します。

3.  Fill KSCAMERA\_EXTENDEDPROP\_METADATAINFO です。必要なメモリアラインメントによる BufferAlignment (KSCAMERA\_EXTENDEDPROP\_MetadataAlignment\_*Xxx*)。 使用可能な値については、 [**KSCAMERA\_EXTENDEDPROP\_MetadataAlignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-kscamera_extendedprop_metadataalignment)を参照してください。

4.  Fill **KSCAMERA\_EXTENDEDPROP\_METADATAINFO です。MaxMetadataBufferSize**には、必要なメタデータバッファーサイズ (バイト単位) を指定します。

次の表には、メタデータコントロールを使用する場合の[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造のフィールドの説明と要件が含まれています。

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
<td><p>これは、フレームにメタデータが含まれている pin に関連付けられた Pin ID である必要があります。 これには、プレビュー、レコード、およびイメージの pin を使用できます。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>これは sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + Sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_METADATAINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo)"><strong>KSCAMERA_EXTENDEDPROP_METADATAINFO</strong></a>) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>これは、最後の設定操作のエラー結果を示します。 設定操作が行われていない場合は、0にする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>これは使用されておらず、0である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 これは、 <strong>KSCAMERA_EXTENDEDPROP_METADATA_ALIGNMENTREQUIRED</strong>または KSCAMERA_EXTENDEDPROP_METADATA_SYSTEMMEMORY の任意の組み合わせにすることができます。</p></td>
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
