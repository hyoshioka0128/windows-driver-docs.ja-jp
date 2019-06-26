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
ms.openlocfilehash: 4475e8a39f2c999e3c534e05926cf40cbb5dcb72
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360025"
---
# <a name="wdm-audio-drivers-overview"></a>WDM オーディオ ドライバーの概要


[Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model) (WDM) オーディオ ドライバーの使用、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming)(KS) コンポーネントは、カーネル モードで動作し、オペレーティング システムの一部であります。

ハードウェア ベンダーは、Windows ベースのオーディオ ハードウェア デバイスの開発を開始する前にいくつかの設計に関する決定事項を作成する必要があります。

最初の意思決定は、ベンダーから提供されたカスタム ドライバーを必要とするオーディオ デバイスを設計するかどうか。 Windows には、Microsoft に準拠する PCI、USB、および IEEE 1394 のデバイスのオペレーティング システムのサポートが含まれています。[ユニバーサル オーディオ アーキテクチャ](universal-audio-architecture.md)(UAA) ガイドライン。 仕入先は、UAA と互換性のあるオーディオ デバイスのカスタム ドライバーを提供する必要はありません。

ただし、ベンダーから提供されたカスタム オーディオ ドライバーが必要な場合、ベンダーによって必要があります、PortCls システム ドライバー (Portcls.sys) または AVStream クラスのシステム ドライバー (Ks.sys) と連携して動作するドライバーを設計するかどうかを選択します。 PortCls と AVStream の両方は、Windows オペレーティング システムの一部です。 PortCls は、ほとんどのオーディオ アダプターに対して適切な選択です。 PortCls の詳細については、次を参照してください。[ポート クラスの概要](introduction-to-port-class.md)します。 AVStream の詳細については、次を参照してください。 [AVStream の概要](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-overview)します。

PortCls を使用するカスタム アダプターのドライバーを設計するとき、オーディオ アダプター上のデバイスは WaveRT を使用してアプリケーションで使用されます。 詳細については、次を参照してください。 [WaveRT ポート ドライバー導入](introducing-the-wavert-port-driver.md)します。

2 つの決定事項には、アダプターのオーディオ アプリケーションへのトポロジと pin のデータ範囲を表示する方法が含まれます。 トポロジは、データ パスとアダプター回路内のコントロールのノードの論理のマップです。 データの範囲は、デバイスは、wave と MIDI ストリームでサポートできるデータ形式を指定します。 両方の決定は、アプリケーションにオーディオ アダプター上のデバイスを表示する方法に影響します。

すべて決定する前に説明したときに、ハードウェア ベンダーは、その実装のコストとパフォーマンスの向上の値を比較検討する必要があります。 別の考慮事項は、特定のソリューションをさまざまな Windows ファミリの製品に機能できるかどうか。 このセクションでは、特定のトピックについての詳細なドキュメントへの参照もこれらの問題の概要を示します。

ここでは、次のトピックについて説明します。

[ユニバーサルのオーディオのアーキテクチャ](universal-audio-architecture.md)

[オーディオ信号の処理モード](audio-signal-processing-modes.md)

[カスタム オーディオ ドライバー](custom-audio-drivers.md)

[トポロジを指定します。](specifying-the-topology.md)

[暗証番号 (pin) のデータ範囲を指定します。](specifying-pin-data-ranges.md)

 

 




