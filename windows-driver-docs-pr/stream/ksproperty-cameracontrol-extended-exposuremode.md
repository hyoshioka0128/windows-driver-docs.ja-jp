---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_EXPOSUREMODE
description: 露出制御プロパティは、公開のために自動処理が行われるか、または手動の時刻値が代わりに使用されるかを指定します。
ms.assetid: 54D4F286-09F2-48B5-9A7A-9445999972BD
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_EXPOSUREMODE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_EXPOSUREMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7ceca5a9fe3e0c53e670f6e39b6dd02292b35380
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843239"
---
# <a name="ksproperty_cameracontrol_extended_exposuremode"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_EXPOSUREMODE

露出制御プロパティは、公開のために自動処理が行われるか、または手動の時刻値が代わりに使用されるかを指定します。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| [購入] | 設定 | 対象 | プロパティ記述子の型 | プロパティ値の型 |
|---|---|---|---|---|
| [はい] | [はい] | フィルター | [**Ksproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) | [**KSCAMERA_EXTENDEDPROP_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) |

プロパティ値 (操作データ) には、 [**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造体と、 [**KSCAMERA\_EXTENDEDPROP\_videoprocsetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)構造体が含まれています。

プロパティデータの合計サイズは**sizeof**(KSCAMERA\_extendedprop\_HEADER) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_videoprocsetting) です。 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**size**メンバーは、この total property データサイズに設定されます。

[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**機能**メンバーには、次のビデオ処理オプションの1つ以上のビットごとの or の組み合わせが含まれています。

| 処理モード                               | 説明                                                                  |
|-----------------------------------------------|------------------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_AUTO   | カメラドライバーは、ビデオに独自の処理ロジックを使用します。                       |
| KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_手動 | カメラドライバーは、事前設定の処理方法を使用します。                               |
| KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_ロック   | 現在のビデオ処理方法はロックされています。                               |

 

[**KSCAMERA\_EXTENDEDPROP\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーには、カメラに現在設定されているビデオ処理フラグが含まれています。 KSCAMERA\_EXTENDEDPROP\_VIDEOが FLAG\_AUTO 設定を、KSCAMERA\_EXTENDEDPROP\_VIDEO FLAG\_LOCK と組み合わせることができます。

このプロパティコントロールは非同期で、キャンセル可能です。

## <a name="remarks"></a>注釈

### <a name="processing-modes"></a>処理モード

<span id="KSCAMERA_EXTENDEDPROP_VIDEOPROCFLAG_AUTO"></span><span id="kscamera_extendedprop_videoprocflag_auto"></span>KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_AUTO  
これは、自動処理がサポートされていることを示します。 ドライバーは、内部ロジックを使用してビデオ処理を最適化します。 \_GET 要求の\_に KSK プロパティを指定する場合、 [**KSCAMERA\_EXTENDEDPROP\_VIDEOPROC 設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)の**videoproc**メンバーには、ビデオ処理に対して決定された現在のドライバー値が含まれている必要があります。

このフラグは、ビットごとの OR 値として KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_ロックと組み合わせることができます。

自動モードを結合せずにロックを解除すると、既にロックされているコントロールはカメラドライバーによる操作なしとして扱われます。 ロックは、Auto モードと組み合わせて、既にロックされているコントロールを使用して新しい収束をトリガーする必要があります。

このフラグは、KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_MANUAL と組み合わせることはできません。

<span id="KSCAMERA_EXTENDEDPROP_VIDEOPROCFLAG_MANUAL"></span><span id="kscamera_extendedprop_videoprocflag_manual"></span>KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_手動  
Manual は、このビデオ処理で特定の値が指定されていることを示します。 ドライバーには特定の値が指定されます。

このフラグは、KSCAMERA\_EXTENDEDPROP\_VIDEOPROP FLAG\_AUTO または KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_ロックと組み合わせることはできません。

<span id="KSCAMERA_EXTENDEDPROP_VIDEOPROCFLAG_LOCK"></span><span id="kscamera_extendedprop_videoprocflag_lock"></span>KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_ロック  
Lock option フラグは、現在のビデオ処理が、現在プログラミングされている値にロックされていることを示します。 たとえば、アプリケーションでは、特定の公開が決定されるまで auto モードを要求できます。 この時点で、アプリケーションはすべての写真を同じように表示します。 このような場合、アプリケーションでは、KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_ロックフラグを指定できます。 

このフラグは、KSCAMERA\_EXTENDEDPROP\_VIDEOのフラグ\_MANUAL と組み合わせることはできません。

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
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |(サポートされているビデオ処理モード)</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>現在のビデオ処理モード。</td>
</tr>
</tbody>
</table>

 

公開モードが以前に設定されていない場合、ドライバーは KSCAMERA\_EXTENDEDPROP に**フラグ**を設定し、[自動] (既定) を\_\_ます。 [**KSCAMERA\_extendedprop\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の後にある[**KSCAMERA\_extendedprop prop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)のメンバーは、処理モードの要件に従って設定されます。

モードが KSCAMERA\_EXTENDEDPROP\_VIDEOPROP フラグ\_AUTO の場合、 **u)** 値には現在の露出設定が含まれている必要があります。

### <a name="setting-the-property"></a>プロパティの設定

プロパティが設定されている場合、KSK プロパティ\_TYPE\_SET 要求では、 [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)の**Flags**メンバーに設定する露出モードが含まれます。 **フラグ**に KSCAMERA\_extendedprop\_videoproc フラグ\_AUTO モードフラグが含まれている場合は、 [ **\_extendedprop\_videoproc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting) **値**のメンバーを無視する必要があります。

## <a name="requirements"></a>要件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr>
<td><p>バージョン</p></td>
<td><p>Windows 8.1 以降で使用できます。</p></td>
</tr>
<tr>
<td><p>Header</p></td>
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[KSCAMERA\_EXTENDEDPROP\_ヘッダー](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[KSCAMERA\_EXTENDEDPROP\_VIDEOの設定](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)
