---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_EXPOSUREMODE
description: 危険度のコントロール プロパティには、消失が発生したかどうかを自動的に処理または手動の時刻の値が代わりに使用を指定します。
ms.assetid: 54D4F286-09F2-48B5-9A7A-9445999972BD
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_EXPOSUREMODE ストリーミング メディア デバイス
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
ms.openlocfilehash: a97b0c7f78410b114009cff50958d4d3f458fd18
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348040"
---
# <a name="kspropertycameracontrolextendedexposuremode"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_EXPOSUREMODE

危険度のコントロール プロパティには、消失が発生したかどうかを自動的に処理または手動の時刻の値が代わりに使用を指定します。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| 取得 | 設定 | 対象 | プロパティ記述子の型 | プロパティ値の型 |
|---|---|---|---|---|
| 〇 | 〇 | フィルター | [**KSPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier) | [**KSCAMERA_EXTENDEDPROP_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) |

プロパティの値 (データの操作) が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と[ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)構造体。

プロパティの合計データ サイズが**sizeof**(KSCAMERA\_EXTENDEDPROP\_ヘッダー) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING). **サイズ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)はこのプロパティの合計データ サイズに設定します。

**機能**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)次の 1 つ以上のビット演算 OR の組み合わせが含まれていますビデオの処理オプション。

| 処理モード                               | 説明                                                                  |
|-----------------------------------------------|------------------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自動   | カメラのドライバーでは、ビデオを独自の処理ロジックを使用します。                       |
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手動 | カメラのドライバーでは、事前設定された処理メソッドを使用します。                               |
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロック   | 現在のビデオの処理方法がロックされています。                               |

 

**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)カメラ現在設定されているビデオ処理フラグが含まれています。 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_KSCAMERA で自動設定を組み合わせることができます\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロックします。

このプロパティのコントロールは、非同期とキャンセル可能なは。

## <a name="remarks"></a>注釈

### <a name="processing-modes"></a>処理モード

<span id="KSCAMERA_EXTENDEDPROP_VIDEOPROCFLAG_AUTO"></span><span id="kscamera_extendedprop_videoprocflag_auto"></span>KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO  
これは、自動処理がサポートされていることを示します。 ドライバーでは、その内部ロジックを使用して、ビデオの処理を最適化します。 KSPROPERTY の\_型\_GET 要求、 **VideoProc**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)ビデオの処理の現在のドライバーの特定値を含める必要があります。

このフラグは、KSCAMERA と組み合わせることも\_EXTENDEDPROP\_VIDEOPROCFLAG\_ビットごとの OR 値としてロックします。

Auto モードの場合は、結合することがなく、ロックが既にロックされているコントロールとして扱う no-op カメラ ドライバーによって。 Auto モードの場合と組み合わせて、ロックが既にロックされているコントロールでは新しい収束が開始する必要があります。

このフラグは、KSCAMERA と組み合わせることはない\_EXTENDEDPROP\_VIDEOPROCFLAG\_手動です。

<span id="KSCAMERA_EXTENDEDPROP_VIDEOPROCFLAG_MANUAL"></span><span id="kscamera_extendedprop_videoprocflag_manual"></span>KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手動  
手動では、このビデオの処理の特定の値を指定することを示します。 特定の値は、ドライバーに提供されます。

このフラグは、KSCAMERA と組み合わせることはできません\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO または KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロックします。

<span id="KSCAMERA_EXTENDEDPROP_VIDEOPROCFLAG_LOCK"></span><span id="kscamera_extendedprop_videoprocflag_lock"></span>KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロック  
ロックのオプション フラグは、現在のビデオの処理がどのような値は、現在プログラムにロックされていることを示します。 たとえば、アプリケーションは、特定の露出を決定するまで、auto モードを要求可能性があります。 その時点で、アプリケーションは、露出が同じですべての写真のシーケンスを決定します。 このような場合は、アプリケーションが、KSCAMERA を指定できます\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロック フラグ。 

このフラグは、KSCAMERA と組み合わせることはない\_EXTENDEDPROP\_VIDEOPROCFLAG\_手動です。

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
<td><p>sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING)</p></td>
</tr>
<tr class="even">
<td>結果</td>
<td>0</td>
</tr>
<tr class="odd">
<td>機能</td>
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |(ビデオ処理モードがサポートされています)</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>現在のビデオの処理モードです。</td>
</tr>
</tbody>
</table>

 

設定できる露出モードが既に設定されていない場合、ドライバー**フラグ**KSCAMERA に\_EXTENDEDPROP\_VIDEOPROCFLAG\_自動 (既定値)。 メンバー、 [ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)に続く構造[ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)処理モードの要件に従って設定されます。

**VideoProp.Value.ull** KSCAMERA モードの場合、値が現在の危険度の設定を含める必要があります\_EXTENDEDPROP\_VIDEOPROCFLAG\_自動。

### <a name="setting-the-property"></a>プロパティの設定

設定すると、プロパティを KSPROPERTY\_型\_セットの要求、**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)設定に露出モードにが含まれます。 **VideoProc.Value**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)ときに無視する必要があります**フラグ** 、KSCAMERA を含む\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO モードのフラグ。

## <a name="requirements"></a>要件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr>
<td><p>バージョン</p></td>
<td><p>Windows 8.1 以降を利用できます。</p></td>
</tr>
<tr>
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[KSCAMERA\_EXTENDEDPROP\_ヘッダー](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)
