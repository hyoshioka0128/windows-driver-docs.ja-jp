---
title: 状態遷移
description: 状態遷移
ms.assetid: c71fd395-28aa-4421-9443-b5b0a1f3ac7e
keywords:
- WDK AVStream ビデオ キャプチャは、ストリームを状態します。
- ビデオの WDK AVStream をキャプチャするには、ストリームを状態します。
- ストリームの状態の WDK ビデオ キャプチャ
- WDK のビデオ キャプチャを状態します。
- 状態遷移の WDK ビデオ キャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b1eab63ea7ccb2ba0d0e70db81c9d704a7a8583
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377834"
---
# <a name="state-transitions"></a>状態遷移


所定のリソース割り当てのために、可能なカーネル ストリーミング状態遷移のサブセットのみが許可されています。 次の表は、有効な遷移と、Stream クラス ミニドライバーは、通常このような遷移中に実行するタスクを一覧表示します。

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
<td><p>一時停止停止します。</p></td>
<td><p>リソースを割り当てます。 移行後される Srb がキューに置かれた読み取り<strong>KSSTATE_PAUSE</strong>が完了します。</p></td>
</tr>
<tr class="even">
<td><p>実行を一時停止します。</p></td>
<td><p>ストリーミングを開始します。</p></td>
</tr>
<tr class="odd">
<td><p>実行を一時停止するには</p></td>
<td><p>ストリーミングを停止します。 未処理の読み取りされる Srb は、ミニドライバーによって管理されるキューに残ります。</p></td>
</tr>
<tr class="even">
<td><p>一時停止するには</p></td>
<td><p>リソースの割り当てを解除し、完了される Srb の未処理のすべて読み取り。 長さが 0 で完了される Srb をイメージに入力されていない、 <strong>DataUsed</strong>のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header" data-raw-source="[&lt;strong&gt;KSSTREAM_HEADER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)"> <strong>KSSTREAM_HEADER</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

**注**  :遷移の間で複数回を切り替えることができます、 **KSSTATE\_一時停止**と**KSSTATE\_実行**状態に戻る前に、 **KSSTATE\_停止**状態。 ビデオ キャプチャ ミニドライバーなどの遷移を想定する必要があります。

 

KSSTATE\_停止 -&gt; **KSSTATE\_ACQUIRE**  - &gt; **KSSTATE\_一時停止** - &gt; **KSSTATE\_実行** - &gt; **KSSTATE\_一時停止** - &gt; **KSSTATE\_実行** - &gt; **KSSTATE\_一時停止** - &gt; KSSTATE\_停止

ストリームがの場合に、 **KSSTATE\_停止**状態では、ミニドライバーは、すべての未処理データ読み取りされる Srb 直ちに完了する必要があります。

受け入れて処理の必要があります、すべての Stream クラス ミニドライバーでストリーミング中に、ユーザー モード アプリケーションが予期せず終了することができます、ため、 [ **SRB\_閉じる\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-close-stream)を要求しますいつでも Stream クラスのインターフェイスです。 クラス インターフェイスの SRB の送信、Stream の前に\_閉じる\_ストリーム、ミニドライバーにを通じてミニドライバーのすべての未解決のバッファーを取り消して**HwCancelPacket**ルーチン。 ストリームの状態を設定することはできません注**KSSTATE\_停止**アプリケーションが終了する前にします。

更新すれば、 **PictureNumber**または**DropCount**のメンバー [ **KS\_フレーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_frame_info)、 [ **KS\_VBI\_フレーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_vbi_frame_info)、または[ **KSPROPERTY\_DROPPEDFRAMES\_現在\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_droppedframes_current_s)からの移行で**KSSTATE\_一時停止**に**KSSTATE\_実行**または**KSSTATE\_実行**KSSTATE に\_一時停止します。 詳細については、次を参照してください。[ビデオのキャプチャ](capturing-video.md)します。

 

 




