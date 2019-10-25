---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_OPTIMIZATIONHINT
description: カメラドライバーは、アプリケーションによって提供されるヒントに基づいて、キャプチャ操作を最適化することができます。 このプロパティは、最も頻繁に使用される操作に基づいて、パフォーマンス戦略を設定するようにドライバーに通知します。
ms.assetid: FEA3D355-B490-4E67-905D-EE5507E91150
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: afee622ffb06489a7cbc2c3580f557b91be5355a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841588"
---
# <a name="ksproperty_cameracontrol_extended_optimizationhint"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_OPTIMIZATIONHINT

カメラドライバーは、アプリケーションによって提供されるヒントに基づいて、キャプチャ操作を最適化することができます。 このプロパティは、最も頻繁に使用される操作に基づいて、パフォーマンス戦略を設定するようにドライバーに通知します。 たとえば、写真用に最適化されている場合、カメラドライバーはセンサーの露出速度と解像度を最適化するようにセンサーをプログラミングすることがあります。これにより、フォトキャプチャトリガーからイメージキャプチャまでの待ち時間が短縮されます。 同様に、ビデオ用に最適化されている場合、カメラドライバーは、フレームレートが高く、解像度が低くなるようにセンサーをプログラミングすることがあります。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

プロパティ値 (操作データ) には、 [**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と、 [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)の構造体が含まれています。

プロパティデータの合計サイズは**sizeof**(KSCAMERA\_extendedprop\_HEADER) + **sizeof**(KSCAMERA\_extendedprop\_値) です。 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**機能**メンバーには、次の最適化ヒントの1つ以上のビットごとの or の組み合わせが含まれています。

| 最適化ヒント                           | 説明                               |
|---------------------------------------------|-------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_最適化\_写真 | カメラの操作は、写真用に最適化されています。 |
| KSCAMERA\_EXTENDEDPROP\_最適化\_ビデオ | カメラ操作はビデオ用に最適化されています。  |

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーには、カメラに現在設定されている最適化 (1 つの値) が含まれています。

既定の最適化の種類は、KSCAMERA\_EXTENDEDPROP\_OPTIMIZATION\_PHOTO です。 このプロパティがカメラドライバーでサポートされている場合は、両方の最適化の種類がサポートされている必要があります。

このプロパティコントロールは同期であり、キャンセルできません。

## <a name="remarks"></a>注釈

### <a name="optimization-modes"></a>最適化モード

**KSCAMERA\_EXTENDEDPROP\_最適化\_写真**
-   KSCAMERA\_EXTENDEDPROP\_最適化\_ビデオモードを使用するように明示的に通知されるまでは、すべてのカメラドライバーがこのモードになっている必要があります。 このモードの目的は、写真操作用のカメラハードウェアを最適化することです。 このモードでは、ビデオ操作を引き続き機能させる必要があります。

**KSCAMERA\_EXTENDEDPROP\_最適化\_ビデオ**
-   このモードは、カメラがビデオ操作に使用される可能性があることを示します。 カメラドライバーは、このモードのビデオ操作のハードウェアを最適化する必要があります。 写真操作は機能している必要がありますが、リソース使用の優先度はビデオ操作用です。

### <a name="getting-the-property"></a>プロパティを取得する

\_GET 要求の種類\_KSK プロパティに応答すると、ドライバーは、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)のメンバーを次のように設定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メンバー</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>バージョン</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF)。</td>
</tr>
<tr class="odd">
<td>Size</td>
<td><p>sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>機能</td>
<td>最適化の値がサポートされています。</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>現在の最適化の値の設定。</td>
</tr>
</tbody>
</table>

最適化モードが設定されていない場合、ドライバーは KSCAMERA\_EXTENDEDPROP\_OPTIMIZATION\_PHOTO (既定値) に**フラグ**を設定します。

### <a name="setting-the-property"></a>プロパティの設定

プロパティが設定されている場合、KSK プロパティ\_TYPE\_SET 要求では、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーに設定する optomization モードが含まれます。

## <a name="requirements"></a>要件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 8.1 以降で使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
