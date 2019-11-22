---
title: 状態遷移
description: 状態遷移
ms.assetid: c71fd395-28aa-4421-9443-b5b0a1f3ac7e
keywords:
- ビデオキャプチャ WDK AVStream、ストリームの状態
- ビデオのキャプチャ WDK AVStream、ストリームの状態
- ストリームの状態 WDK ビデオキャプチャ
- 状態 WDK ビデオキャプチャ
- 状態遷移 WDK ビデオキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b96de2b65d0760518b86a2cfba914bb7e7cdb82
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837695"
---
# <a name="state-transitions"></a>状態遷移


リソースが正常に割り当てられるようにするために、可能なカーネルストリームの状態遷移のサブセットのみを許可します。 次の表に、許可される遷移と、ストリームクラスミニドライバーがこのような遷移中に通常実行するタスクを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Transition</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>一時停止の停止</p></td>
<td><p>リソースを割り当てます。 <strong>KSSTATE_PAUSE</strong>への移行が完了すると、read SRBs がキューに登録されます。</p></td>
</tr>
<tr class="even">
<td><p>実行を一時停止する</p></td>
<td><p>ストリーミングを開始します。</p></td>
</tr>
<tr class="odd">
<td><p>実行して一時停止</p></td>
<td><p>ストリーミングを停止します。 未処理の read SRBs は、ミニドライバーによって保持されているキューに残ります。</p></td>
</tr>
<tr class="even">
<td><p>停止するまで一時停止</p></td>
<td><p>リソースの割り当てを解除し、すべての未処理の読み取り SRBs を完了します。 SRBs 構造体<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header" data-raw-source="[&lt;strong&gt;KSSTREAM_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)"><strong>KSSTREAM_HEADER</strong></a>の<strong>dataused</strong>メンバーでは、イメージが埋め込まれていないは、長さゼロで完了します。</p></td>
</tr>
</tbody>
</table>

 

**注**  : 遷移は、ksk 状態 **\_停止**状態に戻る前に、 **\_一時停止**と**ksk 状態\_実行**状態の間で複数回繰り返すことができます。 Video capture ミニドライバーは、次のような遷移を想定しています。

 

KSSTATE\_STOP-&gt; **ksstate\_**  -&gt; **KSK 状態\_一時停止** -&gt; **Ksstate\_実行** -&gt; **ksstate\_一時停止** -@no__% **\_実行** -&gt; **KSSTATE\_一時停止** -&gt; ksstate\_停止&gt;

ストリームが**Ksk 状態\_停止**状態にある場合、ミニドライバーは、未処理のすべてのデータ読み取り SRBs をすぐに完了する必要があります。

ストリーミング中にユーザーモードアプリケーションが予期せず終了する可能性があるため、すべてのストリームクラスミニドライバーは、いつでもストリームクラスインターフェイスから[ **\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-close-stream)要求を閉じて\_処理する必要があります。 ストリームクラスのインターフェイスは、SRB\_\_ストリームに閉じる前に、ミニドライバーの**HwCancelPacket**ルーチンを通じて未処理のすべてのバッファーをキャンセルします。 アプリケーションが終了する前に、ストリームの状態を Ksk 状態に設定することはできません **\_停止**することに注意してください。

[ **\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)、 [**ks\_VBI\_frame\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_vbi_frame_info)、または ksk[**プロパティ\_DROPPEDFRAMES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_droppedframes_current_s)\_の**PictureNumber**または**dropcount**のメンバーを更新しないでください。または、ksk 状態\_**PAUSE**から**KSPROPERTY\_run**または**ksproperty**\_から ksproperty\_pause に移行します。\_\_ 詳細については、「[ビデオのキャプチャ](capturing-video.md)」を参照してください。

 

 




