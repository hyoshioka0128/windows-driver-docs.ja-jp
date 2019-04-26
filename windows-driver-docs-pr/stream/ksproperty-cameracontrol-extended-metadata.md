---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_メタデータ
description: この拡張プロパティのコントロールは、メタデータのバッファーの要件のドライバーを照会するクライアントによって使用されます。
ms.assetid: 6196DFF6-050A-4916-A188-70A89B60B5EA
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_METADATA ストリーミング メディア デバイス
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
ms.openlocfilehash: 7d60f1b9a3652ddbc5bd211f3d0ece9e7a03ed1f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356707"
---
# <a name="kspropertycameracontrolextendedmetadata"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_メタデータ

この拡張プロパティのコントロールは、メタデータのバッファーの要件のドライバーを照会するクライアントによって使用されます。 標準と共にドライバーに送信される[ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造が続く、 [ **KSCAMERA\_EXTENDEDPROP\_METADATAINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo)構造体。

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
<td><p>Pin</p></td>
<td><p>同期</p></td>
</tr>
</tbody>
</table>

配置できるメタデータ フラグを次に、 **KSCAMERA\_EXTENDEDPROP\_ヘッダー。フラグ**フィールド。

```cpp
#define KSCAMERA_EXTENDEDPROP_METADATA_SYSTEMMEMORY                     0x0000000000000001  
#define KSCAMERA_EXTENDEDPROP_METADATA_ALIGNMENTREQUIRED                0x0000000000000100
```

**取得**呼び出し、ドライバーは次の処理します。

1.  入力**KSCAMERA\_EXTENDEDPROP\_ヘッダー。機能**0。

2.  入力 KSCAMERA\_EXTENDEDPROP\_ヘッダー。上記の KSCAMERA のいずれかの組み合わせを使用したフラグ\_EXTENDEDPROP\_メタデータ\_*XXX*メタデータのメモリ要件を示すフラグ。

3.  入力 KSCAMERA\_EXTENDEDPROP\_METADATAINFO します。目的のメモリ アラインメント BufferAlignment (KSCAMERA\_EXTENDEDPROP\_MetadataAlignment\_*Xxx*)。 参照してください、 [ **KSCAMERA\_EXTENDEDPROP\_MetadataAlignment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-kscamera_extendedprop_metadataalignment)使用可能な値。

4.  入力**KSCAMERA\_EXTENDEDPROP\_METADATAINFO します。MaxMetadataBufferSize**必要なメタデータのバッファー サイズ (バイト単位)。

次の表には、説明と要件が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)メタデータ コントロールを使用する場合は、フィールドを構造体します。

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
<td><p>これは、1 でなければなりません。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>フレームには、メタデータが含まれている pin に関連付けられた暗証番号 (pin) の ID があります。 プレビュー、レコード、およびイメージの暗証番号 (pin) のいずれかを指定できます。</p></td>
</tr>
<tr class="odd">
<td><p>サイズ</p></td>
<td><p>Sizeof 必要があります (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_METADATAINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo)"><strong>KSCAMERA_EXTENDEDPROP_METADATAINFO</strong></a>)、</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>これは、最後の設定操作のエラーの結果を示します。 設定操作が行われていない場合は必ず 0。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>これにより、使用されておらず、0 にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 任意の組み合わせをられます<strong>KSCAMERA_EXTENDEDPROP_METADATA_ALIGNMENTREQUIRED</strong>または KSCAMERA_EXTENDEDPROP_METADATA_SYSTEMMEMORY します。</p></td>
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
