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
ms.openlocfilehash: c029b906e58a8cb612e81161152f00ed1644a9d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364788"
---
# <a name="wavepci-miniport-driver"></a>WavePci ミニポート ドライバー


## <span id="wavepci_miniport_driver"></span><span id="WAVEPCI_MINIPORT_DRIVER"></span>


**重要な**  WavePci の使用は推奨されなく、WaverRT を代わりに使用します。

 

WavePci ミニポート ドライバーでは、物理メモリ内の任意の場所から wave レンダリングまたはまたはオーディオ データを転送できる DMA ハードウェアはスキャッター/ギャザー wave キャプチャ デバイスのハードウェアに依存する関数を管理します。 スキャッター/ギャザーの転送を実行する機能がないか、物理メモリに制限されているリージョンのみにアクセスすることを wave デバイスを使用する必要があります、 [WaveCyclic ミニポート ドライバー](wavecyclic-miniport-driver.md)代わりにします。

WavePci ミニポート ドライバーでは、2 つのインターフェイスを実装する必要があります。

-   **ミニポート インターフェイス**ミニポート ドライバーの初期化、チャネルの列挙型、およびストリームの作成を実行します。

-   **ストリーム インターフェイス**wave ストリームを管理し、ミニポート ドライバーの機能のほとんどを公開します。

ミニポート インターフェイス[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepci)でメソッドを継承、 [IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiport)インターフェイス。 IMiniportWavePci では、次の追加のメソッドを提供します。

[**IMiniportWavePci::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-init)

ミニポート オブジェクトを初期化します。

[**IMiniportWavePci::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-newstream)

新しいストリーム オブジェクトを作成します。

[**IMiniportWavePci::Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-service)

サービスに対する要求のミニポート ドライバーに通知します。

ストリーム インターフェイス、 [IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepcistream)、メソッドを継承します、 [ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)インターフェイス。 IMiniportWavePciStream では、次の追加のメソッドを提供します。

[**IMiniportWavePciStream::GetAllocatorFraming**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-getallocatorframing)

Wave ストリームのミニポート ドライバーの優先アロケーター フレーム パラメーターを取得します。

[**IMiniportWavePciStream::GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-getposition)

Wave ストリーム内のデバイスの現在位置を取得します。

[**IMiniportWavePciStream::MappingAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-mappingavailable)

新しいマッピングがポート ドライバーから使用できることを示します。

[**IMiniportWavePciStream::NormalizePhysicalPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-normalizephysicalposition)

時間ベースの値には、物理バッファー位置の値を変換します。

[**IMiniportWavePciStream::RevokeMappings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-revokemappings)

以前に発行されたマッピングを取り消します。

[**IMiniportWavePciStream::Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-service)

サービスに対する要求のストリーム オブジェクトに通知します。

[**IMiniportWavePciStream::SetFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-setformat)

Wave ストリームのデータ形式を設定します。

[**IMiniportWavePciStream::SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-setstate)

Wave ストリームの状態を設定します。
 

 




