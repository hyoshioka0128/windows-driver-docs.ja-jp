---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_SCENEMODE
description: KSPROPERTY\_CAMERACONTROL\_拡張\_SCENEMODE プロパティ ID、KSPROPERTY で定義されている\_CAMERACONTROL\_拡張\_プロパティ列挙の Oem を提供します。正常に機能は、必要に応じてその他の ISP コントロール パラメーターと共に、シーンのモードを調整します。
ms.assetid: CB3F89AD-4B53-4E47-B60E-4B584DB8418B
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
ms.openlocfilehash: 99423671db7424201da693f6c671a439c76a2a04
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530255"
---
# <a name="kspropertycameracontrolextendedscenemode"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_SCENEMODE

**KSPROPERTY\_CAMERACONTROL\_拡張\_SCENEMODE**で定義されているプロパティ ID、 [ **KSPROPERTY\_CAMERACONTROL\_拡張\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/dn917962)列挙体は Oem に細かく調整機能を他の ISP 制御パラメーターと共にシーン モードに応じて。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Scope</th>
<th>コントロール</th>
<th>種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バージョン 1</p></td>
<td><p>フィルター</p></td>
<td><p>非同期</p></td>
</tr>
</tbody>
</table>

シーン モードは、特定の操作を最適化するためにカメラ システム ガイドへのヒントを条件として使用されます。 シーンのモードとホワイト バランスでは、ISO などの他の ISP コントロールの露出時間、および EV 補正を互いに影響を与えることがなく独立して動作することにある必要があります。

-   その他の ISP コントロール パラメーターを変更する既存のシーン モードを変更する必要があります。 ドライバーは、その他の ISP パラメーターを変更した後、シーンのモードを手動に変更する必要はありません。

-   自動シーン モードの設定は、その他のコントロールの ISP の既存の設定を変更することではできません。 ドライバーでは、その他の ISP のコントロールの完全な自動モードに戻すには必要ありません。

**KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_AUTO**

このフラグは、auto モードのシーンを示します。 カメラのドライバーは自動的にシーンに基づいて最適なシーン モード設定を確認し、シーンの必要に応じて、さまざまな ISP の設定を最適化します。

**KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_手動**

このフラグは適用されません。

**KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_MACRO\\PORTRAIT\\SPORT\\SNOW\\NIGHT\\BEACH\\SUNSET\\CANDLELIGHT\\LANDSCAPE\\NIGHTPORTRAIT\\BACKLIT**

これらのフラグは、定義されている、対応するシーン モードを示します。 カメラのドライバーは、必要に応じて、さまざまな ISP の設定を最適化するためにヒントとして指定されたシーン モードを使用 (たとえば、夜の ISP の設定は環境に最適な夜時間)。

次の表には、説明と要件が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)フィールドを構造体を使用する場合、 **KSPROPERTY\_CAMERACONTROL\_拡張\_SCENEMODE**プロパティ。 [ **KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)の構造は無視されます**KSPROPERTY\_CAMERACONTROL\_拡張\_SCENEMODE**します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メンバー</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>これは、1 でなければなりません。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>これでなければなりません<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0 xffffffff) です。</p></td>
</tr>
<tr class="odd">
<td><p>サイズ</p></td>
<td><p>Sizeof 必要があります (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<strong>KSCAMERA_EXTENDEDPROP_VALUE</strong>)。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>これは、最後の設定操作のエラーの結果を示します。 設定操作が行われていない場合は必ず 0。 値 0 は、エラーが検出されなかったことを示します。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>ビットごとの OR の必要があります<strong>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL</strong>および上記で定義された、サポートされているシーン モードのいずれか。 <strong>KSCAMERA_EXTENDEDPROP_SCENEMODE_AUTO</strong>カメラのドライバーは、このコントロールをサポートしている場合にサポートする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>前に示した、サポートされているシーン モードのいずれかを指定できます。</p></td>
</tr>
</tbody>
</table>

## <a name="requirements"></a>要件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
