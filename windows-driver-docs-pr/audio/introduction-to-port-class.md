---
title: ポート クラスの概要
description: ポート クラスの概要
ms.assetid: 5f986e0c-d021-4dee-85d3-ad69a3708dd8
keywords:
- オーディオのミニポート ドライバー WDK、ポート クラス
- ミニポート ドライバー WDK オーディオ、ポート クラス
- ポート クラス ドライバー WDK オーディオ
- PortCls WDK オーディオ、ミニポート ドライバー
- ポート クラス アダプター ドライバー WDK オーディオ
- アダプターのドライバー WDK オーディオ、ミニポート ドライバー
- ポート ドライバー WDK オーディオ、ミニポート ドライバー
- ポート クラス ライブラリの WDK オーディオ
- ポート ドライバー WDK オーディオ、ポート クラス
- ポート クラス オーディオ アダプター WDK
- ポート ドライバー WDK オーディオ
- PortCls WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50718cd3a4f084e94a267ac30d902af04388fcd8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528501"
---
# <a name="introduction-to-port-class"></a>ポート クラスの概要


## <span id="introduction_to_port_class"></span><span id="INTRODUCTION_TO_PORT_CLASS"></span>


PCI や DMA ベースでのオーディオ デバイスのほとんどのハードウェア ドライバーは、PortCls システム ドライバー (Portcls.sys) からアクセスできるポートをクラス ライブラリに基づいています。 PortCls は、オペレーティング システムの一部として Microsoft を含むオーディオ ポート クラス ドライバーです。 PortCls には、ストリーム配信 (KS) フィルター機能の一般的なカーネルのほとんどを実装しているポート ドライバーのセットが用意されています。 そのため、PortCls は、オーディオ ドライバー開発者のタスクを簡略化します。 ハードウェア ベンダーのみ、オーディオのアダプターのハードウェア固有の関数を処理するために、ミニポート ドライバーのセットを指定する必要があります。

ハードウェア ベンダーには、オーディオ デバイスの場合は、独自 KS フィルターを実装するオプションがありますが、このオプションは難しいと通常のオーディオ デバイスに不要なです。 KS Stream.sys、Stream クラス ドライバー、または Avstream.sys、AVStream クラス ドライバーのいずれかに準拠するようにフィルターを開発することができます。 ただし、Stream.sys に基づいている KS フィルターは AVStream でのみ利用する機能強化を利用できません。 KS フィルターと PortCls についての詳細については、[WDM オーディオ ドライバーの概要](getting-started-with-wdm-audio-drivers.md)を参照してください。

PortCls の内部の実装は、既存のドライバーとの互換性を保持中に、後続の Windows リリースの機能強化をストリーミングするカーネルを活用するために展開できます。

PortCls は Portcls.sys システム ファイルのエクスポート ドライバー (カーネル モード DLL) として実装され、次のものが含まれています。

-   一連のアダプターのドライバーによって呼び出すことができるヘルパー関数

-   コレクション*オーディオ ポート*ドライバー

オーディオ デバイスのハードウェア ベンダーに連絡の役割です、*アダプター ドライバー*します。 アダプターのドライバーには、初期化およびミニポートのドライバー管理コードが含まれています (など、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)関数) のコレクションと*オーディオ ミニポート*ドライバーです。

アダプター ドライバーが読み込まれると、オペレーティング システムとアダプター ドライバー一連のミニポート ドライバー オブジェクトを作成、PortCls システムのドライバーに対応するドライバー オブジェクトのポート セットを作成するように求められます。 (コード例で[サブデバイス作成](subdevice-creation.md)このプロセスを示しています)。これらのポート ドライバーは、通常の Portcls.sys ファイルで使用可能なサブセットです。 各ミニポート ドライバー自体に一致するポート ドライバーのバインドを形成する完全な Portcls.sys*サブデバイス*ドライバー。 組み合わせのポートおよびミニポート サブデバイス ドライバーは、KS フィルター (を参照してください[オーディオ フィルター](audio-filters.md))。 たとえば、通常のアダプターのドライバーには、次の 3 つのミニポート ドライバーが含まれます。WaveRT、DMusUART、およびトポロジ (で[IMiniportWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536737)、 [IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)、および[IMiniportTopology](https://msdn.microsoft.com/library/windows/hardware/ff536712)インターフェイス)。 WaveRT、Dmu、トポロジの各ポート ドライバーを初期化中に、これらのミニポート ドライバーがバインドされている (と[IPortWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536920)、 [IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)、および[IPortTopology](https://msdn.microsoft.com/library/windows/hardware/ff536896)インターフェイス) Portcls.sys ファイルに格納されています。 これらの 3 つのサブデバイス ドライバーのそれぞれは、KS フィルターの形式をとります。 3 つのフィルターは、オーディオのアダプターの完全な機能をまとめて公開します。

通常、ポート、ドライバーは、オーディオ サブデバイスの各クラスの機能の大半を提供します。 たとえば、WaveRT ポート ドライバーは、ミニポート ドライバーは、DMA のアドレスとデバイスの名前などのデバイスに固有の詳細を提供します。 一方、DMA ベースのオーディオ デバイスにオーディオ データをストリームに必要な作業のほとんどは。

オーディオ アダプターおよびミニポートのドライバーは、通常は Microsoft C で記述し、COM インターフェイスの広範に利用します。 ポート ミニポート ドライバーのアーキテクチャでは、モジュール設計を推進します。 派生した C++ クラスとして、ミニポート ドライバーの作成者は、ドライバーを実装する必要があります、 [IMiniport](https://msdn.microsoft.com/library/windows/hardware/ff536698) Portcls.h ヘッダー ファイルで定義されているインターフェイス。 ハードウェア初期化が行われ--ドライバーの読み込み時に通常**Init**のメソッド、 **IMiniport**-派生クラス (たとえば、 [ **IMiniportWaveRT::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536759)). オーディオのミニポート ドライバーの COM の実装の詳細については、[カーネルで COM](com-in-the-kernel.md)を参照してください。

次の図は、ポートおよびミニポート ドライバーと、オーディオ スタック内の位置間のリレーションシップを示しています。

![ポートおよびミニポートのドライバーの間の関係を示す図](images/portcls-diag.png)

上の図では、KSEndpoint コンポーネントは、Windows Vista および Windows の以降のバージョンに付属しているシステムが指定したファイルです。 このコンポーネントは、DLL (Audiokse.dll) の形式で提供されます。 KSEndpoint では、カーネル モード デバイスのエンドポイントを抽象化し、抽象化されたエンドポイントへのアクセス権を持つオーディオ エンジンを提供します。 オーディオ エンジンの詳細については、[、Windows Vista のオーディオ エンジンが調べる](exploring-the-windows-vista-audio-engine.md)を参照してください。

上の図の凡例には、ベンダーが提供するドライバー コンポーネントを表すボックスが表示されます。 各ミニポート ドライバーの上端のインターフェイスがポート、各ドライバーの下端ことに注意してください。 WaveRT ポート ドライバーが公開するなど、 **IPortWaveRT**インターフェイスを公開する WaveRT ミニポート ドライバーを**IMiniportWaveRT**ポート ドライバーへのインターフェイス。 これらのインターフェイスと呼ばれるあります*上端*と*下端*インターフェイス。

ポート クラスと AVStream クラス ドライバーは、同様 WDM ドライバーとそれらの両方が両方ともストリーミング アーキテクチャ WDM カーネルをサポートします。 ただし、ポートのクラス ドライバーは、マルチプロセッサの処理と再入の面で AVStream クラス ドライバーによって異なります。 ポート クラス ドライバーは、次を操作します。

-   3 層のアプローチを組み合わせたクラス ドライバー、ポート ドライバー、およびベンダーから提供されたミニポート ドライバーを使用します。

-   ミニポート ドライバー、オーディオ ハードウェアに近い動作することができます、オーディオの関数の制限された数であります。

-   特定のデバイスにリンクされるようにいくつかのポートまたはミニポート ドライバーを使用できます。 この機能は、多機能のカードのサポートの向上に対するできます。

-   外部バス (USB など) をサポートしていません。 ポートのすべてのドライバーでは、(PCMCIA、および PCI) のシステム バス上に存在するデバイスをサポートします。

WDM オーディオ ポートおよびミニポート ドライバーを記述するための用語は、Windows ドライバーの他のクラスに使用される用語からいくつかの点で異なります。 これらの相違点についてで[WDM オーディオ用語](wdm-audio-terminology.md)します。

このセクションでは、次のトピックについて説明します。

[関数に固有のインターフェイスの実装](implementation-of-function-specific-interfaces.md)

[オペレーティング システムによって PortCls サポート](portcls-support-by-operating-system.md)

 

 




