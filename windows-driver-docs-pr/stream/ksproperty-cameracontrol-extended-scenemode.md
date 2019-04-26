---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_SCENEMODE
description: シーンの mode プロパティは、事前設定されたコントロールのコレクションを表すドライバーが定義されているモードを選択します。
ms.assetid: 32C350FF-AA54-4F28-8AD2-341A31648B60
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5af16830e4ebdf1c98da667000d2dffc70c98675
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351810"
---
# <a name="kspropertycameracontrolextendedscenemode"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_SCENEMODE

シーンの mode プロパティは、事前設定されたコントロールのコレクションを表すドライバーが定義されているモードを選択します。 ドライバーは、シーンのモードに割り当てられているプリセットを決定し、シーンが選択されているときにこれらのコントロールの設定を有効にします。

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
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

プロパティの値 (データの操作) が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と[ **KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)構造体。 **KSCAMERA\_EXTENDEDPROP\_値**が必要ですが、**値**メンバーは無視されます。

プロパティの合計データ サイズが**sizeof**(KSCAMERA\_EXTENDEDPROP\_ヘッダー) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_値)。 **サイズ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)はこのプロパティの合計データ サイズに設定します。

**機能**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)次の 1 つ以上のビット演算 OR の組み合わせが含まれていますドライバーでサポートされているシーン モード。

| シーンのモード                                       | 説明                                                           |
|--------------------------------------------------|-----------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_自動          | 自動の匂いモード。 コントロールでは、自動設定です。            |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_マクロ         | マクロのシーン モード (ドライバーが定義されている)。                                    |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_縦向き      | 縦シーン モード (ドライバーが定義されている)。                                 |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_スポーツ         | スポーツ シーン モード (ドライバーが定義されている)。                                    |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_雪          | 雪シーン モード (ドライバーが定義されている)。                                     |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_夜間         | 夜間シーン モード (ドライバーが定義されている)。                                    |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_ビーチ         | ビーチ シーン モード (ドライバーが定義されている)。                                    |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_日没        | サンセット モード (ドライバーが定義されている)。                                   |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_CANDLELIGHT   | Candlelight シーン モード (ドライバーが定義されている)。                              |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_ランドス ケープ     | 横シーン モード (ドライバーが定義されている)。                                |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_NIGHTPORTRAIT | 夜間縦シーン モード (ドライバーが定義されている)。                           |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_バックライト       | バックライト シーン モード (ドライバーが定義されている)。                                  |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_手動        | コントロールが手動で変更され、事前に定義されたシーン モードが設定されていません。 |

**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)シーン モードが現在のカメラの設定が含まれています。 カメラの既定のシーンのモードは、常に KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_自動。

このプロパティのコントロールは、非同期およびないキャンセル可能なは。

## <a name="remarks"></a>注釈

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
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |(シーン モード サポートされている値)。</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>現在のシーン モード値の設定 (1 つの値)。</td>
</tr>
</tbody>
</table>

シーンのモードが以前設定されていない場合、**フラグ**KSCAMERA に設定されている\_EXTENDEDPROP\_SCENEMODE\_自動 (既定値)。

### <a name="setting-the-property"></a>プロパティの設定

設定すると、プロパティを KSPROPERTY\_型\_セットの要求、**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)シーンのモード有効にするのににはが含まれます。

## <a name="requirements"></a>要件

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
