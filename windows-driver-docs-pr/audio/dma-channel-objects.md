---
title: DMA チャネルのオブジェクト
description: DMA チャネルのオブジェクト
ms.assetid: 2064bbdf-62b7-454f-8764-b2aa21636c02
keywords:
- ヘルパー オブジェクト WDK オーディオ、DMA チャネル オブジェクト
- DMA チャネル オブジェクトの WDK オーディオ
- マスター デバイス WDK オーディオ
- スレーブ デバイス WDK オーディオ
- IDmaChannel インターフェイス
- チャネル オブジェクトの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c315ea0f58297ba2ab6ec655553e2d14e7def245
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360127"
---
# <a name="dma-channel-objects"></a>DMA チャネルのオブジェクト


## <span id="dma_channel_objects"></span><span id="DMA_CHANNEL_OBJECTS"></span>


PortCls システム ドライバーの実装、 [IDmaChannel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-idmachannel)と[IDmaChannelSlave](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-idmachannelslave) WaveCyclic と WavePci のミニポート ドライバーのためのインターフェイス。 **IDmaChannel** DMA チャネルとその関連する DMA バッファーおよびバッファーの使用状況パラメーターを表します。 WaveCyclic ミニポート ドライバーを使用して、さらに、 **IDmaChannelSlave**下位デバイス DMA チャネルを管理します。 **IDmaChannelSlave**継承**IDmaChannel**します。 制御の DMA 操作については、次を参照してください。[アダプター オブジェクトと DMA](https://docs.microsoft.com/windows-hardware/drivers/kernel/adapter-objects-and-dma)します。

**IDmaChannel**オブジェクトは、次をカプセル化します。

-   マスターまたは下位のデバイス用の DMA チャネル

-   チャネルに関連付けられているデータのバッファー

-   チャネルが使用される方法を説明する情報

ポートおよびミニポート ドライバーでは、DMA チャネルの使用状況に関する情報を通信するために DMA チャネル オブジェクトを使用します。 通常、ミニポート ドライバーは、初期化時またはストリームの作成時に、一連の DMA チャネルを割り当てます。 新しいストリームを作成する際は、ミニポート ドライバーは、ストリームの使用は DMA チャネル オブジェクトをポート ドライバーに指示します。

マスターまたは下位のデバイスには、DMA チャネル オブジェクトを作成できます。

-   下位のデバイスでは、組み込みの DMA ハードウェア機能がないので、デバイスを必要とする任意のデータ転送を実行するシステムの DMA コント ローラーに依存する必要があります。

-   マスターのデバイスでは、バス マスター DMA の独自のハードウェアを使用して、システム バス上のデータ転送を実行します。

下位の DMA チャネル オブジェクトを使用して WaveCyclic デバイスの例は、Sb16 サンプル オーディオ ドライバーで、Microsoft Windows Driver Kit (WDK) を参照してください。 マスター DMA チャネル オブジェクトが、ポートおよびミニポート ドライバー間 DMA チャネルについての情報を共有するための backboard よりも少し。 マスターおよび下位のデバイスの詳細については、次を参照してください。[アダプター オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-adapter-objects)します。

マスターまたは下位のデバイスの DMA チャネル オブジェクトには、次は公開します。

-   アダプター オブジェクト

-   ドライバーと DMA のハードウェアを共有できる 1 つの一般的なバッファー

-   バッファー サイズの値を照会および変更できます。

*アダプター オブジェクト*の DMA アダプターの構造は、*物理デバイス オブジェクト (PDO)* します。 ミニポート ドライバーは、次のメソッドのいずれかを呼び出すことによって、DMA チャネル オブジェクトを作成するときに、アダプター オブジェクトが自動的に作成されます。

[**IPortWavePci::NewMasterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepci-newmasterdmachannel)

[**IPortWaveCyclic::NewMasterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavecyclic-newmasterdmachannel)

[**IPortWaveCyclic::NewSlaveDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavecyclic-newslavedmachannel)

メソッド[ **IDmaChannel::GetAdapterObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-getadapterobject)アダプター オブジェクトへのポインターを取得するために使用できます。

アダプタのドライバを呼び出すことも、 [ **PcNewDmaChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewdmachannel) DMA チャネル オブジェクトを作成する機能が、この関数が使用するよりも難しく、 **IPortWave*Xxx*:: 新規*Xxx*もできます**呼び出すため、呼び出し元は、明示的にデバイス オブジェクトとその他のコンテキスト情報を指定する必要があります。

下位のデバイスでは、DMA チャネルの場合、 [ **IDmaChannel::TransferCount** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-transfercount)メソッドは、最大転送サイズを返します (、 *MapSize*パラメーター) が呼び出しで指定された[ **IDmaChannelSlave::Start**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannelslave-start)します。 また、アダプター オブジェクトを操作して、DMA デバイスのクエリを実行するいくつかのメソッドを提供します。 これらのメソッドのいずれもマスター DMA チャネルで意味のありません。

[**IDmaChannel::AllocateBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-allocatebuffer)と[ **IDmaChannel::FreeBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-freebuffer) DMA チャネル オブジェクトに関連付けられている 1 つの一般的なバッファーを管理するために使用します。 オブジェクトによって割り当てられたバッファー ドライバー (カーネルの仮想メモリのアドレス) と (物理メモリのアドレス) を持つ DMA デバイスの両方にアクセスすることが保証されます。 さらに、バッファーは、物理的に連続するになります。 通常、最適な戦略は、物理的に連続するメモリが十分にある最もミニポート ドライバーの初期化中に、DMA バッファーを割り当てることです。 [**IDmaChannel::AllocatedBufferSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-allocatedbuffersize)への呼び出しで指定されたバッファーのサイズを返します**IDmaChannel::AllocateBuffer**します。

[**IDmaChannel::MaximumBufferSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-maximumbuffersize)のために使用できる実際の最大バッファー サイズを示します。 割り当てのサイズがページ サイズの倍数でない場合は、割り当てサイズを超えるこの可能性があります。 割り当てられているサイズより小さいは、DMA デバイスに割り当てられたサイズの転送をサポートできない場合られます可能性があります。 [**IDmaChannel::BufferSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-buffersize)と[ **IDmaChannel::SetBufferSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-setbuffersize)クエリし、DMA の転送に使用するバッファーのサイズの設定に使用されます。 バッファーが割り当てられると、バッファー サイズが最大バッファー サイズを設定します。 初期化後は、ポート ドライバーとミニポート ドライバーすると、バッファー サイズを変更するか、現在の値を検出する機会があります。 ミニポート ドライバーの結果を使用して**IDmaChannel::BufferSize** DMA チャネルが開始されると、DMA 操作の転送サイズを決定します。 [**IDmaChannel::SystemAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-systemaddress)と[ **IDmaChannel::PhysicalAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-physicaladdress)バッファーの仮想および物理アドレスをそれぞれ取得するために使用します。

[**IDmaChannel::CopyTo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-copyto)と[ **IDmaChannel::CopyFrom** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-copyfrom) DMA バッファーとの間に、サンプル データをコピーします。 WaveCyclic ポート ドライバーでは、アプリケーションのバッファーと、ミニポート ドライバーの循環バッファー間でのオーディオ データをコピーするこれらのメソッドを呼び出します。

必ずしも、DMA バッファーは、ストリーミングされたデータを転送するのには使用されません。 WavePci ポート ドライバーの場合、ストリーミングされたデータに配信 (またはから取得した) スキャッター/ギャザー マッピングの一覧としてミニポート ドライバー。 ただし、ミニポート ドライバーがまだを使用する、DMA バッファーとしてアダプターのドライバーと通信するための共有メモリ領域です。

ポートのドライバーでは、ミニポート ドライバーが DMA チャネルの作成に使用できる機能を提供します。 ポートのドライバーの説明で特に明記されていない限り、ポート ドライバーから割り当てられた DMA オブジェクトを使用する絶対必要はありません。 ポート ドライバーへのポインターだけが必要です、 **IDmaChannel**必要なメソッドをサポートするインターフェイス。 ポートのドライバーを必要とする DMA チャネル メソッドの一覧については、各ポート ドライバーのドキュメントを確認します。

通常、ポート ドライバーでは、DMA チャネル割り当て関数を使用することが最も簡単な方法です。 まれに、ミニポート ドライバー開発者は、特定のアダプターの特別な要件を満たすために、独自の DMA チャネル オブジェクトを実装する必要があります。 これには、新しいオブジェクトの実装もが必要です。 それ以外の時間は、ミニポート ドライバーのストリーム オブジェクトを公開するための十分な**IDmaChannel**インターフェイスし、自体 DMA チャネル メソッドを実装します。

**IDmaChannel**インターフェイスは、次のメソッドをサポートしています。

[**IDmaChannel::AllocateBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-allocatebuffer)

[**IDmaChannel::AllocatedBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-allocatedbuffersize)

[**IDmaChannel::BufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-buffersize)

[**IDmaChannel::CopyFrom**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-copyfrom)

[**IDmaChannel::CopyTo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-copyto)

[**IDmaChannel::FreeBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-freebuffer)

[**IDmaChannel::GetAdapterObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-getadapterobject)

[**IDmaChannel::MaximumBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-maximumbuffersize)

[**IDmaChannel::PhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-physicaladdress)

[**IDmaChannel::SetBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-setbuffersize)

[**IDmaChannel::SystemAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-systemaddress)

[**IDmaChannel::TransferCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-transfercount)

**IDmaChannelSlave**インターフェイスは、拡張**IDmaChannel**次のメソッドを追加します。

[**IDmaChannelSlave::ReadCounter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannelslave-readcounter)

[**IDmaChannelSlave::Start**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannelslave-start)

[**IDmaChannelSlave::Stop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannelslave-stop)

[**IDmaChannelSlave::WaitForTC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannelslave-waitfortc)

 

 




