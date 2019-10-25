---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_SCENEMODE
description: Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_SCENEMODE プロパティ ID\_で定義されている CAMERACONTROL\_拡張\_プロパティ列挙型の場合、Oem はシーンモードを微調整する機能を提供します。必要に応じて、その他の ISP コントロールパラメーターと共に使用します。
ms.assetid: CB3F89AD-4B53-4E47-B60E-4B584DB8418B
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
ms.openlocfilehash: 73795fac93c1b22ff4d8ea43df3a0ec100162ad2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823942"
---
# <a name="ksproperty_cameracontrol_extended_scenemode"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_SCENEMODE

Ksk プロパティ **\_CAMERACONTROL\_extended\_SCENEMODE**プロパティ ID に定義されています。この ID は、 [**CAMERACONTROL\_拡張\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)列挙型に\_定義されており、oem は必要に応じて、他の ISP コントロールパラメーターと共にシーンモードを微調整します。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>適用範囲</th>
<th>コントロール</th>
<th>タスクバーの検索ボックスに</th>
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

シーンモードは、特定の条件に対する操作を最適化するためにカメラシステムをガイドするヒントとして使用されます。 シーンモードおよびその他の ISP コントロール (白のバランス、ISO、露出時間、EV 補正など) は、互いに影響を与えることなく、独立して動作できる必要があります。

-   他の ISP コントロールパラメーターを変更しても、既存のシーンモードを変更することはできません。 他の ISP パラメーターを変更した後に、ドライバーはシーンモードを手動に変更する必要はありません。

-   自動シーンモードを設定しても、他の ISP コントロールの既存の設定を変更することはできません。 ドライバーは、他の ISP コントロールのフル自動モードに戻す必要はありません。

**KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_AUTO**

このフラグは、自動シーンモードを示します。 カメラドライバーは、シーンに基づいて最適なシーンモード設定を自動的に決定し、シーンに必要なさまざまな ISP 設定を最適化します。

**KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_MANUAL**

このフラグは適用できません。

**KSCAMERA\_EXTENDEDPROP\_SCENEMODE\_マクロ\\縦\\スポーツ\\雪\\夜\\ビーチ\\日没\\CANDLELIGHT\\横\\NIGHTPORTRAIT\\バック**

これらのフラグは、定義されているように、対応するシーンモードを示します。 カメラドライバーでは、必要に応じてさまざまな ISP 設定を最適化するためのヒントとして指定されているシーンモードが使用されます (たとえば、夜の場合、ISP の設定は夜の時間環境向けに最適化されています)。

次の表には、 **Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_SCENEMODE**プロパティを使用する場合の[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造のフィールドの説明と要件が含まれています。 [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)構造体は、 **KSK プロパティ\_CAMERACONTROL\_拡張\_SCENEMODE**に対しては無視されます。

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
<td><p>これは1である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>これは<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0xffffffff) である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>これは sizeof (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + Sizeof (<strong>KSCAMERA_EXTENDEDPROP_VALUE</strong>) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>これは、最後の設定操作のエラー結果を示します。 設定操作が行われていない場合は、0にする必要があります。 値0は、エラーが検出されなかったことを示します。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>これは、 <strong>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL</strong>のビットごとの or であるか、上で定義されているサポートされているシーンモードである必要があります。 カメラドライバーがこのコントロールをサポートしている場合は、 <strong>KSCAMERA_EXTENDEDPROP_SCENEMODE_AUTO</strong>をサポートする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、上記のサポートされているシーンモードのいずれかになります。</p></td>
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
