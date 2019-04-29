---
title: WaveRT ミニポート ドライバー
description: WaveRT ミニポート ドライバー
ms.assetid: 154dc921-424f-4021-8f17-5482ceef99a8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4ae39f1364f90e8f9900e132d471c10688e7528
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328468"
---
# <a name="wavert-miniport-driver"></a>WaveRT ミニポート ドライバー


WaveRT ミニポート ドライバーが Windows Vista およびそれ以降の Windows オペレーティング システムでサポートされているし、wave レンダリングまたは wave キャプチャのオーディオ デバイスのハードウェアに依存する関数を管理します。 WaveRT 対応のオーディオ デバイスでは、スキャッター/ギャザー DMA のハードウェアと物理メモリ内の任意の場所の間にオーディオ データを転送できるを持っています。

WaveRT ミニポート ドライバーでは、2 つのインターフェイスを実装する必要があります。

-   [IMiniportWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536737)します。 このインターフェイスは、ミニポート ドライバーの初期化、チャネルの列挙型、およびストリームの作成を実行します。

-   [IMiniportWaveRTStream](https://msdn.microsoft.com/library/windows/hardware/ff536738)します。 このインターフェイスは、wave ストリームを管理し、ミニポート ドライバーの機能のほとんどを公開します。

WaveRT ポート ドライバーを補完する WaveRT ミニポート ドライバーを設計する方法については、次を参照してください。、 [WaveRT ミニポート ドライバーを開発](developing-a-wavert-miniport-driver.md)トピック。

### <a name="span-idiminiportwavertspanspan-idiminiportwavertspaniminiportwavert"></a><span id="iminiportwavert"></span><span id="IMINIPORTWAVERT"></span>IMiniportWaveRT

[IMiniportWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536737)インターフェイスは、次のメソッドを提供します。

[**IMiniportWaveRT::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536759)

ミニポート オブジェクトを初期化します。

[**IMiniportWaveRT::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536762)

新しいストリーム オブジェクトを作成します。

[**IMiniportWaveRT::GetDeviceDescription**](https://msdn.microsoft.com/library/windows/hardware/ff536758)

ポインターを返します、 [**デバイス\_説明**](https://msdn.microsoft.com/library/windows/hardware/ff543107)デバイスを記述する構造体。

### <a name="span-idiminiportwavertstreamspanspan-idiminiportwavertstreamspaniminiportwavertstream"></a><span id="iminiportwavertstream"></span><span id="IMINIPORTWAVERTSTREAM"></span>IMiniportWaveRTStream

[IMiniportWaveRTStream](https://msdn.microsoft.com/library/windows/hardware/ff536738)インターフェイスからのメソッドを継承する、 [ **IUnknown** ](https://msdn.microsoft.com/library/windows/desktop/ms680509)インターフェイス。 IMiniportWaveRTStream では、次の追加のメソッドを提供します。

[**IMiniportWaveRTStream::AllocateAudioBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536744)

オーディオ データの循環バッファーを割り当てます。

[**IMiniportWaveRTStream::FreeAudioBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536745)

以前の呼び出しで割り当てられているオーディオのバッファーを解放[ **IMiniportWaveRTStream::AllocateAudioBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536744)します。

[**IMiniportWaveRTStream::GetClockRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536746)

オーディオのサブシステムとそのクライアントにクロックのレジスタを公開するポートのドライバーが必要な情報を取得します。

[**IMiniportWaveRTStream::GetHWLatency**](https://msdn.microsoft.com/library/windows/hardware/ff536747)

オーディオ ハードウェアでストリームの待機時間のソースに関する情報を取得します。

[**IMiniportWaveRTStream::GetPosition**](https://msdn.microsoft.com/library/windows/hardware/ff536749)

現在の再生、バッファーの先頭からのオフセットをバイトとしてレコードの位置を取得します。

[**IMiniportWaveRTStream::GetPositionRegister**](https://msdn.microsoft.com/library/windows/hardware/ff536752)

オーディオのサブシステムとそのクライアントに位置レジスタを公開するポートのドライバーが必要な情報を取得します。

[**IMiniportWaveRTStream::SetFormat**](https://msdn.microsoft.com/library/windows/hardware/ff536753)

Wave ストリームのデータ形式を設定します。

[**IMiniportWaveRTStream::SetState**](https://msdn.microsoft.com/library/windows/hardware/ff536756)

オーディオ ストリームの転送状態を変更します。

 

 




