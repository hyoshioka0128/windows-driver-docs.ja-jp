---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_SCENEMODE
description: シーンモードプロパティは、事前設定されたコントロールのコレクションを表すドライバー定義モードを選択します。
ms.assetid: 32C350FF-AA54-4F28-8AD2-341A31648B60
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE ストリーミングメディアデバイス
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
ms.openlocfilehash: 9ff76b779c92e09f8e28b7c1e695d49981a8f8fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823958"
---
# <a name="ksproperty_cameracontrol_extended_scenemode"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_SCENEMODE

シーンモードプロパティは、事前設定されたコントロールのコレクションを表すドライバー定義モードを選択します。 ドライバーは、シーンモードに割り当てられているプリセットを特定し、シーンを選択したときにコントロールの設定を有効にします。

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

プロパティ値 (操作データ) には、 [**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と、 [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)の構造体が含まれています。 **KSCAMERA\_EXTENDEDPROP\_値**が必要ですが、**値**メンバーは無視されます。

プロパティデータの合計サイズは**sizeof**(KSCAMERA\_extendedprop\_HEADER) + **sizeof**(KSCAMERA\_extendedprop\_値) です。 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**機能**メンバーには、ドライバーでサポートされている次のシーンモードの1つ以上のビットごとの or の組み合わせが含まれています。

| シーンモード                                       | 説明                                                           |
|--------------------------------------------------|-----------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_AUTO          | 自動匂いモード。 コントロールは、自動的に設定されます。            |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_マクロ         | マクロシーンモード (定義されているドライバー)。                                    |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_縦長      | 縦長シーンモード (定義済みドライバー)。                                 |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_スポーツ         | スポーツシーンモード (定義されているドライバー)。                                    |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_雪          | 雪シーンモード (定義されているドライバー)。                                     |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_夜         | 夜間シーンモード (定義されているドライバー)。                                    |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_ビーチ         | ビーチシーンモード (定義されているドライバー)。                                    |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_日没        | 日没シーンモード (定義されているドライバー)。                                   |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_CANDLELIGHT   | Candlelight シーンモード (定義されているドライバー)。                              |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_ランドスケープ     | 横長シーンモード (定義されているドライバー)。                                |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_NIGHTPORTRAIT | 夜間のシーンモード (定義されているドライバー)。                           |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_バックライト       | バックライトシーンモード (定義されているドライバー)。                                  |
| KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_MANUAL        | コントロールが手動で変更され、定義済みのシーンモードは設定されていません。 |

[**KSCAMERA\_EXTENDEDPROP\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーには、カメラに現在設定されているシーンモードが含まれています。 カメラの既定のシーンモードは、常に KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_AUTO に設定されています。

このプロパティコントロールは非同期であり、キャンセルできません。

## <a name="remarks"></a>注釈

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
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |(シーンモードの値がサポートされています)。</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>現在のシーンモード値の設定 (1 つの値のみ)。</td>
</tr>
</tbody>
</table>

シーンモードが以前に設定されていない場合、 **Flags**は KSCAMERA\_extendedprop\_SCENEMODE\_AUTO (既定) に設定されます。

### <a name="setting-the-property"></a>プロパティの設定

プロパティが設定されている場合、KSK プロパティ\_TYPE\_SET 要求では、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーには、有効にするシーンモードが含まれます。

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
