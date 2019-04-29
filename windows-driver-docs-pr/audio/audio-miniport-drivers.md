---
title: オーディオ ミニポート ドライバー
description: オーディオ ミニポート ドライバー
ms.assetid: cf52759e-5da6-41a2-994d-4be15de9ae3d
keywords:
- WDM オーディオ ドライバー WDK、ミニポート ドライバー
- オーディオ ドライバー WDK、ミニポート ドライバー
- オーディオのミニポート ドライバー WDK
- ミニポート ドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fc4006cd8350c30671975755beb639b32ac7e1b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331462"
---
# <a name="audio-miniport-drivers"></a>オーディオ ミニポート ドライバー


## <span id="audio_miniport_drivers"></span><span id="AUDIO_MINIPORT_DRIVERS"></span>


このセクションでは、オーディオのミニポート ドライバー インターフェイスについて説明し、システム バス経由でのレジスタは、システムのプロセッサに直接アクセスできるオーディオ ハードウェア用のアダプター ドライバーを開発する方法について説明します。 このクラス ハードウェアにはには、すべての ISA/DMA、PCMCIA、および PCI オーディオ アダプターが含まれています。

このドキュメントでは、外部バス上に存在するオーディオ デバイスをサポートする方法は説明しません。 外部バス上のオーディオ デバイスのサポートについては、次を参照してください。 [USBAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)と[AVCAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#avcaudio_class_system_driver)します。

次の説明では、リーダーがカーネル (KS) の概念をストリームに精通している前提としています。 背景情報は、次を参照してください。[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff560842)します。

WDM オーディオ ドライバー モデルは、KS フィルターの実装をポートおよびミニポートのドライバーは相互に補完が個別に分割します。 この部門では、オーディオ ハードウェア ドライバーが書き込みフィルターの一般的な実装の問題デバイスに固有のハードウェア インターフェイスの問題からを分離することで簡単です。 ハードウェア ベンダーが、ハードウェア デバイスを直接制御するミニポート ドライバーを記述は、KS フィルターを実装するポート ドライバーがオペレーティング システムで提供されています。 ポートおよびミニポート ドライバーでは、ソフトウェアを適切に定義されたインターフェイスを介して互いと通信します。

ミニポート ドライバーの開発のさまざまな側面は、次のトピックについて説明します。

[ポート クラスの概要](introduction-to-port-class.md)

[デバイスをサポートしています。](supporting-a-device.md)

[COM のカーネル](com-in-the-kernel.md)

[アダプターのドライバーの構築](adapter-driver-construction.md)

[オペレーティング システムによってミニポート ドライバーの種類](miniport-driver-types-by-operating-system.md)

[ミニポート インターフェイス](miniport-interfaces.md)

[ポート クラス オーディオ アダプターをインストールします。](installing-a-port-class-audio-adapter.md)

[ポート ドライバー ヘルパー オブジェクト](port-driver-helper-objects.md)

[オーディオ デバイスの電源管理](power-management-for-audio-devices.md)

[オーディオ ドライバーのバージョン番号](version-numbers-for-audio-drivers.md)

[その他のオーディオ ドライバーの実装の問題](other-implementation-issues-for-audio-drivers.md)

 

 




