---
title: WaveCyclic ミニポート ドライバー
description: WaveCyclic ミニポート ドライバー
ms.assetid: 8a4811e9-e52b-4183-8d11-482883500f82
keywords:
- オーディオのミニポート ドライバー WDK、WaveCyclic
- ミニポート ドライバー WDK オーディオ、WaveCyclic
- WaveCyclic ミニポート ドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 994994954e6f651d6b5a6eeea5b11985397abc31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581581"
---
# <a name="wavecyclic-miniport-driver"></a>WaveCyclic ミニポート ドライバー


## <span id="wavecyclic_miniport_driver"></span><span id="WAVECYCLIC_MINIPORT_DRIVER"></span>


**重要な**  WavePci の使用は推奨されなく、WaverRT を代わりに使用します。

 

WaveCyclic ミニポート ドライバーでは、wave レンダリングまたはオーディオ データの循環バッファーを使用して wave キャプチャ デバイスのハードウェアに依存する関数を管理します。 循環バッファーは、連続した物理メモリの 1 つのブロックは、通常とドライバーの選択のメモリの領域にあることができます。 次の制限事項のいずれかを使用したデバイスが WaveCyclic ミニポート ドライバーを提供する必要がありますではなく[WavePci ミニポート ドライバー](wavepci-miniport-driver.md):

-   デバイスでは、DMA ハードウェアがありません。

-   デバイスの DMA ハードウェアは、連続した物理メモリの 1 つのブロックを占有するバッファーにのみデータにアクセスできます。

-   デバイスの DMA のハードウェアが物理メモリのすべてのリージョンでデータにアクセスできません。

WaveCyclic ミニポート ドライバーでは、2 つのインターフェイスを実装する必要があります。

-   **ミニポート インターフェイス**ミニポート ドライバーの初期化とストリームの作成をサポートします。

-   **ストリーム インターフェイス**wave ストリームを管理し、ミニポート ドライバーの機能のほとんどを公開します。

ミニポート インターフェイス[IMiniportWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536714)でメソッドを継承、 [IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)インターフェイス。 IMiniportWaveCyclic では、次の追加のメソッドを提供します。

[**IMiniportWaveCyclic::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536722)

ミニポート オブジェクトを初期化します。

[**IMiniportWaveCyclic::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536723)

新しいストリーム オブジェクトを作成します。

ストリーム インターフェイス、 [IMiniportWaveCyclicStream](https://msdn.microsoft.com/library/windows/hardware/ff536715)でメソッドを継承、 [ **IUnknown** ](https://msdn.microsoft.com/library/windows/desktop/ms680509)インターフェイス。 IMiniportWaveCyclicStream では、次の追加のメソッドを提供します。

[**IMiniportWaveCyclicStream::GetPosition**](https://msdn.microsoft.com/library/windows/hardware/ff536716)

Wave ストリーム内のデバイスの現在位置を取得します。

[**IMiniportWaveCyclicStream::NormalizePhysicalPosition**](https://msdn.microsoft.com/library/windows/hardware/ff536717)

時間ベースの値には、物理バッファー位置の値を変換します。

[**IMiniportWaveCyclicStream::SetFormat**](https://msdn.microsoft.com/library/windows/hardware/ff536718)

Wave ストリームのデータ形式を設定します。

[**IMiniportWaveCyclicStream::SetNotificationFreq**](https://msdn.microsoft.com/library/windows/hardware/ff536719)

通知に割り込みが発生する頻度を設定します。

[**IMiniportWaveCyclicStream::SetState**](https://msdn.microsoft.com/library/windows/hardware/ff536720)

Wave ストリームの状態を設定します。

[**IMiniportWaveCyclicStream::Silence**](https://msdn.microsoft.com/library/windows/hardware/ff536721)

バッファーにコピー アクティビティがない状態です。
 

 




