---
title: オフロードされたオーディオ処理のためのヘルパー インターフェイス
description: このトピックでは、そのサポート オフロードされたオーディオ処理 PortCls ヘルパー インターフェイスのしやすいように、ドライバーを示します。
ms.assetid: 9C78621E-9824-4992-9D7E-BCF3B51F1BFB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9a2b72a4305fc4fbb3f98c4773c96cab0831f15
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359981"
---
# <a name="helper-interfaces-for-offloaded-audio-processing"></a>オフロードされたオーディオ処理のためのヘルパー インターフェイス


このトピックでは、そのサポート オフロードされたオーディオ処理 Microsoft オーディオ ポート クラス ドライバー (PortCls) に追加のドライバーの実装を簡略化するヘルパー インターフェイスを表示します。

によるハードウェア オフロードされたオーディオ ストリームを処理できるオーディオのアダプターで動作する WaveRT ミニポート ドライバーを開発する際に、ミニポート ドライバーは、オーディオ ストリームやプロセスのデータを PortCls で動作します。

すべて、オフロード関連のカーネル (KS) のプロパティをストリーミングを処理するために PortCls が更新され、どのようなシンプルな方法によるハードウェア オフロードされたオーディオ ストリームを処理するためのサポートを公開する WaveRT ミニポート ドライバーの開発です。 のみ PortCls は、更新プログラムの結果として、ハードウェアや新しく定義した 2 つのインターフェイスを使用してドライバー固有の操作の基になるミニポート ドライバーを呼び出します。

-   [**IMiniportAudioEngineNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportaudioenginenode)

-   [**IMiniportStreamAudioEngineNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportstreamaudioenginenode)

これらのインターフェイスの各インターフェイスのいずれかを使用する 2 つのクラスを開発する必要があります。

## <a name="span-idworkingwithiminiportaudioenginenodespanspan-idworkingwithiminiportaudioenginenodespanspan-idworkingwithiminiportaudioenginenodespanworking-with-iminiportaudioenginenode"></a><span id="Working_with_IMiniportAudioEngineNode"></span><span id="working_with_iminiportaudioenginenode"></span><span id="WORKING_WITH_IMINIPORTAUDIOENGINENODE"></span>IMiniportAudioEngineNode の操作


クラスを使用するために開発を**IMiniportAudioEngineNode**から継承する必要がありますも[IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavert)します。 定義されているメソッド**IMiniportAudioEngineNode** KS フィルターのハンドルを使用してオーディオ エンジンにアクセスする KS プロパティを使用して、ドライバーを許可します。 クラスまたはインターフェイス階層は次のとおりです。

![カスタム wavert ミニポート クラスは、iminiportwavert および iminiportaudioenginenode から継承します。](images/offload-class-hier1.png)

したがって CYourMiniportWaveRT という名前のクラスを開発するなどの場合は、し、上の図からわかるように CYourMiniportWaveRT する必要がありますメソッドを実装すべて (操作として表示) の 2 つの親インターフェイスで定義されています。

このようなクラスのスケルトンのテンプレートは、次のコードが含まれます。

```ManagedCPlusPlus
class CMiniportWaveRT : 
    public IMiniportWaveRT,
    public IMiniportAudioEngineNode,
    public CUnknown
{
...

    IMP_IMiniportWaveRT;
    IMP_IMiniportAudioEngineNode;
...

};
```

*Portcls.h*ヘッダー ファイルは、これらのインターフェイスを定義します。

## <a name="span-idworkingwithiminiportstreamaudioenginenodespanspan-idworkingwithiminiportstreamaudioenginenodespanspan-idworkingwithiminiportstreamaudioenginenodespanworking-with-iminiportstreamaudioenginenode"></a><span id="Working_with_IMiniportStreamAudioEngineNode"></span><span id="working_with_iminiportstreamaudioenginenode"></span><span id="WORKING_WITH_IMINIPORTSTREAMAUDIOENGINENODE"></span>IMiniportStreamAudioEngineNode の操作


2 番目のインターフェイスを使用するために開発クラス**IMiniportStreamAudioEngineNode**から継承する必要がありますも[IMiniportWaveRTStreamNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavertstreamnotification)します。 定義されているメソッド**IMiniportStreamAudioEngineNode**暗証番号 (pin) のインスタンス ハンドルを使用してオーディオ エンジンにアクセスする KS プロパティを使用して、ドライバーを許可します。 クラスまたはインターフェイス階層は次のとおりです。

![カスタム wavert ストリームのミニポート クラスは、および iminiportstreamaudioenginenode iminiportwavertstreamnotification からを継承します。](images/offload-class-hier2.png)

その場合、CYourMiniportWaveRTStream という名前のクラスを開発するなど、上の図からわかるように CYourMiniportWaveRTStream する必要があります実装の 2 つの親インターフェイスで定義されているすべてのメソッド。

このようなクラスのスケルトンのテンプレートは、次のコードが含まれます。

```ManagedCPlusPlus
class CMiniportWaveRTStream : 
    public IMiniportWaveRTStreamNotification,
    public IMiniportStreamAudioEngineNode,
    public CUnknown
{
...
    IMP_IMiniportWaveRTStream;
    IMP_IMiniportWaveRTStreamNotification;
    IMP_IMiniportStreamAudioEngineNode;
...

};
```

*Portcls.h*ヘッダー ファイルは、これらのインターフェイスを定義します。 によるハードウェア オフロードされたオーディオ ストリームを処理できるドライバーを開発する方法の詳細については、次を参照してください。 および[ドライバーの実装詳細](driver-implementation-details.md)します。

 

 




