---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FOCUSMODE
description: フォーカスモードプロパティは、カメラの自動、手動、およびプリセットのフォーカスモードを制御します。
ms.assetid: FA014A4B-0CD3-4288-B721-4A73CDD28551
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSMODE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4fb6fb1eb23baff1c9beace4461ae1f0a3cb015d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843227"
---
# <a name="ksproperty_cameracontrol_extended_focusmode"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FOCUSMODE

フォーカスモードプロパティは、カメラの自動、手動、およびプリセットのフォーカスモードを制御します。

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

プロパティ値 (操作データ) には、 [**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造体と、 [**KSCAMERA\_EXTENDEDPROP\_videoprocsetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)構造体が含まれています。

プロパティデータの合計サイズは**sizeof**(KSCAMERA\_extendedprop\_HEADER) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_videoprocsetting) です。 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**機能**メンバーには、次のビデオ処理オプションの1つ以上のビットごとの or の組み合わせが含まれています。

| 処理モードとフォーカスモード                        | 説明                                                                  |
|--------------------------------------------------|------------------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_AUTO      | カメラドライバーは、ビデオに独自の処理ロジックを使用します。                       |
| KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_手動    | カメラドライバーは、事前設定の処理方法または温度ベースの方法を使用します。 |
| KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_ロック      | 現在のビデオ処理方法はロックされています。                               |
| KSCAMERA\_EXTENDEDPROP\_フォーカス\_継続        | 収束の焦点を設定していません。                                               |
| KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_マクロ      | マクロ範囲の焦点収束。                                               |
| KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_通常     | 通常の範囲の焦点収束。                                              |
| KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_FULLRANGE  | 範囲内のすべての焦点収束。                                                |
| KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_無限大   | 無限範囲の焦点収束。                                            |
| KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_ハイパーフォーカス | Hyperfocal の範囲。                                                            |

[**KSCAMERA\_EXTENDEDPROP\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーには、カメラに現在設定されているビデオ処理フラグが含まれています。 KSCAMERA\_EXTENDEDPROP\_videoが FLAG\_AUTO 設定を、KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_ロックと組み合わせることができます。

このプロパティコントロールは非同期で、キャンセル可能です。

## <a name="remarks"></a>注釈

### <a name="processing-modes"></a>処理モード

**KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_AUTO**

このフラグは、完了イベントがトリガーされたときに、自動フォーカス操作が収束したことを示します。 完了時、およびこのフラグが KSCAMERA\_EXTENDEDPROP と結合されていない場合は、\_VIDEOPROP フラグ\_ロックされると、フォーカスが変わることがあり、カメラドライバーは収束を試行し続ける可能性があります。 KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_ロックフラグが含まれている場合、フォーカスは最初の収束にロックされ、新しいフォーカスコマンドが受信されるまでは変更されません。

自動モードを結合せずにロックを解除すると、既にロックされているコントロールはカメラドライバーによる操作なしとして扱われます。 ロックは、Auto モードと組み合わせて、既にロックされているコントロールを使用して新しい収束をトリガーする必要があります。

このフラグは、KSCAMERA\_EXTENDEDPROP\_VIDEOCONTINUOUS FLAG\_MANUAL および KSCAMERA\_EXTENDEDPROP\_連続フラグ\_フォーカスされています。

**KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_手動**

Manual は、このビデオ処理で特定の値が指定されていることを示します。 ドライバーには特定の値が指定されます。

このフラグは、KSCAMERA\_EXTENDEDPROP\_videoて FLAG\_AUTO、KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_LOCK、または KSCAMERA\_EXTENDEDPROP\_フォーカス\_継続することはできません。

**KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_ロック**

対応する KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_AUTO フラグを指定せずにこのフラグが設定されている場合、カメラドライバーは、フォーカスがロックされると、現在のフォーカス状態をロックし、完了イベントをトリガーします。 カメラドライバーは、新しいフォーカスコマンドが受信されるまでフォーカス状態を変更しないようにする必要があります。 KSCAMERA\_EXTENDEDPROP PROP によって、このフラグを自動的に結合する\_、このフラグを自動で結合した場合、カメラドライバーは自動フォーカス時に収束し、その収束ポイントにフォーカスを固定して、完了イベントをトリガーします。 このフラグは、KSCAMERA\_EXTENDEDPROP\_フォーカス\_CONTINUOUS または KSCAMERA\_EXTENDEDPROP\_VIDEO FLAG\_MANUAL と組み合わせて使用することはできません。

このフラグは、KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_AUTO で結合されている場合を除き、フォーカスコントロールの範囲フラグと共に指定することはできません。 その場合、フォーカスは範囲フラグを使用して実行され、自動フォーカススキャンを試行する場所を決定します。 その後、収束時にフォーカス設定のロックと完了イベントが発生します。

**KSCAMERA\_EXTENDEDPROP\_フォーカス\_継続**

このフラグは、フォーカスが連続していることを示します。 この場合、フォーカスコントロールの1つの収束ポイントはありません。 ドライバーは、この要求を受け入れ、非同期操作を直ちに完了する必要があります。

このフラグは、KSCAMERA\_EXTENDEDPROP PROP と組み合わせて使用することはできません。\_AUTO、KSCAMERA\_EXTENDEDPROP\_VIDEO flag\_LOCK、または KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_手動。

このモードはすべてのドライバーに必要です。

**KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_マクロ**

このフラグは、マクロ範囲に対してフォーカスの収束を実行する必要があることを示します。 正確な範囲はドライバーによって決まります。 このフラグは、KSCAMERA\_EXTENDEDPROP\_VIDEOPROP フラグ\_AUTO および KSCAMERA\_EXTENDEDPROP\_連続\_に焦点を合わせることができます。

**KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_通常**

このフラグは、通常の範囲でフォーカスの収束を実行する必要があることを示します。 正確な範囲はドライバーによって決まります。 このフラグは、KSCAMERA\_EXTENDEDPROP\_VIDEOPROP フラグ\_AUTO および KSCAMERA\_EXTENDEDPROP\_連続\_に焦点を合わせることができます。

**KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_FULLRANGE**

このフラグは、全体の範囲に対してフォーカスの収束を実行する必要があることを示します。 正確な範囲はドライバーによって決まります。 このフラグは、KSCAMERA\_EXTENDEDPROP\_VIDEOPROP フラグ\_AUTO および KSCAMERA\_EXTENDEDPROP\_連続\_に焦点を合わせることができます。

このモードはすべてのドライバーに必要です。

**KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_無限大**

このフラグは、無限の範囲に対してフォーカスの収束を実行する必要があることを示します。 正確な範囲はドライバーによって決まります。 このフラグは、KSCAMERA\_EXTENDEDPROP\_VIDEOPROP フラグ\_AUTO および KSCAMERA\_EXTENDEDPROP\_連続\_に焦点を合わせることができます。

**KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_ハイパーフォーカス**

このフラグは、ハイパーフォーカス範囲に対してフォーカス収束を実行する必要があることを示します。 正確な範囲はドライバーによって決まります。 このフラグは、KSCAMERA\_EXTENDEDPROP\_VIDEOPROP フラグ\_AUTO および KSCAMERA\_EXTENDEDPROP\_連続\_に焦点を合わせることができます。

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
<td><p>sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>機能</td>
<td><p>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |KSCAMERA_EXTENDEDPROP_CAPS_CANCELLABLE |</p>
<p>(サポートされているビデオ処理およびフォーカスモード)</p></td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>現在のビデオ処理およびフォーカスモード。</td>
</tr>
</tbody>
</table>


前にフォーカス範囲のフラグが設定されていない場合、ドライバーは KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_FULLRANGE を KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_AUTO (既定値)**に設定し**ます。 [**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の後にある[**KSCAMERA\_EXTENDEDPROP\_videoの設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)の構造体のメンバーは、フォーカスモードの要件に従って設定されます。

モードが KSCAMERA\_EXTENDEDPROP\_VIDEOPROP フラグ\_AUTO の場合、 **u)** 値には現在の露出設定が含まれている必要があります。

### <a name="setting-the-property"></a>プロパティの設定

プロパティが設定されている場合、KSK プロパティ\_TYPE\_SET 要求では、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーに設定するフォーカスモードが含まれます。 **フラグ**に KSCAMERA\_extendedprop\_videoproc FLAG\_AUTO、\_が含まれている場合は、 [**KSCAMERA\_extendedprop\_videoproc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)値のメンバーを無視する必要があります **。** EXTENDEDPROP\_、\_LOCK、KSCAMERA\_EXTENDEDPROP\_フォーカス\_連続フラグ。

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

[**KSCAMERA\_EXTENDEDPROP\_VIDEOの設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)
