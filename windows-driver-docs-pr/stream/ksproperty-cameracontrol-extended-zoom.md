---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_ズーム
description: KSPROPERTY\_CAMERACONTROL\_拡張\_ズームは、デジタルのズームの制御に使用されます。
ms.assetid: 93CFCBFC-69B3-4241-913F-94615599BE8E
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ZOOM ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ZOOM
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: a6a7542eea0b46d974f6d7afe89ebb3fba9c44a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356649"
---
# <a name="kspropertycameracontrolextendedzoom"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_ズーム

**KSPROPERTY\_CAMERACONTROL\_拡張\_ズーム**デジタル ズームを制御するために使用します。 定義されている、 [ **KSPROPERTY\_CAMERACONTROL\_拡張\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)列挙型を取得およびズームの比率を設定からズーム範囲を取得するために使用し、ドライバー。 Windows 10 で、このコントロールは、サポート、滑らかに拡大もに拡張されます。

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
<td><p>同期</p></td>
</tr>
</tbody>
</table>

次のフラグを配置することができます、 **KSCAMERA\_EXTENDEDPROP\_ヘッダー。フラグ**フィールドを直接ズームとコントロール、滑らかに拡大します。 既定値は、ドライバーによって定義されます。

```cpp
#define KSCAMERA_EXTENDEDPROP_ZOOM_DEFAULT  0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_ZOOM_DIRECT   0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_ZOOM_SMOOTH   0x0000000000000002
```

ドライバーは、このコントロールをサポートする場合、サポートする必要があります**KSCAMERA\_EXTENDEDPROP\_ズーム\_既定**します。

ドライバーがデジタル ズームをサポートしていない場合、ドライバーはこのコントロールを実装しないでください。

次の表では、フラグの機能について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KSCAMERA_EXTENDEDPROP_ZOOM_DEFAULT</strong></p></td>
<td><p>これは、必須の機能です。 ドライバーが、直接のズーム設定または滑らかに拡大を適用するかどうかを決定指定した場合、し、それに応じて VideoProc.Value.ul で指定されたターゲットの倍率をズームします。 このフラグは、ダイレクトと SMOOTH フラグで相互に排他的です。</p></td>
</tr>
<tr class="even">
<td><p><strong>KSCAMERA_EXTENDEDPROP_ZOOM_DIRECT</strong></p></td>
<td><p>これは、必須の機能です。 指定した場合、ドライバーは、可能な限り早く VideoProc.Value.ul で指定されたターゲットの倍率をズームします。 このフラグは、自動と滑らかなフラグで相互に排他的です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>KSCAMERA_EXTENDEDPROP_ZOOM_SMOOTH</strong></p></td>
<td><p>この機能は省略可能です。 指定した場合、ドライバーは段階的には、滑らかな方法で、VideoProc.Value.ul で指定されたターゲットの倍率をズームします。 ドライバーはフレームが指定したズームの倍率に到達する数です。 このフラグは、自動と直接フラグで相互に排他的です。</p></td>
</tr>
</tbody>
</table>

各**取得**呼び出し、ドライバーの必要がありますレポートに現在のズームの範囲は許可されているに基づいて現在の構成またはセットアップします。

次の表には、説明と要件が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)フィールドを構造体を使用する場合、 **KSPROPERTY\_CAMERACONTROL\_拡張\_ズーム**プロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Member</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>これは、1、</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>これでなければなりません<strong>KSCAMERA_EXTENDEDPROP_FILTERSCOPE</strong> (0 xffffffff)</p></td>
</tr>
<tr class="odd">
<td><p>サイズ</p></td>
<td><p>Sizeof 必要があります (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)"><strong>KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING</strong></a>)、</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>これは、最後の設定操作のエラーの結果を示します。 設定操作が行われていない場合は必ず 0。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>上記で定義されたサポートされているフラグのビットごとの OR をする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 上記で定義された、サポートされているフラグのいずれかにできます。</p></td>
</tr>
</tbody>
</table>

次の表には、説明と要件が含まれています、 **KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**のフィールドを構造体、 **KSPROPERTY\_CAMERACONTROL\_拡張\_ズーム**プロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Member</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mode</p></td>
<td><p>これにより、使用されておらず、0 にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>最小/最大/ステップ</p></td>
<td><p>最小/最大/ステップには、最小/最大/の増分 Q16 形式でカメラのドライバーでサポートされるズームの比率が含まれています。 ドライバーは、これらの値を返す必要があります<strong>取得</strong>操作。</p></td>
</tr>
<tr class="odd">
<td><p>VideoProc</p></td>
<td><p><strong>設定</strong>操作、VideoProc.Value.ul は最小/最大/ステップ パラメーターによって示された範囲内でズーム比率を指定する必要があります。 <strong>取得</strong>操作、ドライバーは現在のズーム比を返す必要があります。</p></td>
</tr>
<tr class="even">
<td><p>予約済み</p></td>
<td><p>これは使用されません。 これは、ドライバーによって無視する必要があります。</p></td>
</tr>
</tbody>
</table>

このプロパティのコントロールは、同期およびないキャンセル可能なは。

## <a name="requirements"></a>必要条件

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
