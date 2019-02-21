---
title: DirectMusic WDM カーネル ストリーミングの背景
description: DirectMusic WDM カーネル ストリーミングの背景
ms.assetid: 851fa156-590a-43fb-9c49-df528f0ea608
keywords:
- DirectMusic カーネル モード WDK オーディオ、WDM カーネル ストリーミング
- カーネル モード シンセサイザー WDK オーディオ、WDM カーネル ストリーミング
- WDK オーディオをストリーミング WDM カーネル
- WDK オーディオのストリーミング カーネル
- ポート ドライバー WDK のオーディオ、シンセサイザー
- ハードウェア アクセラレータ WDK オーディオ
- ミニポート ドライバー WDK オーディオ、カーネル モード ハードウェア アクセラレーション
- シンセサイザー WDK オーディオ、カーネル モードのハードウェア アクセラレーション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7455e72d9240e6158ec1adf80945fff7f67b1dde
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553191"
---
# <a name="directmusic-wdm-kernel-streaming-background"></a>DirectMusic WDM カーネル ストリーミングの背景


## <span id="directmusic_wdm_kernel_streaming_background"></span><span id="DIRECTMUSIC_WDM_KERNEL_STREAMING_BACKGROUND"></span>


このセクションでは、DirectMusic および WDM カーネルのストリーミング、または、任意のユーザー カーネル モードのアーキテクチャの概要を簡単に新しいドライバー作成者に便利な可能性があります。 経験豊富な WDM オーディオ ドライバー作成者をスキップする[シンセサイザー ミニポート ドライバーの概要](synthesizer-miniport-driver-overview.md)します。 カーネルのストリーミングに全般的な概要については、次を参照してください。[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff560842)します。

従来は、2 つの種類の Windows のドライバーがありました。

-   Windows 95 スタイル Vxd

-   NT ベースのオペレーティング システム用のドライバー

Windows 98 NT カーネルは、サービスのでき、Windows 98 で実行するほとんどの NT ドライバーすべてが含まれて、私が含まれています//me. WDM ドライバーは、クロス プラットフォームの互換性のため、NT ドライバー環境を使用します。 電源管理とプラグ アンド プレイも実装します。

ストリーミング アーキテクチャ WDM カーネルが起源 (なった DirectShow) ActiveMovie、フィルターのチェーンの概念がメディアのストリーミングに使用されました。 チェーン内の各フィルターにはユーザー モードのフィルター、カーネル モードのフィルターでは、プロキシとして提供されるユーザー モード コードの一部、またはハードウェアをマーシャ リングされたユーザー モード コードの一部も可能性があります (を参照してください[カーネル ストリーミング プロキシを使用して AVStreamモジュール](https://msdn.microsoft.com/library/windows/hardware/ff568671))。 このアーキテクチャをカーネルのストリーミングを作成するには、Windows 2000 カーネルられました。

ピン留めする の用語は Microsoft できるようになりますし、DirectShow 最初由来します。 Pin は 1 つのフィルターの別の接続に使用できるターゲットのカーネル ストリーミングの用語でですようになりました。 たとえば、場合-"out"pin の最初の 2 つのフィルターがある、2 番目は、"in"暗証番号 (pin)--ピン接続できますできるように、最初のフィルターは、2 番目のフィルターにデータのストリームを渡すことができます。 詳細については、次を参照してください。[オーディオ フィルター グラフ](audio-filter-graphs.md)します。

カーネルのストリーミング、WDM の一部になったし、WDM オーディオによって使用されます。 DirectMusic を使用して、 [WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)カーネル モード コンポーネントとしてその情報を渡して I/O 要求パケット (Irp) の形式でのカーネル モードにします。 すべての DirectMusic インターフェイスは厳密に WDM です。

ストリーミング オーディオ フィルター チェーン WDM カーネルはシステム標準は、通常は、Isv および ihv 側で提供することもできます。 [SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)はフィルターのチェーンを管理するコンポーネントです。 フィルターを検索し、フィルター グラフを作成してそれらをフックします。 (SysAudio 自体は、グラフのメンバーである)。

Dmu ミニポート ドライバーを実装するためにカーネル ストリーミングのエキスパートである必要はありません。 Microsoft は、ベンダーこと DirectMusic の書き込みフィルターを簡単に活用できる、大規模な一連の一般的なコードを提供します。 ベンダーはさせる、ミニポート ドライバーを記述できます Dmu ポートのシステムによって提供されるドライバーの汎用的な機能を使用します。 この方法は他の Windows のドライバーのアーキテクチャを使用して、クラス ドライバー/ミニドライバーのモデルに似ています (比較については、次を参照してください。 [WDM オーディオ用語](wdm-audio-terminology.md))。

WDM オーディオ PortCls と呼ばれるコンポーネントがあります (を参照してください[ポート クラスのアダプターのドライバーと PortCls システム ドライバー](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver))、これは、いくつかの種類のオーディオ フィルター用のクラス ドライバー。 これらのオーディオ フィルターは、PCI wave デバイス、DMA wave 循環的なデバイスは、MIDI デバイスを処理します。 フィルターとミニ フィルターとして、またはドライバーとミニドライバー ドライバー コンポーネントを参照ではなく参照するポートおよびミニポートのドライバーとして。 PortCls には、たとえば、MIDI ポート ドライバーが含まれます。

各ポート ドライバーの場合、デバイスに固有の操作を行うミニポート ドライバーのさまざまな種類があります。 たとえば、Windows 98、MIDI ポートの 1 つのドライバーがあるし、片方と FM シンセサイザー デバイスなど、さまざまなミニポート ドライバーを接続できます。 ポートのドライバーでは、FM または MPU デバイスにこれはかどうかに関係なく同じ方法で MIDI データがシーケンスします。 ミニポート ドライバーでは、実際には、MIDI データの再生の詳細を処理します。

Sequencer が MIDI ポート ドライバー自体にあるためは、期限に達すると、その後、それを適切なミニポート ドライバーを使用するまで、タイムスタンプ付きデータを保持します。 たとえば、片方のミニポート ドライバーでは、外部のシンセサイザーのモジュールを使用してデバイスを wave データを送信します。 ミニポート ドライバーの出力は、ポート ドライバーのウェーブ シンクによって管理されます。

MIDI メモのミニポート ドライバーを格納し、ミニポート ドライバーが指定されたメモリ位置に wave データの要求の量をレンダリング MIDI ポート ドライバーの一部では、wave シンクは、オーディオ データの次のブロックが表示されたら、します。 このプロセスの詳細については、次を参照してください。 [DirectMusic ミニポート ドライバー インターフェイス](directmusic-miniport-driver-interface.md)します。

Microsoft では、すべて Mpu の標準のミニポート ドライバーの機能を提供します。 MPU 仕様は、ハードウェアで行う必要があり、応答方法を正確に定義するため、Microsoft は PortCls の一部として Mpu を処理するために、ミニポート ドライバーを提供します。 Mpu があるすべてのサウンド カードには、この同じミニポート ドライバーを使用できます。

PortCls DirectMusic Dmu のミニポート ドライバーにアタッチする Dmu ポート ドライバーを導入するための MIDI ポート ドライバーにのみ接続されている組み込みミニポート ドライバー。 Dmu ポート ドライバーでは、DirectMusic の MIDI シーケンス処理とその他の関数を処理し、MIDI、wave、およびダウンロード可能なサウンド (DL) データを管理します。 サンプルの片方のアダプター ドライバーの Windows Driver Kit (WDK) では、Dmu ポート ドライバーと PortCls に組み込まれている Dmu ミニポート ドライバーのいずれかを使用します。

片方の機能に必要な場合は、WDK に付属する組み込み mpu401.sys ミニポート ドライバーを使用します。 Dmu ポート ドライバーにバインドし、IRQ を設定するだけです。 以前は、このドライバーはによって識別された組み込みのインターフェイスを参照されている、 **IID\_IPortMidi** (PortCls で MIDI ポート ドライバー) と**IID\_IMiniportDriverUart**(PortCls に組み込まれている片方ミニポート ドライバー) クラス Guid (を参照してください[ **PcNewPort** ](https://msdn.microsoft.com/library/windows/hardware/ff537715)と[ **PcNewMiniport** ](https://msdn.microsoft.com/library/windows/hardware/ff537714)). Mpu401.sys ドライバーを次に、参照、 **CLSID\_PortDMus**と**CLSID\_MiniportDriverDMusUART** Guid を DirectMusic をサポートできるようにします。

Dmu ポート ドライバーでは、MIDI のデータを受信すると、そのタイムスタンプに基づいて各メモが並べ替えられると、sequencer をデータをルーティングします。 メモが、sequencer は、ミニポート ドライバーに渡します。 ミニポート ドライバーの実装は、これらの注意事項をプリフェッチする事前にどの程度に指定できます。

Dmu ポート ドライバーが DLS データを含むプロパティ要求を受信すると (を参照してください[ **KSPROPERTY\_シンセサイザー\_DLS\_ダウンロード**](https://msdn.microsoft.com/library/windows/hardware/ff537396))、要求を直接ルーティングミニポート ドライバー。 だけのサウンドを再生可能なため、これらは、ダウンロードされたときに、sequencer または wave シンクを含める必要がありません。

 

 




