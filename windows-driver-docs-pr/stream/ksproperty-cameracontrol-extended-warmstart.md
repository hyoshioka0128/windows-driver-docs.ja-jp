---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_WARMSTART という
description: ウォーム スタート プロパティ コントロールは、故障のない操作を許可する準備がカメラの暗証番号 (pin) を保持するドライバーのヒントを提供します。
ms.assetid: EAC20371-6228-48F1-85FF-FAECC835B070
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_WARMSTART ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_WARMSTART
api_type:
- NA
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 62bab08cc8f2cf01b5fb9addf6518d91f96cec48
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341852"
---
# <a name="kspropertycameracontrolextendedwarmstart"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_WARMSTART という

ウォーム スタート プロパティ コントロールは、故障のない操作を許可する準備がカメラの暗証番号 (pin) を保持するドライバーのヒントを提供します。

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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

プロパティの値 (データの操作) が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造体。

フラグのセットではありません、**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)このプロパティの。

プロパティの合計データ サイズが**sizeof**(KSCAMERA\_EXTENDEDPROP\_ヘッダー)。 **サイズ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)はこのプロパティの合計データ サイズに設定します。

ウォーム スタートが有効か無効になっているを使用して、次のいずれかのフラグ、**機能**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header).

| ウォーム スタート フラグ                                  | 説明             |
|---------------------------------------------------|-------------------------|
| KSCAMERA\_EXTENDEDPROP\_WARMSTART という\_モード\_無効になっています。 | ウォーム スタートは無効です。 |
| KSCAMERA\_EXTENDEDPROP\_WARMSTART という\_モード\_有効  | ウォーム スタートは有効です。  |

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
<td>写真の暗証番号 (pin) の暗証番号 (pin) の ID。</td>
</tr>
<tr class="odd">
<td>サイズ</td>
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>機能</td>
<td><p>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL | KSCAMERA_EXTENDEDPROP_WARMSTART_MODE_DISABLED</p>
<p>- または -</p>
<p>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL | KSCAMERA_EXTENDEDPROP_WARMSTART_MODE_ENABLED</p></td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>0</td>
</tr>
</tbody>
</table>

**結果**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)は常に get 操作では 0 に設定します。

## <a name="see-also"></a>関連項目

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)
