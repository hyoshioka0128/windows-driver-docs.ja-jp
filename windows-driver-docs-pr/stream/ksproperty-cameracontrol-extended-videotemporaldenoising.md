---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_VIDEOTEMPORALDENOISING
description: KSPROPERTY\_CAMERACONTROL\_拡張\_VIDEOTEMPORALDENOISING はドライバーでビデオのテンポラル ノイズ除去の制御に使用します。
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOTEMPORALDENOISING ストリーミング メディア デバイス
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
ms.openlocfilehash: 2da1efe08dab339ed6e58d5f0a913685794e0638
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905429"
---
# <a name="kspropertycameracontrolextendedvideotemporaldenoising"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_VIDEOTEMPORALDENOISING

KSPROPERTY\_CAMERACONTROL\_拡張\_VIDEOTEMPORALDENOISING はドライバーでビデオのテンポラル ノイズ除去の制御に使用します。

## <a name="overview"></a>概要

イメージのシグナル プロセッサ (ISP) の 3 a 統計ロジックはヒット光子の欠落を補正するために、カメラのシステムのライトの機密度を向上させるアナログおよびデジタルのゲインを向上させる傾向がありますカメラのシステムの準最適な光の状態で、動作している場合、課されたキャプチャのフレーム レートでセンサーです。 増幅ショット ノイズ、センサーによって生成されたフレームの見かけ上のノイズが増加の側の効果があります。 これにも明らかな ISP パイプラインを通じて処理された後も。

確率的このショット ノイズ、性質があるため、値の彩度と輝度の問題とシーンの画像の変更以外は、テンポラル incoherence ピクセル値は (プレビューまたはレコード) のビデオでは特に顕著で、ユーザーの不適切な経験する可能性があります。

ノイズを解決し、ノイズの多いピクセルのテンポラル incoherence を蓄積され、時間の制約があるコンテキストでクリーナー出力フレームを生成するために複数のフレームからの情報を組み合わせることによって削減することが目的のビデオ テンポラルのノイズ除去 (VTD)、フレームの待機時間ビデオ ソースなどが重要です。

この追加の処理は、ユーザーは通常、カメラの運用をブロックすることがなく、処理後の手順を必要とせずに、イメージ品質を強化するために最小限の遅延がリアルタイムで実行されているもの。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| Scope | コントロール | 種類 |
| --- | --- | --- |
| バージョン 1 | フィルター | 同期 |

次に、KSCAMERA に配置できるフラグ\_EXTENDEDPROP\_ヘッダー。ドライバーのビデオのテンポラル ノイズ除去をコントロールにフィールドのフラグを設定します。

```cpp
#define KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO   0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_OFF    0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ON     0x0000000000000004
```

ドライバーは、このコントロールをサポートする場合 VIDEOTEMPORALDENOISING_AUTO または VIDEOTEMPORALDENOISING_ON と両方 VIDEOTEMPORALDENOISING_OFF 少なくともサポートを必要があります。

ドライバーがビデオのテンポラル ノイズ除去をサポートしていない場合、ドライバーはこのコントロールを実装しないでください。

これはサポートされているすべてのピンからストリーミング中に動的に制御できる同期コントロールです。  

次の表では、フラグの機能について説明します。

| Flag | 説明 |
| --- | --- |
| KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO | これは、KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_OFF と KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ON がサポートされていない場合に必須の機能です。 指定した場合、テンポラルのノイズ除去をビデオは自動的に有効または無効に、ドライバーと影響をすべてサポートされている pin の光の可視スペクトルのピクセルをストリーミングします。 時にすべてのフレームの実際の処理を保証するこれがない、中にこのため、実行者の discretions が ISP に渡されるビデオ信号を指定した位置がかかる場合があります。 |
| KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_OFF | これは、KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO がサポートされており、これは省略がない場合に必須の機能です。 指定した場合は、光の可視スペクトルのピクセルのストリーミングのサポートされているすべてのピンをすべて時に、ドライバーで無効になってはビデオ テンポラル ノイズ除去します。 |
| KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ON | これは、KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_AUTO がサポートされており、これは省略がない場合に必須の機能です。 指定した場合は、光の可視スペクトルのピクセルのストリーミングのサポートされているすべてのピンをすべて時に、ドライバーで有効ですテンポラルのノイズ除去をビデオ。 |

次の表には、説明と要件が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)コントロールを使用する場合は、フィールドを構造体します。

| Member | 説明 |
| --- | --- |
| バージョン | 1 にする必要があります。 |
| PinId | KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0 xffffffff) 必要があります。 |
| サイズ | Sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE) 必要があります。 |
| 結果 | 最後の設定操作のエラーの結果を示します。  設定操作が行われていない場合は必ず 0。 |
| 機能 | ビットごとの OR、サポートされている KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_ * フラグの上に定義されている必要があります。 |
| フラグ | これは、読み取り/書き込みフィールドです。  これは、上記で定義された KSCAMERA_EXTENDEDPROP_VIDEOTEMPORALDENOISING_XXX フラグのいずれかでなければなりません。 これらのフラグは相互に排他的で、ビットごとの OR の組み合わせで設定できませんに注意してください。 |

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
