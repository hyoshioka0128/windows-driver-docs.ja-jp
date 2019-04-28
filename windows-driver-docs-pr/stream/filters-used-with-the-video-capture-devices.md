---
title: ビデオ キャプチャ デバイスで使用されるフィルター
description: ビデオ キャプチャ デバイスで使用されるフィルター
ms.assetid: 797f855d-5c6f-45bc-8b4a-f03543fa196d
keywords:
- グラフ構成 WDK ビデオ キャプチャ、DirectShow をフィルター処理します。
- DirectShow の WDK ビデオのキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4224abfd47a8a248c4633c6e8ddeadd2d98bb11f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376098"
---
# <a name="filters-used-with-the-video-capture-devices"></a>ビデオ キャプチャ デバイスで使用されるフィルター


Microsoft DirectShow は、ビデオ キャプチャ ミニドライバーの一般的なクライアントです。 ユーザー モード DirectShow フィルターは、ユーザー モード アプリケーションへのビデオ キャプチャ ミニドライバーに含まれている機能を公開します。

マイクロソフトでは、基になるビデオ キャプチャ ミニドライバーの機能を公開する Stream クラス ミニドライバーで動作する 4 つの DirectShow フィルターを提供します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>フィルターの機能</th>
<th>カーネルのストリーミングでサポートされているプロパティ セット</th>
<th>目的</th>
<th>DLL</th>
<th>公開される DirectShow インターフェイス</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ビデオのキャプチャ</p></td>
<td><p>PROPSETID_VIDCAP_DROPPEDFRAMES</p>
<p>PROPSETID_VIDCAP_VIDEOCOMPRESSION</p>
<p>PROPSETID_VIDCAP_VIDEOCONTROL</p>
<p>PROPSETID_VIDCAP_VIDEODECODER</p>
<p>PROPSETID_VIDCAP_CAMERAMCONTROL</p>
<p>PROPSETID_VIDCAP_VIDEOPROCAMP</p></td>
<td><p>デジタル ビデオ データの出力ストリームと補助データ ストリームを提供します。</p></td>
<td><p><em>KsProxy.ax</em></p></td>
<td><p><strong>IAMAnalogVideoDecoder</strong></p>
<p><strong>IAMCameraControl</strong></p>
<p><strong>IAMVideoProcAmp</strong></p>
<p><strong>IAMDroppedFrames</strong></p>
<p><strong>IAMStreamConfig</strong></p>
<p><strong>IAMVideoControl</strong></p>
<p><strong>IAMVideoCompression</strong></p>
<p><strong>IAMBufferNegotiation</strong></p></td>
</tr>
<tr class="even">
<td><p>テレビのチューニング</p></td>
<td><p>PROPSETID_TUNER</p></td>
<td><p>アナログ テレビ、デジタル テレビ、FM のチューニングの制御を提供し、チューナーのできました。</p></td>
<td><p><em>KsTvTune.ax</em></p></td>
<td><p><strong>IAMTVTuner</strong></p></td>
</tr>
<tr class="odd">
<td><p>テレビのオーディオ</p></td>
<td><p>PROPSETID_VIDCAP_TVAUDIO</p></td>
<td><p>SAP の選択などのテレビのオーディオの制御を提供します。</p></td>
<td><p><em>KsXBar.ax</em></p></td>
<td><p><strong>IAMTVAudio</strong></p></td>
</tr>
<tr class="even">
<td><p>クロスバー</p></td>
<td><p>PROPSETID_VIDCAP_CROSSBAR</p></td>
<td><p>ビデオとオーディオ ストリームのルーティングを提供します。</p></td>
<td><p><em>KsXBar.ax</em></p></td>
<td><p><strong>IAMCrossbar</strong></p></td>
</tr>
</tbody>
</table>

 

これらのフィルターと機能を (ビデオのキャプチャ、テレビやラジオのチューニング、テレビのオーディオおよびクロスバー) を公開するは、一意のインターフェイスを公開する別個のフィルターとしてフィルター グラフに表示されます。

上記の表に示されている DirectShow インターフェイスの詳細については、DirectShow ソフトウェア開発キット (SDK) を参照してください。 DirectShow の SDK ドキュメントには、幅広い WDM と VfW の両方のキャプチャのグラフを作成する方法を示すサンプル アプリケーション (AMCAP) も含まれています。

 

 




