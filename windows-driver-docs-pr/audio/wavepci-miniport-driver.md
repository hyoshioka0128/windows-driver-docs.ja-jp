---
title: WavePci ミニポート ドライバー
description: WavePci ミニポート ドライバー
ms.assetid: 8a166087-d158-4d49-a917-2a5a78b43cb4
keywords:
- オーディオのミニポート ドライバー WDK、WavePci
- ミニポート ドライバー WDK オーディオ、WavePci
- WavePci ミニポート ドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4c3f964af84e1da63b41271cd89c905e1626eaa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335231"
---
# <a name="wavepci-miniport-driver"></a>WavePci ミニポート ドライバー


## <span id="wavepci_miniport_driver"></span><span id="WAVEPCI_MINIPORT_DRIVER"></span>


**重要な**  WavePci の使用は推奨されなく、WaverRT を代わりに使用します。

 

WavePci ミニポート ドライバーでは、物理メモリ内の任意の場所から wave レンダリングまたはまたはオーディオ データを転送できる DMA ハードウェアはスキャッター/ギャザー wave キャプチャ デバイスのハードウェアに依存する関数を管理します。 スキャッター/ギャザーの転送を実行する機能がないか、物理メモリに制限されているリージョンのみにアクセスすることを wave デバイスを使用する必要があります、 [WaveCyclic ミニポート ドライバー](wavecyclic-miniport-driver.md)代わりにします。

WavePci ミニポート ドライバーでは、2 つのインターフェイスを実装する必要があります。

-   **ミニポート インターフェイス**ミニポート ドライバーの初期化、チャネルの列挙型、およびストリームの作成を実行します。

-   **ストリーム インターフェイス**wave ストリームを管理し、ミニポート ドライバーの機能のほとんどを公開します。

ミニポート インターフェイス[IMiniportWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536724)でメソッドを継承、 [IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698)インターフェイス。 IMiniportWavePci では、次の追加のメソッドを提供します。

[**IMiniportWavePci::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536734)

ミニポート オブジェクトを初期化します。

[**IMiniportWavePci::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536735)

新しいストリーム オブジェクトを作成します。

[**IMiniportWavePci::Service**](https://msdn.microsoft.com/library/windows/hardware/ff536736)

サービスに対する要求のミニポート ドライバーに通知します。

ストリーム インターフェイス、 [IMiniportWavePciStream](https://msdn.microsoft.com/library/windows/hardware/ff536725)、メソッドを継承します、 [ **IUnknown** ](https://msdn.microsoft.com/library/windows/desktop/ms680509)インターフェイス。 IMiniportWavePciStream では、次の追加のメソッドを提供します。

[**IMiniportWavePciStream::GetAllocatorFraming**](https://msdn.microsoft.com/library/windows/hardware/ff536726)

Wave ストリームのミニポート ドライバーの優先アロケーター フレーム パラメーターを取得します。

[**IMiniportWavePciStream::GetPosition**](https://msdn.microsoft.com/library/windows/hardware/ff536727)

Wave ストリーム内のデバイスの現在位置を取得します。

[**IMiniportWavePciStream::MappingAvailable**](https://msdn.microsoft.com/library/windows/hardware/ff536728)

新しいマッピングがポート ドライバーから使用できることを示します。

[**IMiniportWavePciStream::NormalizePhysicalPosition**](https://msdn.microsoft.com/library/windows/hardware/ff536729)

時間ベースの値には、物理バッファー位置の値を変換します。

[**IMiniportWavePciStream::RevokeMappings**](https://msdn.microsoft.com/library/windows/hardware/ff536730)

以前に発行されたマッピングを取り消します。

[**IMiniportWavePciStream::Service**](https://msdn.microsoft.com/library/windows/hardware/ff536731)

サービスに対する要求のストリーム オブジェクトに通知します。

[**IMiniportWavePciStream::SetFormat**](https://msdn.microsoft.com/library/windows/hardware/ff536732)

Wave ストリームのデータ形式を設定します。

[**IMiniportWavePciStream::SetState**](https://msdn.microsoft.com/library/windows/hardware/ff536733)

Wave ストリームの状態を設定します。
 

 




