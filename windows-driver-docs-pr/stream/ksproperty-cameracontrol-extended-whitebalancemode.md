---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_WHITEBALANCEMODE
description: ホワイト バランス モード プロパティは、ホワイト バランスが発生したかどうかを自動的に処理または手動の温度の値が代わりに使用を指定します。
ms.assetid: 5DEC4A56-3868-40AF-9FD0-CDB0637B875A
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_WHITEBALANCEMODE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_WHITEBALANCEMODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 03ec84ea1d613ae1be4f620ebe67856630cf784a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529541"
---
# <a name="kspropertycameracontrolextendedwhitebalancemode"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_WHITEBALANCEMODE

ホワイト バランス モード プロパティは、ホワイト バランスが発生したかどうかを自動的に処理または手動の温度の値が代わりに使用を指定します。

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

プロパティの値 (データの操作) が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造と[ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)構造体。

プロパティの合計データ サイズが**sizeof**(KSCAMERA\_EXTENDEDPROP\_ヘッダー) + **sizeof**(KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING). **サイズ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)はこのプロパティの合計データ サイズに設定します。

**機能**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)次の 1 つ以上のビット演算 OR の組み合わせが含まれていますビデオの処理オプション。

| 処理モード                               | 説明                                                                  |
|-----------------------------------------------|------------------------------------------------------------------------------|
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_自動   | カメラのドライバーでは、ビデオを独自の処理ロジックを使用します。                       |
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手動 | カメラのドライバーでは、事前設定された処理メソッドまたはベース温度メソッドを使用します。 |
| KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロック   | 現在のビデオの処理方法がロックされています。                               |

**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)カメラ現在設定されているビデオ処理フラグが含まれています。 KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_KSCAMERA で自動設定を組み合わせることができます\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロックします。

このプロパティのコントロールは、非同期およびないキャンセル可能なは。

## <a name="remarks"></a>注釈

### <a name="processing-modes"></a>処理モード

<span id="KSCAMERA_EXTENDEDPROP_VIDEOPROCFLAG_AUTO"></span><span id="kscamera_extendedprop_videoprocflag_auto"></span>KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO  
これは、自動処理がサポートされていることを示します。 ドライバーでは、その内部ロジックを使用して、ビデオの処理を最適化します。 KSPROPERTY の\_型\_GET 要求、 **VideoProc**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)ビデオの処理の現在のドライバーの特定値を含める必要があります。 ホワイト バランスでは、場合は現在の気温ケルビンで含める必要があります。 **モード**自動操作のメンバーは無視されます。

このフラグは、KSCAMERA と組み合わせることも\_EXTENDEDPROP\_VIDEOPROCFLAG\_ビットごとの OR 値としてロックします。 ロックされると、カメラのドライバーの想定される動作は、ホワイト バランスで収束し、ロックを試みていない自動ホワイト バランス、もう一度新しいホワイト バランス コマンドが受信されるまで、集約型の値にホワイト バランス値には。

Auto モードの場合は、結合することがなく、ロックが既にロックされているコントロールとして扱う no-op カメラ ドライバーによって。 Auto モードの場合と組み合わせて、ロックが既にロックされているコントロールでは新しい収束が開始する必要があります。

**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_手動**  
-   手動では、このビデオの処理の特定の値を指定することを示します。 ホワイト バランスの場合は場合、**モード**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting) KSCAMERAをことを示します。\_EXTENDEDPROP\_ホワイト バランス\_、温度、 **VideoProc.Value.ul**ケルビンで温度値が含まれます。

**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロック**
-   ロックのオプション フラグは、現在のビデオの処理がどのような値は、現在プログラムにロックされていることを示します。 たとえば、特定ホワイト バランスを決定するまで、アプリケーションの auto モードが要求する、同じホワイト バランス設定を含むすべての写真のシーケンスを実行するアプリケーションがその時点で決定されます。 このような場合は、アプリケーションが、KSCAMERA を指定できます\_EXTENDEDPROP\_VIDEOPROCFLAG\_ロック フラグ。 カメラのドライバーはホワイト バランスについては、別の写真の間で変わらないことを確認します。

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
<td>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL |(ビデオ処理モードがサポートされています)</td>
</tr>
<tr class="even">
<td>フラグ</td>
<td>現在のビデオの処理モードです。</td>
</tr>
</tbody>
</table>

ホワイト バランス モードが既に設定されていない場合のドライバー設定**フラグ**KSCAMERA に\_EXTENDEDPROP\_VIDEOPROCFLAG\_自動 (既定値)。 メンバー、 [ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)に続く構造[ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)処理モードの要件に従って設定されます。

### <a name="setting-the-property"></a>プロパティの設定

設定すると、プロパティを KSPROPERTY\_型\_セットの要求、**フラグ**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)を設定するホワイト バランス モードにが含まれます。 **VideoProc.Value**のメンバー [ **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)ときに無視する必要があります**フラグ** 、KSCAMERA を含む\_EXTENDEDPROP\_VIDEOPROCFLAG\_AUTO モードのフラグ。

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

[**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)

[**KSPROPERTY\_CAMERACONTROL\_拡張\_EXPOSUREMODE**](ksproperty-cameracontrol-extended-exposuremode.md)
