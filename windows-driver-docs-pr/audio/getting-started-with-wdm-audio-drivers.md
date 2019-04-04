---
title: WDM オーディオ ドライバーの概要
description: Windows Driver Model (WDM) オーディオ ドライバーの作成は、カーネルのカーネル モードで動作し、オペレーティング システムの一部である (KS) コンポーネントをストリームの使用します。
ms.assetid: 573a9b6d-6c50-40a6-9241-470ab418eb66
keywords:
- WDM オーディオ ドライバー WDK
- オーディオ ドライバー WDK、オーディオ ドライバーについて
- WDM オーディオ ドライバー WDK、WDM オーディオ ドライバーについて
- ベンダーから提供されたドライバー WDK オーディオ
- カスタム オーディオ ドライバー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17b668ad57b5c6bdb7f2f27afb70f677ff32ac3b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553196"
---
# <a name="wdm-audio-drivers-overview"></a>WDM オーディオ ドライバーの概要


[Windows Driver Model](https://msdn.microsoft.com/library/windows/hardware/ff565698) (WDM) オーディオ ドライバーの使用、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff560842)(KS) コンポーネントは、カーネル モードで動作し、オペレーティング システムの一部であります。

ハードウェア ベンダーは、Windows ベースのオーディオ ハードウェア デバイスの開発を開始する前にいくつかの設計に関する決定事項を作成する必要があります。

最初の意思決定は、ベンダーから提供されたカスタム ドライバーを必要とするオーディオ デバイスを設計するかどうか。 Windows には、Microsoft に準拠する PCI、USB、および IEEE 1394 のデバイスのオペレーティング システムのサポートが含まれています。[ユニバーサル オーディオ アーキテクチャ](universal-audio-architecture.md)(UAA) ガイドライン。 仕入先は、UAA と互換性のあるオーディオ デバイスのカスタム ドライバーを提供する必要はありません。

ただし、ベンダーから提供されたカスタム オーディオ ドライバーが必要な場合、ベンダーによって必要があります、PortCls システム ドライバー (Portcls.sys) または AVStream クラスのシステム ドライバー (Ks.sys) と連携して動作するドライバーを設計するかどうかを選択します。 PortCls と AVStream の両方は、Windows オペレーティング システムの一部です。 PortCls は、ほとんどのオーディオ アダプターに対して適切な選択です。 PortCls の詳細については、[ポート クラスの概要](introduction-to-port-class.md)を参照してください。 AVStream の詳細については、[AVStream の概要](https://msdn.microsoft.com/library/windows/hardware/ff554240)を参照してください。

PortCls を使用するカスタム アダプターのドライバーを設計するとき、オーディオ アダプター上のデバイスは WaveRT を使用してアプリケーションで使用されます。 詳細については、[WaveRT ポート ドライバー導入](introducing-the-wavert-port-driver.md)を参照してください。

2 つの決定事項には、アダプターのオーディオ アプリケーションへのトポロジと pin のデータ範囲を表示する方法が含まれます。 トポロジは、データ パスとアダプター回路内のコントロールのノードの論理のマップです。 データの範囲は、デバイスは、wave と MIDI ストリームでサポートできるデータ形式を指定します。 両方の決定は、アプリケーションにオーディオ アダプター上のデバイスを表示する方法に影響します。

すべて決定する前に説明したときに、ハードウェア ベンダーは、その実装のコストとパフォーマンスの向上の値を比較検討する必要があります。 別の考慮事項は、特定のソリューションをさまざまな Windows ファミリの製品に機能できるかどうか。 このセクションでは、特定のトピックについての詳細なドキュメントへの参照もこれらの問題の概要を示します。

ここでは、次のトピックについて説明します。

[ユニバーサルのオーディオのアーキテクチャ](universal-audio-architecture.md)

[オーディオ信号の処理モード](audio-signal-processing-modes.md)

[カスタム オーディオ ドライバー](custom-audio-drivers.md)

[トポロジを指定します。](specifying-the-topology.md)

[暗証番号 (pin) のデータ範囲を指定します。](specifying-pin-data-ranges.md)

 

 




