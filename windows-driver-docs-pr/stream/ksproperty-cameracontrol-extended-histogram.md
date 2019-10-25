---
title: KSK プロパティ\_CAMERACONTROL\_拡張\_ヒストグラム
description: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_ヒストグラムは、ドライバーによって生成されるヒストグラムメタデータを制御するために使用されるプロパティ ID です。 これは、プレビューの pin のピンレベルコントロールです。
ms.assetid: 638AA1AA-F8E5-4FD7-9283-CF1F23266474
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_HISTOGRAM ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_HISTOGRAM
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 678986809f5efc2152997fa74f602f98a80af3ef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841598"
---
# <a name="ksproperty_cameracontrol_extended_histogram"></a>KSK プロパティ\_CAMERACONTROL\_拡張\_ヒストグラム


**Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_ヒストグラム**は、ドライバーによって生成されるヒストグラムメタデータを制御するために使用されるプロパティ ID です。 これは、プレビューの pin のピンレベルコントロールです。

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

 

次のフラグは、 **KSCAMERA\_EXTENDEDPROP\_ヘッダーに配置できます。[フラグ**] フィールドを指定して、ドライバーのヒストグラムメタデータを制御します。 既定値は **ヒストグラム\_オフ**です。

```cpp
#define KSCAMERA_EXTENDEDPROP_HISTOGRAM_OFF      0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_HISTOGRAM_ON       0x0000000000000001
```

このコントロールは、 [**Ksk プロパティ\_CAMERACONTROL\_拡張\_メタデータ**](ksproperty-cameracontrol-extended-metadata.md)コントロールの前に使用して、適切なサイズのメタデータバッファーが割り当てられるようにする必要があります。

[**ヒストグラム\_オフ**] に設定した場合、ドライバーは、プレビューピンのヒストグラムメタデータを配信しません。 ドライバーでは、メタデータバッファーサイズの要件にヒストグラムメタデータのサイズを含めないでください。

**ヒストグラム\_** に設定すると、ドライバーはプレビューピンにヒストグラムメタデータを配信します。 ドライバーでは、メタデータバッファーサイズの要件にヒストグラムメタデータのサイズが含まれている必要があります。

ドライバーがヒストグラムメタデータを生成する機能を備えていない場合、ドライバーはこのコントロールを実装しません。 ドライバーがこのコントロールをサポートしている場合は、 [**CAMERACONTROL\_拡張\_メタデータコントロールである Ksk プロパティ\_** ](ksproperty-cameracontrol-extended-metadata.md)もサポートする必要があります。

このコントロールの**SET**呼び出しは、プレビューピンが ksk 状態\_停止状態よりも大きい状態にある場合は効果がありません。 Preview が停止状態でない場合は、ドライバーは**SET**呼び出しを拒否し、**デバイス\_状態\_無効\_状態**を返します。 **GET**呼び出しでは、ドライバーは**Flags**フィールドの現在の設定を返します。

次の表に、コントロールを使用する場合の[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造体のフィールドの説明と要件を示します。

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
<td><p>は、プレビュー pin に関連付けられている Pin ID である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>これは sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + Sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>最後の<strong>設定</strong>操作のエラー結果を示します。 <strong>設定</strong>操作が行われていない場合は、0にする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>0にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 これには、上記で定義されている<strong>KSCAMERA_EXTENDEDPROP_HISTOGRAM_ *</strong>フラグのいずれかを指定できます。</p></td>
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
