---
title: ポート クラスの概要
description: ポート クラスの概要
ms.assetid: 5f986e0c-d021-4dee-85d3-ad69a3708dd8
keywords:
- オーディオミニポートドライバー WDK、ポートクラス
- ミニポートドライバー WDK オーディオ、ポートクラス
- ポートクラスドライバー WDK オーディオ
- PortCls WDK オーディオ、ミニポートドライバー
- ポートクラスアダプタードライバー WDK オーディオ
- アダプタードライバー WDK オーディオ、ミニポートドライバー
- ポートドライバー WDK オーディオ、ミニポートドライバー
- ポートクラスライブラリ WDK オーディオ
- ポートドライバー WDK オーディオ、ポートクラス
- ポートクラスオーディオアダプター WDK
- ポートドライバー WDK オーディオ
- PortCls WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b19c47194ff3b4c6631102f7db8615d0620cc90
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833200"
---
# <a name="introduction-to-port-class"></a>ポート クラスの概要


## <span id="introduction_to_port_class"></span><span id="INTRODUCTION_TO_PORT_CLASS"></span>


PCI および DMA ベースのオーディオデバイス用のほとんどのハードウェアドライバーは、PortCls システムドライバー (Portcls) を介してアクセスできるポートクラスライブラリに基づいています。 PortCls は、Microsoft がオペレーティングシステムの一部として含むオーディオポートクラスのドライバーです。 PortCls には、汎用カーネルストリーミング (KS) フィルター機能のほとんどを実装する一連のポートドライバーが用意されています。 そのため、PortCls は、オーディオドライバーの開発者のタスクを簡略化します。 ハードウェアベンダーは、オーディオアダプターのハードウェア固有の機能を処理するために、一連のミニポートドライバーを提供するだけで済みます。

ハードウェアベンダーには、オーディオデバイス用に独自の KS フィルターを実装するオプションがありますが、一般的なオーディオデバイスでは、このオプションは困難であり、不要です。 KS フィルターを開発して、Stream、Stream クラスドライバー、または Avstream. sys (AVStream クラスドライバー) のいずれかに準拠させることができます。 ただし、.sys に基づく KS フィルターでは、AVStream でのみ使用できる機能強化を利用できません。 KS フィルターと PortCls の詳細については、「[はじめにと WDM オーディオドライバー](getting-started-with-wdm-audio-drivers.md)」を参照してください。

PortCls の内部実装は、既存のドライバーとの互換性を維持しながら、連続した Windows リリースでカーネルストリームの機能強化を利用できるように発展させることができます。

PortCls は、Portcls システムファイルにエクスポートドライバー (カーネルモード DLL) として実装され、次の項目が含まれています。

-   アダプタードライバーによって呼び出すことができるヘルパー関数のセット

-   *オーディオポート*ドライバーのコレクション

*アダプタードライバー*を提供するには、オーディオデバイスのハードウェアベンダーが責任を負う必要があります。 アダプタードライバーには、初期化とミニポートのドライバー管理コード ( [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)機能を含む) と*オーディオミニポート*ドライバーのコレクションが含まれています。

オペレーティングシステムがアダプタドライバを読み込むと、アダプタドライバは一連のミニポートドライバオブジェクトを作成し、PortCls システムドライバに対応する一連のポートドライバオブジェクトを作成するように要求します。 ([サブデバイスの作成](subdevice-creation.md)のコード例では、このプロセスを示しています)。これらのポートドライバーは、通常、Portcls ファイルで使用できるもののサブセットです。 各ミニポートドライバーは、Portcls の一致するポートドライバーにそれ自体をバインドして、完全な*サブデバイス*ドライバーを形成します。 ポートとミニポートのサブデバイスドライバーの組み合わせは KS フィルターです (「[オーディオフィルター](audio-filters.md)」を参照してください)。 たとえば、一般的なアダプタードライバーには、WaveRT、Dマス Uart、およびトポロジ ( [](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert)、 [IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)、および[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)インターフェイスを使用) という3つのミニポートドライバーが含まれている場合があります。 初期化中に、これらのミニポートドライバーは、Portcls ファイルに格納されている WaveRT、DMus、およびトポロジポートドライバー ( [IPortWaveRT](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavert)、 [iportdmus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)、および[iporttopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)インターフェイス) にバインドされます。 これら3つのサブデバイスドライバーは、それぞれ KS フィルターの形式をとります。 これら3つのフィルターにより、オーディオアダプターの完全な機能が公開されます。

通常、ポートドライバーは、オーディオサブデバイスの各クラスの機能の大部分を提供します。 たとえば、WaveRT ポートドライバーは、オーディオデータを DMA ベースのオーディオデバイスにストリーミングするために必要なほとんどの作業を実行します。一方、ミニポートドライバーは、DMA アドレスやデバイス名などのデバイス固有の詳細情報を提供します。

オーディオアダプターのドライバーとミニポートドライバーは、通常C++ 、Microsoft で作成され、COM インターフェイスを広範囲に使用します。 ポートミニポートドライバーのアーキテクチャによって、モジュールの設計が促進されます。 ミニポートドライバーの作成者は、 C++ [IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)インターフェイスから派生したクラスとしてドライバーを実装する必要があります。これは、ヘッダーファイル Portcls で定義されています。 ハードウェアの初期化は、ドライバーの読み込み時に行われます。通常は、 **IMiniport**派生クラス (たとえば、 [**IMiniportWaveRT:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavert-init)) の**Init**メソッドで実行されます。 オーディオミニポートドライバーの COM 実装の詳細については、「[カーネル内の com](com-in-the-kernel.md)」を参照してください。

次の図は、ポートとミニポートドライバーの関係と、オーディオスタック内のそれらの位置を示しています。

![ポートとミニポートドライバーの関係を示す図](images/portcls-diag.png)

前の図では、Ksk エンドポイントコンポーネントは、Windows Vista 以降のバージョンの Windows に付属するシステム提供のファイルです。 このコンポーネントは、DLL (Audiokse .dll) の形式で提供されます。 Ksk エンドポイントは、カーネルモードのデバイスエンドポイントを抽象化し、抽象化されたエンドポイントにアクセスできるようにオーディオエンジンを提供します。 オーディオエンジンの詳細については、「 [Windows Vista オーディオエンジンの](exploring-the-windows-vista-audio-engine.md)操作」を参照してください。

上の図の凡例には、ベンダーが提供するドライバーコンポーネントを表すボックスが示されています。 各ミニポートドライバーの上端が各ポートドライバーの下部にあることに注意してください。 たとえば、 **Wavert**ポートドライバーは、ポートドライバーへの**IMiniportWaveRT**インターフェイスを公開する wavert ミニポートドライバーへのインターフェイスを公開します。 これらのインターフェイスは、*エッジ*インターフェイスと*下位*インターフェイスと呼ばれることもあります。

ポートクラスと AVStream クラスドライバーは両方とも WDM ドライバーであり、両方とも WDM カーネルストリーミングアーキテクチャをサポートしています。 ただし、ポートクラスドライバーは、マルチプロセッサ処理と再入の領域で AVStream クラスドライバーとは異なります。 Port クラスドライバーは、次の処理を行います。

-   クラスドライバー、ポートドライバー、およびベンダーが提供するミニポートドライバーを組み合わせた3層のアプローチを使用します。

-   オーディオ機能の数が制限されており、ミニポートドライバーがオーディオハードウェアに近い動作を可能にします。

-   特定のデバイスに対して、複数のポートまたはミニポートドライバーのリンクを許可します。 この機能により、多機能カードのサポートが強化されます。

-   外部バス (USB など) はサポートしていません。 すべてのポートドライバーは、システムバス (PCMCIA および PCI) 上に存在するデバイスをサポートしています。

WDM オーディオポートとミニポートドライバーを記述するための用語は、Windows ドライバーの他のクラスで使用される用語とは異なる点があります。 これらの違いについては、「 [WDM オーディオ用語](wdm-audio-terminology.md)」で説明しています。

このセクションでは、次のトピックについて説明します。

[関数固有のインターフェイスの実装](implementation-of-function-specific-interfaces.md)

[オペレーティングシステムによる PortCls のサポート](portcls-support-by-operating-system.md)

 

 




