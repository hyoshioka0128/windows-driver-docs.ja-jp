---
title: DMA チャネルのオブジェクト
description: DMA チャネルのオブジェクト
ms.assetid: 2064bbdf-62b7-454f-8764-b2aa21636c02
keywords:
- ヘルパーオブジェクト WDK オーディオ、DMA チャネルオブジェクト
- DMA チャネルオブジェクト WDK オーディオ
- マスターデバイス WDK オーディオ
- IDmaChannel インターフェイス
- チャネルオブジェクト WDK オーディオ
ms.date: 06/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: e95aca2d9485a70df9ebedd916b2924d1ccf6618
ms.sourcegitcommit: bd120d96651f9e338956388c618acec7d215b0d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681676"
---
# <a name="dma-channel-objects"></a>DMA チャネルのオブジェクト

> [!NOTE]
> Microsoft は、多様で inclusionary な環境をサポートしています。 このドキュメント内には、"スレーブ" という語への参照があります。 Microsoft のバイアスフリー通信用スタイルガイドでは、これを exclusionary 語として認識しています。 この表現は、現在ソフトウェア内で使用されている用語として使用されています。

PortCls システムドライバーは、WaveCyclic および WavePci ミニポートドライバーの利点を得るために、 [IDmaChannel](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idmachannel)インターフェイスと[IDmaChannelSlave](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idmachannelslave)インターフェイスを実装しています。 **IDmaChannel**は、dma チャネルとそれに関連付けられている dma バッファーおよびバッファー使用法パラメーターを表します。 また、WaveCyclic ミニポートドライバーは、 **IDmaChannelSlave**を使用して下位デバイスの DMA チャネルを管理します。 **IDmaChannelSlave**は**IDmaChannel**から継承します。 DMA 操作の制御の詳細については、「[アダプターオブジェクトと dma](https://docs.microsoft.com/windows-hardware/drivers/kernel/adapter-objects-and-dma)」を参照してください。

**IDmaChannel**オブジェクトは、次のものをカプセル化します。

- マスターデバイスまたは下位デバイスの DMA チャネル

- チャネルに関連付けられているデータバッファー

- チャネルの使用方法を説明する情報

ポートとミニポートドライバーは、dma チャネルオブジェクトを使用して、DMA チャネルの使用状況に関する情報を伝達します。 通常、ミニポートドライバーは、初期化中またはストリームの作成中に、一連の DMA チャネルを割り当てます。 新しいストリームの作成時に、ミニポートドライバーは、ストリームに使用する DMA チャネルオブジェクトをポートドライバーに伝えます。

DMA チャネルオブジェクトは、マスターデバイスまたは下位デバイスに対して作成できます。

- 下位デバイスには DMA ハードウェア機能が組み込まれていないため、デバイスに必要なデータ転送を実行するには、システム DMA コントローラーに依存する必要があります。

- マスターデバイスは、独自のバスマスタリング DMA ハードウェアを使用して、システムバス上でデータ転送を実行します。

下位 DMA チャネルオブジェクトを使用する WaveCyclic デバイスの例については、Microsoft Windows Driver Kit (WDK) の Sb16 サンプルオーディオドライバーを参照してください。 マスタ DMA チャネルオブジェクトは、ポートとミニポートドライバー間の DMA チャネルに関する情報を共有するためのバックボードよりもわずかです。 マスターデバイスと下位デバイスの詳細については、「[アダプターオブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-adapter-objects)」を参照してください。

マスターデバイスまたは下位デバイスの DMA チャネルオブジェクトでは、次のものが公開されます。

- アダプターオブジェクト

- ドライバーと DMA ハードウェアが共有できる1つの共通バッファー

- クエリと変更が可能なバッファーサイズ値

*アダプターオブジェクト*は、*物理デバイスオブジェクト (PDO)* の DMA アダプター構造です。 次のいずれかのメソッドを呼び出すことによって、ミニポートドライバーが DMA チャネルオブジェクトを作成すると、アダプターオブジェクトが自動的に作成されます。

[**IPortWavePci::NewMasterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-newmasterdmachannel)

[**IPortWaveCyclic::NewMasterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-newmasterdmachannel)

[**IPortWaveCyclic::NewSlaveDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-newslavedmachannel)

[**IDmaChannel:: GetAdapterObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-getadapterobject)メソッドを使用して、アダプターオブジェクトへのポインターを取得できます。

アダプタードライバーは、 [**PcNewDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewdmachannel)関数を呼び出して DMA チャネルオブジェクトを作成することもできますが、この関数は、 **IPortWave*Xxx*:: New*xxx*DmaChannel**の呼び出しよりも使用するのが困難です。これは、呼び出し元がデバイスオブジェクトとその他のコンテキスト情報を明示的に指定する必要があるためです。

下位デバイスの DMA チャネルの場合、 [**IDmaChannel:: TransferCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-transfercount)メソッドは、 [**IDmaChannelSlave:: Start**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannelslave-start)の呼び出しで指定された最大転送サイズ ( *mapsize*パラメーター) を返します。 また、アダプターオブジェクトには、DMA デバイスの操作とクエリを実行するためのメソッドが用意されています。 これらの方法のいずれも、マスタ DMA チャネルでは意味がありません。

[**IDmaChannel:: AllocateBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-allocatebuffer)と[**IDmaChannel:: FREEBUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-freebuffer)は、DMA チャネルオブジェクトに関連付けられている単一の共通バッファーを管理するために使用されます。 オブジェクトによって割り当てられたバッファーは、ドライバー (カーネルの仮想メモリアドレスを持つ) と DMA デバイス (物理メモリアドレスを持つ) の両方からアクセスできることが保証されます。 また、バッファーは物理的に連続しています。 通常、最適な方法は、物理的に連続するメモリが最も多くある場合に、ミニポートドライバーの初期化時に DMA バッファーを割り当てることです。 [**IDmaChannel:: AllocatedBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-allocatedbuffersize)は、 **IDmaChannel:: allocatebuffer**の呼び出しで指定されたバッファーのサイズを返します。

[**IDmaChannel:: MaximumBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-maximumbuffersize)は、使用できる実際の最大バッファーサイズを示します。 割り当てられたサイズがページサイズの偶数倍でない場合は、割り当てられたサイズを超える可能性があります。 DMA デバイスで割り当てられたサイズの転送がサポートされていない場合、割り当てられたサイズよりも小さくなることがあります。 [**IDmaChannel:: BufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-buffersize)と[**IDmaChannel:: SETBUFFERSIZE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-setbuffersize)は、DMA 転送に使用するバッファーのサイズを照会および設定するために使用されます。 バッファーが割り当てられると、バッファーサイズは最大バッファーサイズに設定されます。 初期化後、ポートドライバーとミニポートドライバーの両方で、バッファーサイズを変更したり、現在の値を検出したりすることができます。 ミニポートドライバーは、 **IDmaChannel:: BufferSize**の結果を使用して、dma チャネルが開始されたときの dma 操作の転送サイズを決定します。 [**IDmaChannel:: systemaddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-systemaddress)と[**IDmaChannel::P Hysare address**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-physicaladdress)は、バッファーの仮想アドレスと物理アドレスをそれぞれ取得するために使用されます。

[**IDmaChannel:: CopyTo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-copyto)と[**IDmaChannel:: copyfrom**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-copyfrom)サンプルデータを DMA バッファーとの間でコピーします。 WaveCyclic port ドライバーは、これらのメソッドを呼び出して、アプリケーションバッファーとミニポートドライバーの循環バッファーとの間でオーディオデータをコピーします。

DMA バッファーは、ストリーミングされたデータの転送に必ずしも使用されるわけではありません。 WavePci port ドライバーの場合、ストリーミングされたデータは、分散/収集マッピングの一覧としてミニポートドライバーに配信 (または取得) されます。 ただし、ミニポートドライバーは、アダプタードライバーと通信するための共有メモリ領域として DMA バッファーを引き続き使用する場合があります。

ポートドライバーには、DMA チャネルを作成するために使用できる機能を備えたミニポートドライバーが用意されています。 ポートドライバーの説明で特に明記されていない限り、ポートドライバーから割り当てられた DMA オブジェクトを使用する必要はありません。 ポートドライバーは、必要なメソッドをサポートする**IDmaChannel**インターフェイスへのポインターを必要とします。 ポートドライバーが必要とする DMA チャネルメソッドの一覧については、各ポートドライバーのドキュメントを参照してください。

通常、最も簡単な方法は、ポートドライバーが実装する DMA チャネル割り当て関数を使用することです。 まれに、ミニポートドライバーの開発者は、特定のアダプターの特別な要件を満たすために独自の DMA チャネルオブジェクトを実装する必要がある場合があります。 これには、新しいオブジェクトの実装が必要になる場合があります。 それ以外の場合は、ミニポートドライバーのストリームオブジェクトが**IDmaChannel**インターフェイスを公開し、DMA チャネルメソッド自体を実装するだけで十分です。

**IDmaChannel**インターフェイスは、次のメソッドをサポートしています。

[**IDmaChannel:: AllocateBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-allocatebuffer)

[**IDmaChannel::AllocatedBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-allocatedbuffersize)

[**IDmaChannel:: BufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-buffersize)

[**IDmaChannel:: CopyFrom**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-copyfrom)

[**IDmaChannel:: CopyTo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-copyto)

[**IDmaChannel:: FreeBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-freebuffer)

[**IDmaChannel:: GetAdapterObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-getadapterobject)

[**IDmaChannel:: MaximumBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-maximumbuffersize)

[**IDmaChannel::P Hysのアドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-physicaladdress)

[**IDmaChannel:: SetBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-setbuffersize)

[**IDmaChannel:: SystemAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-systemaddress)

[**IDmaChannel:: TransferCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-transfercount)

**IDmaChannelSlave**インターフェイスは、次のメソッドを追加して**IDmaChannel**を拡張します。

[**IDmaChannelSlave:: ReadCounter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannelslave-readcounter)

[**IDmaChannelSlave:: Start**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannelslave-start)

[**IDmaChannelSlave:: Stop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannelslave-stop)

[**IDmaChannelSlave:: WaitForTC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannelslave-waitfortc)

 

 




