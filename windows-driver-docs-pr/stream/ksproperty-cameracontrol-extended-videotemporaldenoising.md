---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_VIDEOTEMPORALDENOISING
description: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_VIDEOTEMPORALDENOISING は、ドライバーのビデオテンポラル Denoising を制御するために使用されます。
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOTEMPORALDENOISING ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOTEMPORALDENOISING
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 04/03/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 33321a84ffccf3d78e597be7e364e66fa72cd302
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837849"
---
# <a name="ksproperty_cameracontrol_extended_videotemporaldenoising"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_VIDEOTEMPORALDENOISING

KSK プロパティ\_CAMERACONTROL\_EXTENDED\_VIDEOTEMPORALDENOISING は、ドライバーのビデオテンポラル Denoising を制御するために使用されます。

## <a name="overview"></a>概要

カメラシステムを最適でない状態で運用する場合、イメージ信号プロセッサ (ISP) の3A 統計ロジックでは、カメラシステムの光感度を向上させて、photons が発生していないことを補うために、アナログとデジタルのゲインが向上する傾向があります。適用されたキャプチャフレームレートでのセンサー。 これは、センサーによって生成されたフレームの知覚ノイズが増加する増幅させるショットノイズの副作用です。 これは、ISP パイプラインを介して処理された後でも明らかになる可能性があります。

彩度とルミナンスの aberrations を使用してシーンのイメージを変更すること以外に、このショットのノイズのストキャスティクスの性質により、ピクセル値の一時的な一貫性は特にビデオ (プレビューまたは記録) で顕著になり、ユーザーにとって悪いエクスペリエンスにつながる可能性があります。

Video テンポラル Denoising (VTD) の目的は、複数のフレームからの情報を累積して結合し、フレームの待機時間が制限されたコンテキストでクリーン出力フレームを生成することにより、ノイズを解消し、ノイズピクセルの一時的な一貫性を減らすことです。ビデオソースを使用する場合などに重要です。

この追加の処理は、ユーザーが通常どおりにカメラを操作できないようにし、後処理の手順を必要とすることなく、イメージの品質を向上させることで、リアルタイムの方法で実行することを意図しています。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| 適用範囲 | コントロール | タスクバーの検索ボックスに |
| --- | --- | --- |
| バージョン 1 | フィルター | 同期 |

次に示すのは、KSCAMERA\_EXTENDEDPROP\_ヘッダーに配置できるフラグです。ドライバー上のビデオテンポラル Denoising を制御するフラグフィールド。

```cpp
#define KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO   0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_OFF    0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ON     0x0000000000000004
```

ドライバーがこのコントロールをサポートしている場合は、VIDEOTEMPORALDENOISING_AUTO または VIDEOTEMPORALDENOISING_ON と VIDEOTEMPORALDENOISING_OFF の両方をサポートしている必要があります。

ドライバーが Video テンポラル Denoising をサポートしていない場合、ドライバーはこのコントロールを実装しません。

これは、サポートされているすべての pin からのストリーミング中に動的に制御できる同期コントロールです。  

次の表では、フラグ機能について説明します。

| Flag | 説明 |
| --- | --- |
| KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO | KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_OFF と KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ON がサポートされていない場合、これは必須の機能です。 指定した場合、Video テンポラル Denoising はドライバーで自動的に有効または無効になり、表示される光の中でサポートされているすべてのピンストリーミングピクセルに影響します。 これは、常にフレームを実際に処理することを保証するものではありませんが、これは、ISP を通過するビデオ信号によって、実装者の discretions で実行されることを意味します。 |
| KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_OFF | これは、KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO がサポートされていない場合は必須の機能であり、存在する場合は省略可能です。 指定した場合、ビデオのテンポラル Denoising は、表示されている光の中でサポートされているすべてのピンストリーミングピクセルに対して、常にドライバーで無効になります。 |
| KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ON | これは、KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO がサポートされていない場合は必須の機能であり、存在する場合は省略可能です。 指定した場合、ビデオのテンポラル Denoising は、表示されている光の中でサポートされているすべてのピンストリーミングピクセルに対して、常にドライバーで有効になります。 |

次の表には、コントロールを使用する場合の[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造のフィールドの説明と要件が含まれています。

| メンバー | 説明 |
| --- | --- |
| バージョン | 1にする必要があります。 |
| PinId | KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF) である必要があります。 |
| Size | Sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE) である必要があります。 |
| 結果 | 最後の設定操作のエラー結果を示します。  設定操作が行われていない場合は、0にする必要があります。 |
| 機能 | は、上で定義された、サポートされている KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ * フラグのビットごとの OR である必要があります。 |
| フラグ | これは、読み取り/書き込みフィールドです。  これは、上記で定義されている KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_XXX フラグのいずれかである必要があります。 これらのフラグは相互に排他的であり、ビットごとの OR の組み合わせで設定することはできません。 |

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
