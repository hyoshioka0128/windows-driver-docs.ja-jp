---
title: KSK プロパティ\_CAMERACONTROL\_拡張\_PHOTOMAXFRAMERATE
description: このプロパティは、カメラがフォトシーケンスモードの場合の最大キャプチャフレームレートを示します。
ms.assetid: 49A93E02-232C-4009-8F18-75D067CA7150
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMAXFRAMERATE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMAXFRAMERATE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: b3ad8b4c4104e2204f42c16e4488e3c870a2ebbd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841586"
---
# <a name="ksproperty_cameracontrol_extended_photomaxframerate"></a>KSK プロパティ\_CAMERACONTROL\_拡張\_PHOTOMAXFRAMERATE

このプロパティは、カメラがフォトシーケンスモードの場合の最大キャプチャフレームレートを示します。

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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

プロパティ値 (操作データ) には、 [**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と、 [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)の構造体が含まれています。 1秒あたりのフレーム数の最大フォトフレームレートは、 **KSCAMERA\_EXTENDEDPROP\_値**の値として設定または返されます。

このプロパティの[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**flags**メンバーには、フラグが設定されていません。

プロパティデータの合計サイズは**sizeof**(KSCAMERA\_extendedprop\_HEADER) + **sizeof**(KSCAMERA\_extendedprop\_値) です。 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

このプロパティコントロールは非同期であり、キャンセルできません。

## <a name="remarks"></a>注釈

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
<td>フォト pin の pin ID。</td>
</tr>
<tr class="odd">
<td>Size</td>
<td><p>sizeof (KSCAMERA_EXTENDEDPROP_HEADER) +</p>
<p>sizeof (KSCAMERA_EXTENDEDPROP_VALUE)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td><p>最大フレームレートを読み取ろうとした結果のエラー値。</p>
<p>それ以外の場合は0です。</p></td>
</tr>
<tr class="odd">
<td>機能</td>
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>0</td>
</tr>
</tbody>
</table>

フレームレートの値は、 [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)の**比率**メンバーで設定されます。 **比率. HighPart**には、フレームレートと比率の分子が含まれ**ます。 lowpart**には、フレームレートの分母が含まれます。

ドライバーがフォトシーケンスモードの場合、写真キャプチャの最大フレームレートを制限する必要がある場合があります。 これは、構成された期間内に、特定の数の履歴フレームを含む "モーメントインタイム" キャプチャシナリオが含まれるようにするためです。 たとえば、メモリの制約に基づいて、アプリケーションで過去の履歴を1秒分キャプチャする場合は、キャプチャレートを上限にする必要があります。これにより、必要なフレーム数は N 個だけになります。

設定すると、カメラがフレームを要求された速度で高速にキャプチャできる場合でも、ドライバーはフレームレートを使用する必要があります。 必要に応じて、ドライバーは、要求されたレートに合わせて余分なフレームをドロップできます。

最大フレームレートの値を 0 (HighPart の場合は0、**比率**の lowpart の場合は 0) に設定すると、ドライバーの最大フレームレート設定がクリアされ、可能な限り高速にフレームを提供するようにドライバーに指示した場合と同じ効果が得られます。  フレームレートが0に設定されると、その後のクエリでは、カメラドライバーで可能な最大フレームレートの値が返されます。 

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
