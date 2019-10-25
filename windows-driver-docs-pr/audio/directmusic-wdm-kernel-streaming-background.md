---
title: DirectMusic WDM カーネル ストリーミングの背景
description: DirectMusic WDM カーネル ストリーミングの背景
ms.assetid: 851fa156-590a-43fb-9c49-df528f0ea608
keywords:
- DirectMusic カーネルモード WDK audio、WDM カーネルストリーミング
- カーネルモード synths WDK audio、WDM カーネルストリーミング
- WDM カーネルストリーミング WDK オーディオ
- カーネルストリーミング WDK オーディオ
- ポートドライバー WDK オーディオ、シンセサイザー
- ハードウェア高速化の WDK オーディオ
- ミニポートドライバー WDK オーディオ、カーネルモードハードウェアアクセラレーション
- シンセサイザー WDK オーディオ、カーネルモードハードウェアアクセラレーション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd3a8f936bc973b1ab722ca9069dad1f897ef0a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833503"
---
# <a name="directmusic-wdm-kernel-streaming-background"></a>DirectMusic WDM カーネル ストリーミングの背景


## <span id="directmusic_wdm_kernel_streaming_background"></span><span id="DIRECTMUSIC_WDM_KERNEL_STREAMING_BACKGROUND"></span>


このセクションは、DirectMusic および WDM カーネルストリーミングを初めて使用するドライバーライターや、カーネルモードアーキテクチャの概要を知りたいすべてのユーザーに役立つ場合があります。 経験豊富な WDM オーディオドライバーの作成者は、[シンセサイザーミニポートドライバーの概要](synthesizer-miniport-driver-overview.md)に進むことができます。 カーネルストリーミングの一般的な概要については、「[カーネルストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming)」を参照してください。

従来、Windows 用のドライバーには次の2種類がありました。

-   Windows 95-スタイルの Vxd

-   NT ベースのオペレーティングシステムのドライバー

Windows 98/Me には、すべての NT カーネルサービスを備え、ほとんどの NT ドライバーを Windows 98/Me で実行できる ntkern が含まれています。 WDM ドライバーは、クロスプラットフォームの互換性のために NT ドライバー環境を使用します。 また、電源管理とプラグアンドプレイも実装しています。

WDM カーネルストリーミングアーキテクチャには、フィルターチェーンの概念がメディアのストリーミングに使用されていた、ActiveMovie のルート (DirectShow) がありました。 チェーン内の各フィルターは、ユーザーモードフィルター、カーネルモードフィルターのプロキシとして使用されるユーザーモードコードの一部、またはハードウェアの一部をマーシャリングするユーザーモードコードの一部にすることができます (詳細については[、「AVStream とカーネルストリーミングプロキシモジュールを使用](https://docs.microsoft.com/windows-hardware/drivers/stream/using-avstream-with-the-kernel-streaming-proxy-module)する」を参照してください). このアーキテクチャは、カーネルストリーミングを作成するために Windows 2000 カーネルに導入されました。

"Pin" の用語は、当初は Microsoft DirectAnimation と DirectShow から取得されています。 ピンは、あるフィルターを別のフィルターに接続するために使用できるターゲットのカーネルストリーミング用語になりました。 たとえば、2つのフィルターがあり、最初のフィルターが "out" ピン、2番目が "in" ピンである場合、最初のフィルターがデータストリームを2番目のフィルターに渡すことができるように、ピンを接続できます。 詳細については、「[オーディオフィルターグラフ](audio-filter-graphs.md)」を参照してください。

カーネルストリーミングが WDM の一部になり、WDM オーディオによって使用されるようになりました。 DirectMusic は、 [WDMAud システムドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)をカーネルモードコンポーネントとして使用し、i/o 要求パケット (irp) の形式でカーネルモードに情報を渡します。 すべての DirectMusic インターフェイスは、厳密には WDM です。

通常、WDM カーネルストリーミングオーディオフィルタチェーンはシステムによって提供されますが、Isv や Ihv が提供することもできます。 [Sysaudio システムドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)は、フィルターチェーンを管理するコンポーネントです。 フィルターを検索し、それらをフックしてフィルターグラフを作成します。 (SysAudio 自体はグラフのメンバーではありません)。

DMus ミニポートドライバーを実装するために、カーネルストリームの専門家である必要はありません。 Microsoft では、ベンダーが DirectMusic のフィルターを簡単に作成するために利用できる、多数の共通コードを提供しています。 ベンダーは、システムによって提供される DMus ポートドライバーの汎用機能を利用するために、ミニポートドライバーを記述できます。 この方法は、他の Windows ドライバーアーキテクチャが使用するクラスドライバー/ミニドライバーモデルに似ています (比較については、「 [WDM オーディオ用語](wdm-audio-terminology.md)」を参照してください)。

WDM オーディオには[PortCls という](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver)コンポーネントがあります。これは、いくつかの種類のオーディオフィルターのクラスドライバーです。 これらのオーディオフィルターは、PCI wave デバイス、巡回 DMA wave デバイス、および MIDI デバイスを処理します。 ドライバーコンポーネントをフィルターやミニフィルターとして、またはドライバーとミニドライバーとして参照するのではなく、ポートおよびミニポートドライバーと呼びます。 PortCls には、などの MIDI ポートドライバーが含まれています。

ポートドライバーごとに、デバイス固有の操作を行うさまざまな種類のミニポートドライバーを使用できます。 たとえば、Windows 98 では、1つの MIDI ポートドライバーがあり、MPU-401 デバイスや FM シンセサイザーデバイスなど、さまざまなミニポートドライバーを接続できます。 ポートドライバーは、FM または MPU デバイスのどちらになるかに関係なく、同じ方法で MIDI データをシーケンス処理します。 ミニポートドライバーは、実際に MIDI データを再生していることの詳細を処理します。

Sequencer は MIDI ポートドライバー自体に含まれているため、期限が切れてから、適切なミニポートドライバーを使用してデータを再生します。 たとえば、MPU-401 ミニポートドライバーは、外部シンセサイザーモジュールを使用して wave データをデバイスに送信します。 ミニポートドライバーの出力は、ポートドライバーの wave シンクによって管理されます。

ミニポートドライバーは、MIDI ノートを格納します。また、MIDI ポートドライバーの一部である wave シンクが次のオーディオデータブロックを要求すると、ミニポートドライバーは、要求された量の wave データを指定されたメモリ位置にレンダリングします。 このプロセスの詳細については、「 [DirectMusic ミニポートドライバーインターフェイス](directmusic-miniport-driver-interface.md)」を参照してください。

Microsoft は、すべての MPUs に対して標準のミニポートドライバー機能を提供しています。 MPU 仕様では、ハードウェアが行う必要があることとその応答方法が明確に定義されているため、Microsoft では、PortCls の一部として MPUs を処理するミニポートドライバーを提供しています。 MPUs を持つすべてのサウンドカードは、同じミニポートドライバーを使用できます。

PortCls の組み込みのミニポートドライバーは、MIDI ポートドライバーにのみ接続されています。そのため、dmf us ポートドライバーが DMus ミニポートドライバーに接続するようになりました。 DMus ポートドライバーは、MIDI シーケンス処理や DirectMusic のその他の機能を処理し、MIDI、wave、ダウンロード可能なサウンド (DLS) データを管理します。 Windows Driver Kit (WDK) のサンプル MPU-401 アダプタードライバーは、DMus ポートドライバーと、PortCls に組み込まれている DMus ミニポートドライバーの1つを使用します。

必要なものが MPU-401 の機能だけである場合は、WDK に付属している、組み込みの mpu401 ミニポートドライバーを使用します。 それを DMus ポートドライバーにバインドし、IRQ を設定するだけです。 以前は、このドライバーは、 **iid\_IPortMidi** (PORTCLS の MIDI ポートドライバー) と**iid\_IMiniportDriverUart** (PortCls に組み込まれている MPU-401 ミニポートドライバー) によって識別された組み込みインターフェイスを参照していました。クラス Guid ( [**Pcnewport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)と[**pcnewport ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport)を参照してください)。 これで、mpu401 ドライバーは、DirectMusic をサポートできるように、 **\_Miniportdriverdマス** **\_の clsid**を参照します。

DMus ポートドライバーが MIDI データを受信すると、データが sequencer にルーティングされ、そのタイムスタンプに基づいて各メモが並べ替えられます。 メモが期限切れになると、sequencer はミニポートドライバーに渡します。 ミニポートドライバーの実装では、これらのメモを事前にプリフェッチするまでの時間を指定できます。

DMus ポートドライバーが、DLS データを含むプロパティ要求を受信すると ( [**Ksk プロパティ\_シンセサイザー\_dls\_ダウンロード**](https://docs.microsoft.com/previous-versions/ff537396(v=vs.85)))、要求を直接ミニポートドライバーにルーティングします。 これらは再生できるだけなので、ダウンロード時に sequencer や wave シンクを含める必要はありません。

 

 




