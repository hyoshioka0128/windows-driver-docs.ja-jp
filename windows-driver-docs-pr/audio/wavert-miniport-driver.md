---
title: WaveRT ミニポート ドライバー
description: WaveRT ミニポート ドライバー
ms.assetid: 154dc921-424f-4021-8f17-5482ceef99a8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bec5fc60b482d9b839b924bb296370b9c8bd47b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829936"
---
# <a name="wavert-miniport-driver"></a>WaveRT ミニポート ドライバー


WaveRT ミニポートドライバーは、Windows Vista 以降の Windows オペレーティングシステムでサポートされており、wave レンダリングまたは wave キャプチャオーディオデバイスのハードウェアに依存する機能を管理します。 WaveRT 対応のオーディオデバイスには、物理メモリ内の任意の場所との間でオーディオデータを転送できる、スキャッター/ギャザー DMA ハードウェアが搭載されています。

WaveRT ミニポートドライバーは、次の2つのインターフェイスを実装する必要があります。

-   [IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert)。 このインターフェイスは、ミニポートドライバーの初期化、チャネル列挙、およびストリーム作成を実行します。

-   [IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream)。 このインターフェイスは、wave ストリームを管理し、ミニポートドライバーのほとんどの機能を公開します。

Wavert ポートドライバーを補完する wavert ミニポートドライバーを設計する方法の詳細については、「 [Wavert ミニポートドライバーの開発](developing-a-wavert-miniport-driver.md)」を参照してください。

### <a name="span-idiminiportwavertspanspan-idiminiportwavertspaniminiportwavert"></a><span id="iminiportwavert"></span><span id="IMINIPORTWAVERT"></span>IMiniportWaveRT

[IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert)インターフェイスには、次のメソッドが用意されています。

[**IMiniportWaveRT:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavert-init)

ミニポートオブジェクトを初期化します。

[**IMiniportWaveRT:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavert-newstream)

新しいストリームオブジェクトを作成します。

[**IMiniportWaveRT:: GetDeviceDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavert-getdevicedescription)

デバイスを記述する[**デバイス\_説明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_description)構造体へのポインターを返します。

### <a name="span-idiminiportwavertstreamspanspan-idiminiportwavertstreamspaniminiportwavertstream"></a><span id="iminiportwavertstream"></span><span id="IMINIPORTWAVERTSTREAM"></span>IMiniportWaveRTStream

[IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream)インターフェイスは、 [**IUnknown**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)インターフェイスからメソッドを継承します。 IMiniportWaveRTStream には、次の追加のメソッドが用意されています。

[**IMiniportWaveRTStream:: AllocateAudioBuffer**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536744(v=vs.85))

オーディオデータの循環バッファーを割り当てます。

[**IMiniportWaveRTStream:: FreeAudioBuffer**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536745(v=vs.85))

[**IMiniportWaveRTStream:: AllocateAudioBuffer**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536744(v=vs.85))の呼び出しで以前に割り当てられたオーディオバッファーを解放します。

[**IMiniportWaveRTStream:: GetClockRegister**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536746(v=vs.85))

クロックレジスタをオーディオサブシステムとそのクライアントに公開するために、ポートドライバーが必要とする情報を取得します。

[**IMiniportWaveRTStream::GetHWLatency**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536747(v=vs.85))

オーディオハードウェアのストリーム待機時間のソースに関する情報を取得します。

[**IMiniportWaveRTStream::GetPosition**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536749(v=vs.85))

現在の再生位置またはレコード位置を、バッファーの先頭からのバイトオフセットとして取得します。

[**IMiniportWaveRTStream:: GetPositionRegister**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536752(v=vs.85))

オーディオサブシステムとそのクライアントに位置登録を公開するために、ポートドライバーが必要とする情報を取得します。

[**IMiniportWaveRTStream:: SetFormat**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536753(v=vs.85))

Wave ストリームのデータ形式を設定します。

[**IMiniportWaveRTStream:: SetState**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536756(v=vs.85))

オーディオストリームのトランスポートの状態を変更します。

 

 




