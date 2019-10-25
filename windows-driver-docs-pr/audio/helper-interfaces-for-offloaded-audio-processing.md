---
title: オフロードされたオーディオ処理のためのヘルパー インターフェイス
description: このトピックでは、オフロードオーディオ処理をサポートするドライバーを簡略化するための PortCls helper インターフェイスについて説明します。
ms.assetid: 9C78621E-9824-4992-9D7E-BCF3B51F1BFB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fcf6c040a9cb1958997abd8a0db7ff155ec2374
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833303"
---
# <a name="helper-interfaces-for-offloaded-audio-processing"></a>オフロードされたオーディオ処理のためのヘルパー インターフェイス


このトピックでは、オフロードオーディオ処理をサポートするドライバーの実装を簡略化するために、Microsoft がオーディオポートクラスドライバー (PortCls) に追加したヘルパーインターフェイスについて説明します。

ハードウェアオフロードオーディオストリームを処理できるオーディオアダプターで動作する WaveRT ミニポートドライバーを開発する場合、ミニポートドライバーは PortCls と連携して、オーディオデータをストリーミングまたは処理します。

PortCls は、すべてのオフロード関連のカーネルストリーミング (KS) プロパティを処理するように更新されています。これにより、ハードウェアオフロードオーディオストリームの処理をサポートするための WaveRT ミニポートドライバーを簡単に開発できるようになります。 更新の結果として、PortCls は、新しく定義された2つのインターフェイスを使用して、ハードウェアやドライバー固有の操作を行うために、基になるミニポートドライバーのみを呼び出します。

-   [**IMiniportAudioEngineNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportaudioenginenode)

-   [**IMiniportStreamAudioEngineNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportstreamaudioenginenode)

これらのインターフェイスを使用するには、インターフェイスごとに1つずつ、2つのクラスを開発する必要があります。

## <a name="span-idworking_with_iminiportaudioenginenodespanspan-idworking_with_iminiportaudioenginenodespanspan-idworking_with_iminiportaudioenginenodespanworking-with-iminiportaudioenginenode"></a><span id="Working_with_IMiniportAudioEngineNode"></span><span id="working_with_iminiportaudioenginenode"></span><span id="WORKING_WITH_IMINIPORTAUDIOENGINENODE"></span>IMiniportAudioEngineNode の操作


**IMiniportAudioEngineNode**を使用するために開発するクラスは、 [IMiniportWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert)からも継承する必要があります。 **IMiniportAudioEngineNode**で定義されているメソッドを使用すると、ドライバーは ks フィルターハンドルを介してオーディオエンジンにアクセスする ks プロパティを使用できます。 クラス/インターフェイス階層は次のとおりです。

![カスタム wavert ミニポートクラスは、iminiportaudioenginenode から継承されます。](images/offload-class-hier1.png)

たとえば、CYourMiniportWaveRT というクラスを開発する場合は、前の図からわかるように、CYourMiniportWaveRT は2つの親インターフェイスに対して定義されているすべてのメソッド (操作として表示) を実装する必要があります。

このようなクラスのスケルトンテンプレートには、次のコードが含まれます。

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

これらのインターフェイスは、 *Portcls*ヘッダーファイルで定義されています。

## <a name="span-idworking_with_iminiportstreamaudioenginenodespanspan-idworking_with_iminiportstreamaudioenginenodespanspan-idworking_with_iminiportstreamaudioenginenodespanworking-with-iminiportstreamaudioenginenode"></a><span id="Working_with_IMiniportStreamAudioEngineNode"></span><span id="working_with_iminiportstreamaudioenginenode"></span><span id="WORKING_WITH_IMINIPORTSTREAMAUDIOENGINENODE"></span>IMiniportStreamAudioEngineNode の操作


2番目のインターフェイス**IMiniportStreamAudioEngineNode**を操作するために開発するクラスは、 [IMiniportWaveRTStreamNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstreamnotification)からも継承する必要があります。 **IMiniportStreamAudioEngineNode**で定義されているメソッドを使用すると、ドライバーは、pin インスタンスハンドルを介してオーディオエンジンにアクセスする KS プロパティを使用できます。 クラス/インターフェイス階層は次のとおりです。

![カスタム wavert ストリームミニポートクラスは、iminiportstreamaudioenginenode から継承されます。](images/offload-class-hier2.png)

たとえば、ca Miniportwavertstream というクラスを開発する場合は、前の図からわかるように、Cit Miniportwavertstream は、2つの親インターフェイスに対して定義されているすべてのメソッドを実装する必要があります。

このようなクラスのスケルトンテンプレートには、次のコードが含まれます。

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

これらのインターフェイスは、 *Portcls*ヘッダーファイルで定義されています。 ハードウェアオフロードオーディオストリームを処理できるドライバーを開発する方法の詳細については、「[ドライバーの実装の詳細](driver-implementation-details.md)」を参照してください。

 

 




