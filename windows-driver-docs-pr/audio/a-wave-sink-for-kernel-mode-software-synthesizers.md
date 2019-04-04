---
title: カーネル モードのソフトウェアのシンセサイザーのウェーブ シンク
description: カーネル モードのソフトウェアのシンセサイザーのウェーブ シンク
ms.assetid: 37ba9ad5-8b35-4252-a6fd-46dead924294
keywords:
- wave オーディオ、カーネル モード ソフトウェアのシンセサイザーの WDK をシンクします。
- MIDI トランスポート WDK オーディオ
- wave オーディオ、MIDI トランスポートの WDK をシンクします。
- シンセサイザー WDK オーディオ、MIDI トランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89dcb17890d03ad20f851c3c3a7adc780fcb02c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560826"
---
# <a name="a-wave-sink-for-kernel-mode-software-synthesizers"></a>カーネル モードのソフトウェアのシンセサイザーのウェーブ シンク


## <span id="a_wave_sink_for_kernel_mode_software_synthesizers"></span><span id="A_WAVE_SINK_FOR_KERNEL_MODE_SOFTWARE_SYNTHESIZERS"></span>


説明したよう[シンセサイザーと Wave シンク](synthesizers-and-wave-sinks.md)、Dmu ポート ドライバーがカーネル モードで動作するソフトウェアのシンセサイザーのウェーブ シンクを実装します。 シンセサイザーのミニポート ドライバーを公開して、 [ISynthSinkDMus](https://msdn.microsoft.com/library/windows/hardware/ff537011)ポート ドライバーへのインターフェイス。 ポート ドライバーのウェーブ シンクでは、このインターフェイスを使用して、シンセサイザーによって生成される wave データを読み取る。

Dmu ポート ドライバーの波のシンクの Dmu のミニポート ドライバーを使用するのには、暗証番号 (pin) の 2 つの型を持つ DirectMusic フィルターを定義する必要があります。

-   DirectMusic 入力ピンまたは MIDI が pin を入力します。 この pin は、MIDI メッセージを含むレンダー ストリームのシンクです。

-   Wave は、暗証番号 (pin) を出力します。 この pin は、PCM のサンプルを含むレンダー ストリームのソースです。

シンセサイザーのノードを含む DirectMusic フィルターを次に示します ([**KSNODETYPE\_シンセサイザー**](https://msdn.microsoft.com/library/windows/hardware/ff537203))。 このフィルターは、DirectMusic 入力ピンと出力の pin を wave を提供することによって前のシンセサイザーのカーネル モード ソフトウェア要件を満たしています。 (さらに、レガシ MIDI 合成をサポートしている Dmu ミニポート ドライバー pin を指定できる MIDI 入力します。)

![カーネル モード ソフトウェアのシンセサイザーの directmusic フィルターを示す図](images/wavesink.png)

図の左側にある、MIDI ストリームは DirectMusic 入力ピンを使用して、フィルターになります。 このピンは、 [IMXF](https://msdn.microsoft.com/library/windows/hardware/ff536782)ポート ドライバーに公開するインターフェイス。 ポートのドライバーが呼び出すことによってこのインターフェイスを取得、 [ **IMiniportDMus::NewStream** ](https://msdn.microsoft.com/library/windows/hardware/ff536701)メソッド。 ポート ドライバーでは、ピンに MIDI メッセージをフィードを呼び出して、 [ **IMXF::PutMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff536791)メソッド。

図の右側にある、wave ストリームは、ポート ドライバーのウェーブ シンクに wave 出力ピンとフローを使用して、フィルターを終了します。 ポート ドライバーを通じて暗証番号 (pin) と通信してその**ISynthSinkDMus**インターフェイス。 ポート ドライバーは、最初の呼び出しによってこのインターフェイスを取得**IMiniportDMus::NewStream**を使用して、ストリーム オブジェクトを取得、 **IMXF**インターフェイス、およびオブジェクトを照会してその**ISynthSinkDMus**インターフェイス。 Wave シンク wave はデータを取得、暗証番号 (pin) から呼び出すことによって、 [ **ISynthSinkDMus::Render** ](https://msdn.microsoft.com/library/windows/hardware/ff537015)メソッド。

原則としてのハードウェア シンセサイザーでしたがポート ドライバーの波のシンクへの呼び出しをレンダリングするために依存して**ISynthSinkDMus::Render** MIDI stream やすく魅力的ではありません多くの対話型に十分な待機時間を追加します。アプリケーション。 ハードウェアのシンセサイザーの内部接続をされている可能性がストリームの待機時間を減らすためには、ポート ドライバーのウェーブ シンクを使用する代わりにミキシングおよび wave レンダリングのハードウェア。 この種類のシンセサイザー有線接続上の図の右側にある wave 出力ピンが置き換えられます (として表される、*ブリッジ pin*) ハードウェア ミキサーにします。

**ISynthSinkDMus** wave シンクを使用して wave データを表示するためにメソッドは、サンプリング時間と、参照時間から変換し、マスターのクロックと同期インターフェイスを提供します。

[**ISynthSinkDMus::RefTimeToSample**](https://msdn.microsoft.com/library/windows/hardware/ff537013)

[**ISynthSinkDMus::Render**](https://msdn.microsoft.com/library/windows/hardware/ff537015)

[**ISynthSinkDMus::SampleToRefTime**](https://msdn.microsoft.com/library/windows/hardware/ff537018)

[**ISynthSinkDMus::SyncToMaster**](https://msdn.microsoft.com/library/windows/hardware/ff537019)

**ISynthSinkDMus**継承、 **IMXF**インターフェイス。 詳細については、[ISynthSinkDMus](https://msdn.microsoft.com/library/windows/hardware/ff537011)を参照してください。

上記の図の Dmu ミニポート ドライバーでは、その DirectMusic 入力ピンと出力ピンを wave としては、次のように識別します。

-   ミニポート ドライバー、DirectMusic 入力ピンを識別するためには、型 KSDATAFORMAT の主要な形式に暗証番号 (pin) のデータ範囲を定義します\_型\_音楽およびのサブフォーマット型 KSDATAFORMAT\_サブタイプ\_DIRECTMUSIC します。 この組み合わせは、pin が MIDI タイムスタンプ付きストリームを受け入れることを示します。 データ範囲の記述子が型の構造体[ **KSDATARANGE\_音楽**](https://msdn.microsoft.com/library/windows/hardware/ff537097)します。 (例については、次を参照してください[DirectMusic Stream データ範囲](directmusic-stream-data-range.md)。)。ミニポート ドライバー KSPIN に暗証番号 (pin) のデータ フローの方向を定義する\_データフロー\_in です。 (、 [ **PCPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537721)構造体の**KsPinDescriptor**します。データ フローのメンバーを示すデータ フローの方向。)呼び出すときに**IMiniportDMus::NewStream**ポート ドライバーの設定をこのピンのストリーム オブジェクトを作成する、 *StreamType*パラメーター DMU を\_ストリーム\_MIDI\_をレンダリングします。

-   ミニポート ドライバーを wave 出力ピンを識別するためには、型 KSDATAFORMAT の主要な形式に暗証番号 (pin) のデータ範囲を定義します\_型\_オーディオおよびのサブフォーマット型 KSDATAFORMAT\_サブタイプ\_PCM。 この組み合わせは、pin が PCM サンプルを含む、wave オーディオ ストリームに出力することを示します。 データ範囲の記述子が型の構造体[ **KSDATARANGE\_オーディオ**](https://msdn.microsoft.com/library/windows/hardware/ff537096)します。 (例を参照してください[PCM Stream データ範囲](pcm-stream-data-range.md)。)。ミニポート ドライバー KSPIN に暗証番号 (pin) のデータ フローの方向を定義する\_データフロー\_アウトします。 呼び出すときに**IMiniportDMus::NewStream**ポート ドライバーの設定をこのピンのストリーム オブジェクトを作成する、 *StreamType*パラメーター DMU を\_ストリーム\_WAVE\_シンクします。

さらに、シンセサイザーの MIDI 入力ピンをサポートする場合、ドライバーは、その定義は、DirectMusic の入力ピンのようになりますが、pin の定義、サブフォーマット型 KSDATAFORMAT の指定\_サブタイプ\_MIDI、MIDI、タイムスタンプ付きストリームではなく生のストリームを MIDI、暗証番号 (pin) が受け入れていました。

 

 




