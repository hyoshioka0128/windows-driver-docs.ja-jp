---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_OPTIMIZATIONHINT
description: KSPROPERTY\_CAMERACONTROL\_拡張\_OPTIMIZATIONHINT はビデオ キャプチャと写真をキャプチャの基本的なユース ケースを制御するために使用します。 Windows 10 では、このコントロールは、拡張されたハードウェアの最適化ヒントをサポートするために拡張されます。
ms.assetid: 1E2787B7-4BC2-4FBC-8909-ACB122B87F08
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: c50d0281f1136be2d273ebc736f1b35b305a87f6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357009"
---
# <a name="kspropertycameracontrolextendedoptimizationhint"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_OPTIMIZATIONHINT

KSPROPERTY\_CAMERACONTROL\_拡張\_OPTIMIZATIONHINT はビデオ キャプチャと写真をキャプチャの基本的なユース ケースを制御するために使用します。 Windows 10 では、このコントロールは、拡張されたハードウェアの最適化ヒントをサポートするために拡張されます。

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

次のフラグは、KSCAMERA に配置できる\_EXTENDEDPROP\_ヘッダー。ドライバーのハードウェアの最適化ヒントを flags フィールドです。

基本的なユース ケースを指定するために、写真とビデオのヒントを続けます。

Windows 10 では、追加のビット フラグは、品質、速度、およびドライバーの電力消費量のバランスを支援します。 既定では、ドライバーが KSCAMERA\_EXTENDEDPROP\_最適化\_写真。

```cpp
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_DEFAULT      0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_PHOTO        0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_VIDEO        0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_QUALITY      0x0000000000000004
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_LATENCY      0x0000000000000008
#define KSCAMERA_EXTENDEDPROP_OPTIMIZATION_POWER        0x0000000000000010
```

f、ドライバーは、このコントロールをサポートしている、KSCAMERA をサポートする必要があります\_EXTENDEDPROP\_最適化\_写真と KSCAMERA\_EXTENDEDPROP\_最適化\_ビデオ。

ドライバーが最適化ヒントをサポートしていない場合、ドライバーはこのコントロールを実装しないでください。

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
<td><p>KSCAMERA_EXTENDEDPROP_OPTIMIZATION_DEFAULT</p></td>
<td><p>これは、必須の機能です。 指定した場合、ドライバーする必要があります以前のヒントをオフ ドライバーの設定し、ドライバーの既定の電源、品質、待機時間のトレードオフを適用します。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_OPTIMIZATION_PHOTO</p></td>
<td><p>これは、必須の機能です。 指定すると、基本的なユース ケースが写真をキャプチャし、ドライバーは、ビデオ記録をより、写真をキャプチャを優先するものとします。 プレビューの暗証番号 (pin) のビデオのみを記録中に、写真の品質を優先してセンサー モードを選択して、停止状態または写真をキャプチャの実行中の状態には、ときに、このフラグを指定できます。 写真撮影のビデオ記録中に指定した場合、ビデオ ストリームの不具合は写真の品質が向上を優先して許容です。 このフラグは、ビデオのフラグで相互に排他的では、いずれか 1 つまたは 2 つの品質、待機時間、および電源フラグで使用できます。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_OPTIMIZATION_VIDEO</p></td>
<td><p>これは、必須の機能です。 基本的なユース ケースがビデオ キャプチャには、指定した場合と、ドライバーでは、ビデオ、写真をキャプチャを記録、優先順位を設定します。 プレビューの暗証番号 (pin) のビデオのみを記録中にビデオ記録、優先センサー モードを選択して、停止状態または写真をキャプチャの実行中の状態には、ときに、このフラグを指定できます。 写真撮影のビデオ記録中に指定した場合、ビデオ ストリームに不具合が許可されていません。 このフラグは、写真のフラグで相互に排他的では、いずれか 1 つまたは 2 つの品質、待機時間、および電源フラグで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_OPTIMIZATION_QUALITY</p></td>
<td><p>この機能は省略可能です。 指定した場合、ドライバーでは、写真をキャプチャの画像の品質とビデオのビデオ記録の品質を最適化します。 写真をキャプチャ (履歴のフレームを使用せず、通常の写真、VP、PS をなど) やビデオ記録を開始する前に、または、暗証番号 (pin) が停止状態の場合、このフラグを指定できます。 写真のフラグ、またはビデオ フラグと共に待機時間または電源のフラグは、このフラグを使用できます。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_OPTIMIZATION_LATENCY</p></td>
<td><p>この機能は省略可能です。 指定した場合、ドライバーでは、速度と、写真をキャプチャし、ビデオ記録の待機時間を最適化します。 (履歴のフレームを使用せず、通常の写真、VP、PS をなど)、写真をキャプチャする前にこのフラグを指定することができますやビデオ記録の開始、または pin が停止状態にします。 写真のフラグ、またはビデオ フラグと共に品質または電源のフラグは、このフラグを使用できます。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_OPTIMIZATION_POWER</p></td>
<td><p>この機能は省略可能です。 指定した場合、ドライバーは、写真をキャプチャし、ビデオ記録の電力消費を最適化します。 写真をキャプチャ (履歴がない、通常の写真、VP、PS をなど) やビデオ記録を開始する前に、または、暗証番号 (pin) が停止状態の場合、このフラグを指定できます。 このフラグは、ビデオ フラグと共に、品質や待機時間のフラグで使用できます。</p></td>
</tr>
</tbody>
</table>

次の表には、説明と要件が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)コントロールを使用する場合は、フィールドを構造体します。

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
<td><p>これは、1 でなければなりません。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0 xffffffff) 必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>サイズ</p></td>
<td><p>これは、sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VALUE) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>最後の設定操作のエラーの結果を示します。 設定操作が行われていない場合は必ず 0。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>上記に定義されているサポートされている KSCAMERA_EXTENDEDPROP_OPTIMIZATION_ * フラグのビットごとの OR をする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 これは、サポートされている KSCAMERA_EXTENDEDPROP_OPTIMIZATION_ * フラグの上で定義した任意の有効な組み合わせを指定できます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>注釈

最適化ヒントを使用する場合は、次の項目に注意してください。

-   品質/待機時間/電源と写真とビデオは、独立したヒントの 2 つのセットです。 同時に、または別の時刻に個別にまとめて指定することができます。 品質/待機時間/電源設定は、写真とビデオ、またはその逆は上書きされません。 別の時刻に指定した場合、ドライバーは、GET 呼び出しでヒントの両方のセットの現在の設定を返す必要があります。

-   品質/待機時間/電源のヒントが設定されている場合、ドライバーをその制約内で最適化する必要があります。 最適化が使用できない場合、ドライバーは、ヒントを無視する必要があります。

-   2 つのヒントを指定するには、ビデオのユース ケースと同時に、1 つだけのヒントが指定されている場合よりも小さいを各ヒントの最適化にあります。 具体的な機能は次のとおりです。

    -   待機時間は品質または電源に優先される品質または電源が指定されても時にします。 このような場合より小さいとのみ品質を指定すると、電力消費量が唯一の電源が指定されている場合よりも高い可能性があります、品質可能性があります。

    -   品質と電源の両方を指定するより小さいとのみ品質を指定すると、電力消費量が唯一の電源が指定されている場合よりも高い可能性があります、品質可能性があります。

-   最適化ヒントは 3A、ISP の処理、センサーの選択など、アプリケーションで指定されたキャプチャのシナリオの制約内での処理のトレードオフを容易にドライバーにヒントとしてのみ提供されます。 アプリ開発者を選択し、最適な結果を実現するために、最も適切な制御と、特定のキャプチャのシナリオ用の Api を構成するために重要です。 それ以外の場合、単独での最適化ヒントには、低下の影響があります。 たとえば、高品質な写真をキャプチャ、VP または LowLagPhoto/TakePhoto を使用する必要があります代わりに、品質を使用するために特定の IHV プラットフォームで PS のヒントです。 同様に、ビデオ安定化より低待機時間または電源の消費量が必要な場合は無効にする必要があります。

-   最適化ヒントは、各機能フラグで指定されているもの以外の時間/状態で受信した場合に無視されるものとします。

ビデオ安定化コントロールも有効な場合 (ON または自動) ドライバーで。

-   ドライバーには、最も積極的なビデオ安定化低待機時間や待機時間や電力のヒントが設定されている場合は、処理の待機時間や電源消費量を削減する低電力ビデオ安定化アルゴリズムを含むが適用されます。 ビデオ安定化が AUTO に設定されている場合、ドライバー、待機時間や電力の消費量を軽減するために、ビデオ安定化をオフにします。

-   ドライバーには、品質のヒントが設定されている場合は、ビデオの品質を向上させるために最も高いアグレッシブなビデオ安定が適用されます。


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
