---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_OPTIMIZATIONHINT
description: カメラのドライバーは、アプリケーションによって提供されるヒントに基づく、キャプチャ操作を最適化可能性があります。 このプロパティは、どのような操作が可能性に基づいて、パフォーマンスの戦略を設定するドライバーは最もよく使用を通知します。
ms.assetid: FEA3D355-B490-4E67-905D-EE5507E91150
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT ストリーミング メディア デバイス
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
ms.openlocfilehash: c9af2b8d67f65cb8051aeb1f908d2e1a2a4fb644
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569646"
---
# <a name="kspropertycameracontrolextendedoptimizationhint"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_OPTIMIZATIONHINT

カメラのドライバーは、アプリケーションによって提供されるヒントに基づく、キャプチャ操作を最適化可能性があります。 このプロパティは、どのような操作が可能性に基づいて、パフォーマンスの戦略を設定するドライバーは最もよく使用を通知します。 たとえばの写真の最適化時にカメラのドライバーはセンサー露出の速度とイメージをキャプチャするには、写真のキャプチャのトリガーから少ない待機時間の解像度を最適化するためにセンサーをプログラム可能性があります。 同様に、ビデオ用の最適化時にカメラのドライバーはフレーム レートが低い解像度で、センサーをプログラミング可能性があります。

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
<th>取得</th>
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

プロパティの値 (データの操作) が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と[ **KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)構造体。

プロパティの合計データ サイズが**sizeof**(KSCAMERA\_EXTENDEDPROP\_ヘッダー) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_値)。 **サイズ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)はこのプロパティの合計データ サイズに設定します。

**機能**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)次の 1 つ以上のビット演算 OR の組み合わせが含まれています最適化ヒント。

| 最適化ヒント                           | 説明                               |
|---------------------------------------------|-------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_最適化\_写真 | カメラの操作は、写真に最適です。 |
| KSCAMERA\_EXTENDEDPROP\_最適化\_ビデオ | カメラの操作は、ビデオに最適です。  |

**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)カメラ (1 つの値) に設定されている最適化が含まれています。

既定の最適化の種類は KSCAMERA\_EXTENDEDPROP\_最適化\_写真。 このプロパティは、カメラ ドライバーでサポートされて、両方の最適化の種類をサポートする必要があります。

このプロパティのコントロールは、同期およびないキャンセル可能なは。

## <a name="remarks"></a>コメント

### <a name="optimization-modes"></a>最適化モード

**KSCAMERA\_EXTENDEDPROP\_最適化\_写真**
-   カメラのすべてのドライバーが、KSCAMERA を使用して明示的に通知されるまで、このモードである必要があります\_EXTENDEDPROP\_最適化\_ビデオ モード。 このモードの目的は、写真の操作のカメラのハードウェアを最適化するためにです。 ビデオ操作は、このモードで機能する必要があります。

**KSCAMERA\_EXTENDEDPROP\_最適化\_ビデオ**
-   このモードでは、ビデオの操作の場合、カメラを使用することを示します。 カメラのドライバーでは、このモードの操作でビデオ ハードウェアを最適化する必要があります。 写真の操作は、機能である必要がありますが、リソース使用量の優先度のビデオの操作があります。

### <a name="getting-the-property"></a>プロパティを取得

KSPROPERTY に応答するとき\_型\_GET 要求をドライバーのメンバーの設定、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)に、次の場合。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Member</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>バージョン</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0 XFFFFFFFF) です。</td>
</tr>
<tr class="odd">
<td>サイズ</td>
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VALUE)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>機能</td>
<td>サポートされている値を最適化します。</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>現在最適化の値の設定。</td>
</tr>
</tbody>
</table>

設定の最適化モードが既に設定されていない場合、ドライバー**フラグ**KSCAMERA に\_EXTENDEDPROP\_最適化\_写真 (既定値)。

### <a name="setting-the-property"></a>プロパティの設定

設定すると、プロパティを KSPROPERTY\_型\_セットの要求、**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)設定の最適化モードにが含まれます。

## <a name="requirements"></a>必要条件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 8.1 以降を利用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
