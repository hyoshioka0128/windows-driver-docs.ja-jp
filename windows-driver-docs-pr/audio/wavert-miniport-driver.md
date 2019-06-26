---
title: WaveRT ミニポート ドライバー
description: WaveRT ミニポート ドライバー
ms.assetid: 154dc921-424f-4021-8f17-5482ceef99a8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 064146e8eca9a2ffb80f927bd5856cad0711465d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364786"
---
# <a name="wavert-miniport-driver"></a>WaveRT ミニポート ドライバー


WaveRT ミニポート ドライバーが Windows Vista およびそれ以降の Windows オペレーティング システムでサポートされているし、wave レンダリングまたは wave キャプチャのオーディオ デバイスのハードウェアに依存する関数を管理します。 WaveRT 対応のオーディオ デバイスでは、スキャッター/ギャザー DMA のハードウェアと物理メモリ内の任意の場所の間にオーディオ データを転送できるを持っています。

WaveRT ミニポート ドライバーでは、2 つのインターフェイスを実装する必要があります。

-   [IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavert)します。 このインターフェイスは、ミニポート ドライバーの初期化、チャネルの列挙型、およびストリームの作成を実行します。

-   [IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavertstream)します。 このインターフェイスは、wave ストリームを管理し、ミニポート ドライバーの機能のほとんどを公開します。

WaveRT ポート ドライバーを補完する WaveRT ミニポート ドライバーを設計する方法については、次を参照してください。、 [WaveRT ミニポート ドライバーを開発](developing-a-wavert-miniport-driver.md)トピック。

### <a name="span-idiminiportwavertspanspan-idiminiportwavertspaniminiportwavert"></a><span id="iminiportwavert"></span><span id="IMINIPORTWAVERT"></span>IMiniportWaveRT

[IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavert)インターフェイスは、次のメソッドを提供します。

[**IMiniportWaveRT::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavert-init)

ミニポート オブジェクトを初期化します。

[**IMiniportWaveRT::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavert-newstream)

新しいストリーム オブジェクトを作成します。

[**IMiniportWaveRT::GetDeviceDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavert-getdevicedescription)

ポインターを返します、 [**デバイス\_説明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_description)デバイスを記述する構造体。

### <a name="span-idiminiportwavertstreamspanspan-idiminiportwavertstreamspaniminiportwavertstream"></a><span id="iminiportwavertstream"></span><span id="IMINIPORTWAVERTSTREAM"></span>IMiniportWaveRTStream

[IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavertstream)インターフェイスからのメソッドを継承する、 [ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)インターフェイス。 IMiniportWaveRTStream では、次の追加のメソッドを提供します。

[**IMiniportWaveRTStream::AllocateAudioBuffer**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536744(v=vs.85))

オーディオ データの循環バッファーを割り当てます。

[**IMiniportWaveRTStream::FreeAudioBuffer**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536745(v=vs.85))

以前の呼び出しで割り当てられているオーディオのバッファーを解放[ **IMiniportWaveRTStream::AllocateAudioBuffer**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536744(v=vs.85))します。

[**IMiniportWaveRTStream::GetClockRegister**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536746(v=vs.85))

オーディオのサブシステムとそのクライアントにクロックのレジスタを公開するポートのドライバーが必要な情報を取得します。

[**IMiniportWaveRTStream::GetHWLatency**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536747(v=vs.85))

オーディオ ハードウェアでストリームの待機時間のソースに関する情報を取得します。

[**IMiniportWaveRTStream::GetPosition**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536749(v=vs.85))

現在の再生、バッファーの先頭からのオフセットをバイトとしてレコードの位置を取得します。

[**IMiniportWaveRTStream::GetPositionRegister**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536752(v=vs.85))

オーディオのサブシステムとそのクライアントに位置レジスタを公開するポートのドライバーが必要な情報を取得します。

[**IMiniportWaveRTStream::SetFormat**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536753(v=vs.85))

Wave ストリームのデータ形式を設定します。

[**IMiniportWaveRTStream::SetState**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536756(v=vs.85))

オーディオ ストリームの転送状態を変更します。

 

 




