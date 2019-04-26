---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_VIDEOSTABILIZATION
description: この拡張プロパティのコントロールは、ドライバーでのデジタル ビデオ安定化の制御に使用されます\\MFT0 します。
ms.assetid: 60F7D1B2-02F1-459A-8F6A-FC61D65705E1
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOSTABILIZATION ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOSTABILIZATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: e9564f4d5bf27437b18ca386db43b636618b83df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341878"
---
# <a name="kspropertycameracontrolextendedvideostabilization"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_VIDEOSTABILIZATION

この拡張プロパティのコントロールは、ドライバーでのデジタル ビデオ安定化の制御に使用されます\\MFT0 します。

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
<td><p>Pin</p></td>
<td><p>同期</p></td>
</tr>
</tbody>
</table>

次のフラグ、KSCAMERA 内に配置できる\_EXTENDEDPROP\_ヘッダー。フラグは、ドライバーでのデジタル ビデオ安定化を制御するフラグをフィールド\\MFT0 します。 既定では、ドライバーはビデオ安定化をが必要です。

```cpp
#define KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_OFF       0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_ON        0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_AUTO      0x0000000000000002
```

ドライバーがデジタル ビデオ安定化をサポートしていない場合、ドライバーはこのコントロールを実装しないでください。

VIDEOSTABILIZATION をサポートする必要があります、ドライバーは、このコントロールをサポートする場合\_ON\\OFF。

このコントロールの設定の呼び出しも何も起こりませんビデオの暗証番号 (pin) が、状態、KSSTATE よりも高い\_停止状態です。 ドライバーはビデオ ピンが停止状態でないとステータスを返す場合の受信設定の呼び出し元に戻す\_無効な\_デバイス\_状態。 ドライバーは、GET 呼び出しで、フラグ フィールドの現在の設定を返す必要があります。

このコントロールは、プロファイルのコンテキストで使用するプロファイルは、品質モードのドライバーにヒントとして機能します。 ドライバーは、ビデオ会議、または高品質のビデオ記録ビデオ安定化を有効にする基に、プロファイルを選択すると、たとえば、低待機時間または高品質を最適化するかどうかを判断できます。

> [!NOTE]
> PROPSETID\_しました\_CAMERACONTROL\_ビデオ\_安定化は、Windows 10 で非推奨になります。

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
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_OFF</p></td>
<td><p>これは、必須の機能です。 指定した場合、driver\MFT0 でデジタル ビデオ安定化は無効です。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_ON</p></td>
<td><p>これは、必須の機能です。 Driver\MFT0 でデジタル ビデオ安定化が有効になっている指定した場合、および padding 設定既定オーバーがドライバーの責任です。 このフラグは、自動と OFF のフラグで相互に排他的です。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_AUTO</p></td>
<td><p>この機能は省略可能です。 指定した場合、ビデオ安定化を実行するかどうかと、シーンの分析とキャプチャのシナリオに基づいて、どの程度の安定化を適用するこのような機能をサポートしているドライバーが決まります。 このフラグは、ON、OFF のフラグで相互に排他的です。</p></td>
</tr>
</tbody>
</table>

> [!NOTE]
> 実装によって overscanned バッファーが割り当てられ、ドライバーによって内部的に、またはパイプラインによって。

Overscanned バッファーをドライバーによって割り当てられる場合は、ドライバーは定期的なメディアの種類し、overscanned メディアの種類の両方を提供する必要があります。 MFT0 には、定期的なメディアの種類を提供する必要があります。 MFT0 の出力メディアの種類の定期的なメディアの種類を設定したときに、MFT0 が対応する overscanned メディアを選択します。 ビデオ安定化が有効な場合、ドライバーからの型がその入力メディアの種類としてメディアの種類を提供します。 ビデオ安定化をオフにすると、MFT0 は入力メディアの種類として定期的なメディアの種類を選択する必要があります。 MF を返す必要があります、MFT0\_E\_INVALIDMEDIATYPE overscanned メディアの種類の場合は、ビデオ安定化をオンにするとメディアの種類を出力として設定されます。

Overscanned バッファーが、ドライバーによって割り当てられている場合、ドライバーと MFT0 は定期的なメディアの種類を提供する必要があります。 MFT0 は、両方の入力メディアの種類の定期的なメディアの種類を設定し、メディアの種類を出力する必要があります。

影響でビデオ安定化 (つまり、ビデオ安定化ドライバーも MFT0 完了) をサポートするために、ドライバーと MFT0 する必要がありますさらにアドバタイズ overscanned メディアの種類に関係なく。 この場合、両方の正規表現と overscanned メディアの種類は、ドライバーと MFT0 によって公開されます。 次の規則ベースの効果とドライバーの両方を確実に適用されます\\ベース MFT0 ビデオ安定化が正常に動作します。

-   ドライバーの中に MFT0 出力メディアの種類として、overscanned メディアの種類が設定されている場合\\ベース MFT0 ビデオ安定化は、MF を返す必要があります MFT0\_E\_INVALIDMEDIATYPE。

-   MFT0 出力メディアの種類として、定期的なメディアの種類を設定すると、アプリのベースの効果のビデオ安定化 overscanned メディアの種類を受け取ることができるベースのビデオ安定化に効果を有効にする試行でエラーを返します。

次の表には、説明と要件が含まれています、 [KSCAMERA\_EXTENDEDPROP\_ヘッダー](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)ビデオ安定化コントロールを使用する場合は、フィールドを構造体します。

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
<td><p>必要がある、暗証番号 (pin) の ID に関連付けられているビデオ ピン留めします。</p></td>
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
<td><p>定義したように、サポートされている KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_XXX フラグのビットごとの OR があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 上記で定義された KSCAMERA_EXTENDEDPROP_VIDEOSTABILIZATION_XXX フラグのいずれかにできます。</p></td>
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
