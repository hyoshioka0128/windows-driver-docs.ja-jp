---
title: ストリーミングの状態
description: ストリーミングの状態
ms.assetid: 1030e5cd-441b-4f6a-8f6a-21ce11aaca96
keywords:
- WDK AVStream ビデオ キャプチャは、ストリームを状態します。
- ビデオの WDK AVStream をキャプチャするには、ストリームを状態します。
- ストリームの状態の WDK ビデオ キャプチャ
- WDK のビデオ キャプチャを状態します。
- 状態の WDK ビデオ キャプチャを停止します。
- WDK ビデオ キャプチャの状態を取得します。
- 一時停止状態の WDK ビデオ キャプチャ
- WDK ビデオ キャプチャの状態を実行します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a1068fdabfc1dc1747065eb09693d4ab6a0db3c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390865"
---
# <a name="streaming-states"></a>ストリーミングの状態


4 つの状態のいずれかで、ミニドライバーによって提供される各ストリームが存在します。KSSTATE\_停止、KSSTATE\_ACQUIRE、KSSTATE\_一時停止、または KSSTATE\_を実行します。 初期化時に、ストリームが、既定で、 **KSSTATE\_停止**状態。 Stream クラス インターフェイスを送信するときに他の状態に遷移が行われた、 [ **SRB\_設定\_ストリーム\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff568210)ミニドライバーに要求します。 次の表では、識別し、4 つのストリームの状態について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状態</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSSTATE_STOP</p></td>
<td><p>ストリームの状態が停止したときに、ミニドライバーは、リソースの絶対最小値を使用して、未処理データ Srb ミニドライバーのキューではありません。</p></td>
</tr>
<tr class="even">
<td><p>KSSTATE_ACQUIRE</p></td>
<td><p>ストリームの状態は、リソースを取得するが場合、ミニドライバーは USB と IEEE 1394 の帯域幅など、必要なすべてのリソースを割り当てます。</p></td>
</tr>
<tr class="odd">
<td><p>KSSTATE_PAUSE</p></td>
<td><p>ストリームの状態が一時停止すると、ミニドライバーは KSSTATE_RUN を瞬時に遷移する準備済みです。</p></td>
</tr>
<tr class="even">
<td><p>KSSTATE_RUN</p></td>
<td><p>ミニドライバーが入力バッファーとされる Srb の使用が完了すると、ストリームの状態は、ストリーミング中、 <strong>CompleteStreamSRB</strong>します。</p></td>
</tr>
</tbody>
</table>

 

 

 




