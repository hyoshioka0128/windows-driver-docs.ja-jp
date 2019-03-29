---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOMAXFRAMERATE
description: このプロパティは、写真シーケンス モードにあるときに、カメラの最大のキャプチャのフレーム レートを提供します。
ms.assetid: 49A93E02-232C-4009-8F18-75D067CA7150
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMAXFRAMERATE ストリーミング メディア デバイス
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
ms.openlocfilehash: 452a233fdb5ef3316d86c96875e1a331f7856c79
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571469"
---
# <a name="kspropertycameracontrolextendedphotomaxframerate"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOMAXFRAMERATE

このプロパティは、写真シーケンス モードにあるときに、カメラの最大のキャプチャのフレーム レートを提供します。

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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

プロパティの値 (データの操作) が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と[ **KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)構造体。 1 秒あたりのフレームで最大フォト フレーム レートを設定または値として返される**KSCAMERA\_EXTENDEDPROP\_値**します。

フラグのセットではありません、**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)このプロパティの。

プロパティの合計データ サイズが**sizeof**(KSCAMERA\_EXTENDEDPROP\_ヘッダー) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_値)。 **サイズ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)はこのプロパティの合計データ サイズに設定します。

このプロパティのコントロールは、非同期およびないキャンセル可能なは。

## <a name="remarks"></a>コメント

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
<td>写真の暗証番号 (pin) の暗証番号 (pin) の ID。</td>
</tr>
<tr class="odd">
<td>サイズ</td>
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER) +</p>
<p>sizeof(KSCAMERA_EXTENDEDPROP_VALUE)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td><p>結果の最大フレーム レートを読み取ろうとしてエラー値。</p>
<p>それ以外の場合、0 を返します。</p></td>
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

フレーム レートの値の設定、**比率**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)します。 **Ratio.HighPart**フレーム レートの分子が含まれていますと**Ratio.LowPart**フレーム レートの分母が含まれています。

ドライバーは、フォト シーケンス モードでは、ときに、写真をキャプチャの最大フレーム レートを制限するために必要な場合があります。 これは、履歴のフレーム数での「時点」キャプチャ シナリオは、構成された時間範囲に含まれるようにします。 たとえば、メモリの制約に基づいて、アプリケーションが過去の履歴の価値の 1 秒をキャプチャする場合、必要があるため、キャプチャ レートを制限するフレームの N 個のみが必要です。

設定すると、カメラが高速のフレームをキャプチャできる場合でも提供されているフレーム レート、要求レート、ドライバーは使用する必要があります。 必要に応じて、ドライバーは、要求レートを対応するために余分なフレームをドロップできます。

最大フレーム レートの値を 0 に設定 (0、上位との下位の場合は 0 を**比率**) ドライバーの最大フレーム レートの設定をクリアし、フレームをできる限り迅速に提供するドライバーを確認すると同じ効果があります。  フレーム レートを 0 に設定すると、すべての後続のクエリは値を返します最大フレーム レートのカメラのドライバーの考えられる。 

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
