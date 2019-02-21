---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_FOCUSMODE
description: フォーカス モードのプロパティは、auto、カメラの手動、および既定のフォーカス モードを制御します。
ms.assetid: FA014A4B-0CD3-4288-B721-4A73CDD28551
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSMODE ストリーミング メディア デバイス
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
ms.openlocfilehash: 4a6504be2543611f462bde0934e9a903be368497
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549482"
---
# <a name="kspropertycameracontrolextendedfocusmode"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_FOCUSMODE

フォーカス モードのプロパティは、auto、カメラの手動、および既定のフォーカス モードを制御します。

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

プロパティの値 (データの操作) が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と[ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://msdn.microsoft.com/library/windows/hardware/dn567566)構造体。

プロパティの合計データ サイズが**sizeof**(KSCAMERA\_EXTENDEDPROP\_ヘッダー) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING). **サイズ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)はこのプロパティの合計データ サイズに設定します。

**機能**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)次の 1 つ以上のビット演算 OR の組み合わせが含まれていますビデオの処理オプション。

| 処理とフォーカス モード                        | 説明                                                                  |
|--------------------------------------------------|------------------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自動      | カメラのドライバーでは、ビデオを独自の処理ロジックを使用します。                       |
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手動    | カメラのドライバーでは、事前設定された処理メソッドまたはベース温度メソッドを使用します。 |
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロック      | 現在のビデオの処理方法がロックされています。                               |
| KSCAMERA\_EXTENDEDPROP\_フォーカス\_CONTINUOUS        | 集約の中心が設定されていません。                                               |
| KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_マクロ      | マクロの範囲の焦点の収束します。                                               |
| KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_標準     | 通常の範囲の焦点収束します。                                              |
| KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_引き  | さまざまな焦点収束します。                                                |
| KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_無限大   | 無限の範囲の焦点収束します。                                            |
| KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_HYPERFOCAL | Hyperfocal 範囲です。                                                            |

**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)カメラ現在設定されているビデオ処理フラグが含まれています。 場合 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_KSCAMERA で自動設定を組み合わせることができます\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロックします。

このプロパティのコントロールは、非同期とキャンセル可能なは。

## <a name="remarks"></a>注釈

### <a name="processing-modes"></a>処理モード

**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO**

このフラグは、自動のフォーカス操作では、完了イベントがトリガーされたときに集中することを示します。 このフラグが KSCAMERA と組み合わせた場合に、完了すると、\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロック、フォーカスが分岐し、カメラのドライバーを続行しよう収束します。 場合、KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロック フラグを含めると、フォーカスは、最初の収束がロックされているし、新しいフォーカス コマンドを受信するまで変更されません。

Auto モードの場合は、結合することがなく、ロックが既にロックされているコントロールとして扱う no-op カメラ ドライバーによって。 Auto モードの場合と組み合わせて、ロックが既にロックされているコントロールでは新しい収束が開始する必要があります。

このフラグは、KSCAMERA で相互に排他的\_EXTENDEDPROP\_VIDEOPROCFLAG\_手動と KSCAMERA\_EXTENDEDPROP\_フォーカス\_継続的なフラグ。

**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手動**

手動では、このビデオの処理の特定の値を指定することを示します。 特定の値は、ドライバーに提供されます。

このフラグは、KSCAMERA と組み合わせることはない\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO、KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロック、または KSCAMERA\_EXTENDEDPROP\_フォーカス\_連続。

**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロック**

このフラグの設定されている対応する KSCAMERA せず場合\_EXTENDEDPROP\_VIDEOPROCFLAG\_自動フラグ、カメラのドライバーが現在のフォーカス状態のロックが必要ですし、フォーカス 1 回の完了イベントのトリガーがロックされています。 カメラのドライバーは、新しいフォーカス コマンドが受信されるまで、フォーカスの状態を変更しなければなりません。 場合 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自動はこのフラグを組み合わせて、カメラのドライバーは自動フォーカスに収束し収束するポイントにフォーカスをロックし、完了イベントをトリガーします。 このフラグは、する必要があります KSCAMERA と結合できない\_EXTENDEDPROP\_フォーカス\_CONTINUOUS または KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手動です。

KSCAMERA と組み合わせない限り、このフラグをフォーカス コントロールの範囲のフラグを指定できません。\_EXTENDEDPROP\_VIDEOPROCFLAG\_自動。 その場合は、フォーカスがフォーカス設定の自動スキャンを試行する場所を特定する範囲フラグを使用して実行されます。 次に、収束すると、フォーカス設定をロックし、完了イベントが発生します。

**KSCAMERA\_EXTENDEDPROP\_フォーカス\_CONTINUOUS**

このフラグは、フォーカスが継続的なことを示します。 意味がない 1 つの収束フォーカス コントロールの場合。 ドライバーは、この要求を受け入れるし、すぐに非同期操作を完了する必要があります。

このフラグは、KSCAMERA と組み合わせることはない\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO、KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロック、または KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手動です。

このモードは、すべてのドライバーに必要です。

**KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_マクロ**

このフラグは、マクロの範囲のフォーカスの収束を実行することを示します。 正確な焦点範囲は、ドライバーによって決定されます。 このフラグは、KSCAMERA と組み合わせることも\_EXTENDEDPROP\_VIDEOPROCFLAG\_自動と KSCAMERA\_EXTENDEDPROP\_フォーカス\_連続。

**KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_標準**

このフラグは、通常の範囲のフォーカスの収束を実行することを示します。 正確な焦点範囲は、ドライバーによって決定されます。 このフラグは、KSCAMERA と組み合わせることも\_EXTENDEDPROP\_VIDEOPROCFLAG\_自動と KSCAMERA\_EXTENDEDPROP\_フォーカス\_連続。

**KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_引き**

このフラグは、完全な範囲のフォーカスの収束を実行することを示します。 正確な焦点範囲は、ドライバーによって決定されます。 このフラグは、KSCAMERA と組み合わせることも\_EXTENDEDPROP\_VIDEOPROCFLAG\_自動と KSCAMERA\_EXTENDEDPROP\_フォーカス\_連続。

このモードは、すべてのドライバーに必要です。

**KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_無限大**

このフラグは、無限の範囲のフォーカスの収束を実行することを示します。 正確な焦点範囲は、ドライバーによって決定されます。 このフラグは、KSCAMERA と組み合わせることも\_EXTENDEDPROP\_VIDEOPROCFLAG\_自動と KSCAMERA\_EXTENDEDPROP\_フォーカス\_連続。

**KSCAMERA\_EXTENDEDPROP\_フォーカス\_範囲\_HYPERFOCAL**

このフラグは、hyperfocal 範囲のフォーカスの収束を実行することを示します。 正確な焦点範囲は、ドライバーによって決定されます。 このフラグは、KSCAMERA と組み合わせることも\_EXTENDEDPROP\_VIDEOPROCFLAG\_自動と KSCAMERA\_EXTENDEDPROP\_フォーカス\_連続。

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
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>機能</td>
<td><p>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL | KSCAMERA_EXTENDEDPROP_CAPS_CANCELLABLE |</p>
<p>(ビデオ処理とフォーカス モードはサポート)</p></td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>現在のビデオの処理とフォーカス モード。</td>
</tr>
</tbody>
</table>


以前フォーカス範囲のフラグが設定されていない場合のドライバー設定**フラグ**KSCAMERA に\_EXTENDEDPROP\_フォーカス\_範囲\_KSCAMERA と共に引き\_EXTENDEDPROP\_VIDEOPROCFLAG\_自動 (既定値)。 メンバー、 [ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://msdn.microsoft.com/library/windows/hardware/dn567566)に続く構造[ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)フォーカス モードの要件に従って設定されます。

**VideoProp.Value.ull** KSCAMERA モードの場合、値が現在の危険度の設定を含める必要があります\_EXTENDEDPROP\_VIDEOPROCFLAG\_自動。

### <a name="setting-the-property"></a>プロパティの設定

設定すると、プロパティを KSPROPERTY\_型\_セットの要求、**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)はフォーカス モード設定にはが含まれます。 **VideoProc.Value**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://msdn.microsoft.com/library/windows/hardware/dn567566)ときに無視する必要があります**フラグ** 、KSCAMERA を含む\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO、KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロック、KSCAMERA\_EXTENDEDPROP\_フォーカス\_継続的なフラグ。

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

[**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://msdn.microsoft.com/library/windows/hardware/dn567566)
