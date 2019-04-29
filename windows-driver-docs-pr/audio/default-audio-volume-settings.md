---
title: 既定のオーディオ音量の設定
description: 既定のオーディオ音量の設定
ms.assetid: 5d694aa2-5a47-44c5-92d5-ec8c4885820f
keywords:
- オーディオ アダプター WDK、ボリュームの設定
- アダプターのドライバー WDK オーディオ、ボリュームの設定
- ポート クラス オーディオ アダプター WDK、ボリュームの設定
- 既定のボリューム設定
- WDK のオーディオのボリュームの設定
- マスター ボリューム スライダー WDK オーディオ
- ボリューム スライダー WDK オーディオ
- WDK オーディオのサウンドのレベルの設定
- WDK のオーディオをマスター ボリュームの設定
- 既定のマスター ボリューム設定
- フル ボリューム スライダー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2ca4779183d005f3a06082783b17b593c7b3225
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333815"
---
# <a name="default-audio-volume-settings"></a>既定のオーディオ音量の設定


## <span id="default_audio_volume_settings"></span><span id="DEFAULT_AUDIO_VOLUME_SETTINGS"></span>


SndVol プログラム (を参照してください[システム トレイと SndVol32](systray-and-sndvol32.md)) ボリューム スライダーのセットが表示されます。 スライダーでは、さまざまなオーディオ デバイスとスピーカーやシステム サウンドなどのアプリケーションのボリューム レベルの設定を指定します。 オーディオ出力および入力ごとに、エンドポイントのボリュームとアプリケーションごとに、アプリケーションのボリュームがあります。 オーディオ ドライバーを KSPROPERTY を使用して、独自のエンドポイント ボリューム経由でのみ制御\_オーディオ\_VOLUMELEVEL します。 ドライバーによってインストールされている時点でのこれらのボリュームの設定が明示的に初期化しない場合、オペレーティング システムは、これらの設定の独自の既定値を選択します。 オペレーティング システムを選択する既定値が同じでないすべての Windows リリースで、ベンダーは、ボリューム レベルが高すぎるも小さすぎるの直後に次のドライバーのインストールに設定されていることを確認するアカウントにこれらの違いを実行する必要があります。

一般的な規則としてオーディオ アダプター ドライブの一連のアナログのスピーカーを独自の物理ボリューム コントロールを持つ場合、INF ファイル設定しないでください、既定のボリューム レベル小さすぎます。 それ以外の場合、ユーザーは、サウンド カードのマスターの量が増加するのではなくスピーカーのボリュームを増やすことで補正するためにお試しください可能性があります。 信号レベルが増えの結果は、オーディオ品質の低下です。

オーディオのアダプターはハードウェア アンプを持たない場合は、次を参照してください。[ソフトウェア ボリューム コントロールをサポート](software-volume-control-support.md)提供されるソフトウェアのサポートについてはします。

**注**  ハードウェア アンプがあるかどうかは、ドライバー レベルを設定、範囲と既定値を使用して、 [ **KSPROPERTY\_オーディオ\_VOLUMELEVEL** ](https://msdn.microsoft.com/library/windows/hardware/ff537309)カーネル プロパティをストリーミングします。 ハードウェア アンプがない場合、Windows は、APO ソフトウェア ボリューム コントロールを作成します。
物理的なボリュームつまみがスピーカーのアクティブなセットを使用する場合は、HID コントロールとして Windows に表示されます。 ボリュームに同様にこの関数は上向きと下向きの矢印ボタン キーボード上のボリューム。Windows がボリュームつまみが有効にしては、ボリュームをプログラム制御これに応じて拡大縮小 (は、ハードウェアまたはソフトウェアのボリューム) かどうかを参照してください。

 

理想的には、オーディオのアダプター カードと同じボックスで出荷される一連のアクティブなスピーカー、ファクトリは、アダプターの既定のボリュームの設定で最適な位置にスピーカーのボリュームつまみを調節してください。 オーディオのアダプターが物理ボリューム コントロールのノブを持たない場合を参照してください、[ソフトウェア ボリューム コントロールをサポート](https://msdn.microsoft.com/library/windows/hardware/ff539263)Windows によって提供されるソフトウェアのサポートについてはトピック。

**注**  オーディオ ハードウェア (ボリュームつまみ) のようなハードウェア ボリューム コントロールを公開するかどうかは、ドライバー レベルを設定、範囲と既定値を使用して、 [ **KSPROPERTY\_オーディオ\_VOLUMELEVEL** ](https://msdn.microsoft.com/library/windows/hardware/ff537309)カーネル ストリーミング プロパティ。

 

次の表は、ボリュームの範囲と既定のオーディオ ボリューム レベルの異なるバージョンの Windows でします。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows のバージョン</th>
<th align="left">マイクの既定値</th>
<th align="left">非-マイク * 既定値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Windows Vista SP1</td>
<td align="left"><p>既定のレベル:0.0db</p>
<p>ボリュームの範囲:-192.0 dB ~ + 12.0dB</p></td>
<td align="left"><p>既定のレベル:0.0db</p>
<p>ボリュームの範囲:-192.0 dB ~ 0dB</p></td>
</tr>
<tr class="even">
<td align="left">Windows 7</td>
<td align="left"><p>既定のレベル: + 30.0dB</p>
<p>ボリュームの範囲:-192 dB ~ +30.0 dB</p></td>
<td align="left"><p>既定のレベル:0 dB</p>
<p>ボリュームの範囲:-192 dB ~ 0 dB</p></td>
</tr>
<tr class="odd">
<td align="left">Windows 8</td>
<td align="left"><p>既定のレベル:0.0 dB</p>
<p>ボリュームの範囲:-96 dB ~ +30 dB</p></td>
<td align="left"><p>既定のレベル:0.0 dB</p>
<p>ボリュームの範囲:-96 dB ~ 0 dB</p></td>
</tr>
</tbody>
</table>

 

\*マイク用語以外には、すべての再生デバイスと以外マイクの録音デバイスについて説明します。
Windows アプリケーションでのソフトウェアのボリューム スライダーで表される物理ボリューム スライダーの運用特性については、次を参照してください。 [Audio-Tapered ボリューム コントロール](https://msdn.microsoft.com/library/windows/desktop/dd370798.aspx)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[既定のオーディオ音量設定のカスタマイズ](customizing-default-audio-volume-settings.md)  



