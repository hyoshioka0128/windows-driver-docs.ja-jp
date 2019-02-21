---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_EVCOMPENSATION
description: EV 補正プロパティは、露出ユニット単位、またはゾーン システムに、コントロールの露出の調整を使用できます。
ms.assetid: 1109C533-89CA-4A23-BCF9-D44C28C0C6BF
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_EVCOMPENSATION ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_EVCOMPENSATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: e99f765cd327079a5d2fdf2545d71ec1120b96e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561002"
---
# <a name="kspropertycameracontrolextendedevcompensation"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_EVCOMPENSATION


EV 補正プロパティは、露出ユニット単位、またはゾーン システムに、コントロールの露出の調整を使用できます。

### <a name="usage-summary-table"></a>使用状況の概要テーブル

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

 

プロパティの値 (データの操作) が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と[ **KSCAMERA\_EXTENDEDPROP\_EVCOMPENSATION** ](https://msdn.microsoft.com/library/windows/hardware/dn567561)構造体。

プロパティの合計データ サイズが**sizeof**(KSCAMERA\_EXTENDEDPROP\_ヘッダー) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_EVCOMPENSATION)。 **サイズ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)はこのプロパティの合計データ サイズに設定します。

**機能**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)次の 1 つ以上のビット演算 OR の組み合わせが含まれています補正の設定です。

| EV 補正ステップ実行                    | 説明                                                             |
|---------------------------------------------|-------------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_EVCOMP\_進み   | EV 危険度の値の 1 つの 6 番目 (1/6) の手順で変更を補正します。  |
| KSCAMERA\_EXTENDEDPROP\_EVCOMP\_QUARTERSTEP | EV 危険度の値の 4 分の 1 (1/4) の手順で変更を補正します。 |
| KSCAMERA\_EXTENDEDPROP\_EVCOMP\_THIRDSTEP   | EV 危険度の値の 3 分の 1 (1/3) の手順で変更を補正します。  |
| KSCAMERA\_EXTENDEDPROP\_EVCOMP\_HALFSTEP    | EV 補正の変更の半分の危険度の値 (1/2) の手順。   |
| KSCAMERA\_EXTENDEDPROP\_EVCOMP\_FULLSTEP    | EV 補正は、いずれかで変更の危険度の値 (1/1) の手順。        |

 

**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)カメラ (1 つの値) のステップ実行の現在の EV 報酬が含まれています.最も低い EV 補正ステップ サイズに対してのみのサポートを提供するは、ドライバーがお勧めします。

このプロパティのコントロールは、非同期およびないキャンセル可能なは。

<a name="remarks"></a>注釈
-------

### <a name="getting-the-property"></a>プロパティを取得

KSPROPERTY に応答するとき\_型\_GET 要求をドライバーのメンバーの設定、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)に、次の場合。

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
<td>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0 XFFFFFFFF) です。</td>
</tr>
<tr class="odd">
<td>サイズ</td>
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_EVCOMPENSATION)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>機能</td>
<td>ドライバーによってサポートされているフラグをステップ実行します。</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>現在のステップ実行の値を設定します。</td>
</tr>
</tbody>
</table>

 

ドライバーの設定でのステップ実行現在 EV 補正**フラグ**します。 メンバー [ **KSCAMERA\_EXTENDEDPROP\_EVCOMPENSATION** ](https://msdn.microsoft.com/library/windows/hardware/dn567561)ステップ単位の現在の範囲と補正するための手順の数を示します。

### <a name="setting-the-property"></a>プロパティの設定

設定すると、プロパティを KSPROPERTY\_型\_セットの要求、**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) EV 補正を使用するステップが含まれます。 新しい補正するためのステップ単位数設定**値**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_EVCOMPENSATION**](https://msdn.microsoft.com/library/windows/hardware/dn567561)します。

<a name="requirements"></a>要件
------------

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

[**KSCAMERA\_EXTENDEDPROP\_EVCOMPENSATION**](https://msdn.microsoft.com/library/windows/hardware/dn567561)
