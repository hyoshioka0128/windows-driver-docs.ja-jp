---
title: Windows カーネルモード I/O マネージャー
description: Windows カーネルモード I/O マネージャー
ms.assetid: 8652f37d-0ece-4c08-9bce-499f0fedb0dd
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9e96566d4fd0d59f5fe539321c0b195d1947defe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358026"
---
# <a name="windows-kernel-mode-io-manager"></a>Windows カーネルモード I/O マネージャー


コンピューターは、入力と出力 (I/O)、外部との間に提供するさまざまなデバイスで構成されます。 代表的なデバイスは、キーボード、マウス、コント ローラーのオーディオ、ビデオ コント ローラー、ディスク ドライブ、ネットワーク ポート、およびなどです。 デバイス ドライバーは、ソフトウェアのデバイスとオペレーティング システムの間の接続を提供します。 このため、I/O は、デバイス ドライバーのライターに非常に重要です。

Windows カーネル モードの I/O マネージャーは、アプリケーションとデバイス ドライバーが提供するインターフェイス間の通信を管理します。 デバイスがオペレーティング システムが一致しない速度で動作、ため、オペレーティング システムとデバイス ドライバーの間の通信は主に I/O 要求パケット (Irp) を通じて行われます。 これらのパケットは、ネットワーク パケットや Windows メッセージのパケットに似ています。 特定のドライバーをオペレーティング システムと別の 1 つのドライバーから渡されます。

Windows I/O システムでは、スタックと呼ばれる階層化ドライバー モデルを提供します。 通常 Irp は 1 つのドライバーからの通信を容易に同じスタック内の別のに移動します。 たとえば、ジョイスティック ドライバーがコンピューターのハードウェアの残りの部分に、PCI バス経由で通信する必要がありますし、USB ホスト コント ローラーと通信する必要がありますに USB ハブとの通信には必要があります。 スタックは、ジョイスティック ドライバー、USB ハブ、USB ホスト コント ローラー、および PCI バスで構成されます。 この通信は、各ドライバー スタック送信することで調整され、Irp を受信します。

強調することはできません、十分には、ドライバーが送信し、を効率的に動作するスタック全体を適時に Irp を受信する必要があります。 ドライバー スタックの一部であるとは正しく受信、処理、および情報を渡す場合、ドライバーが原因でシステムがクラッシュします。

Irp の詳細については、次を参照してください。 [Irp の処理](handling-irps.md)します。

ドライバー スタックの詳細については、次を参照してください。[デバイス オブジェクトとデバイス スタック](device-objects-and-device-stacks.md)します。

I/O の管理に関連する techiques をプログラミングするには、次を参照してください。 [I/O マネージャー プログラミング手法](i-o-programming-techniques.md)します。

I/O マネージャーに直接インターフェイスを提供するルーチンには文字で、通常、プレフィックス"**Io**"。 たとえば、 **IoCreateDevice**します。 I/O マネージャー ルーチンの一覧は、次を参照してください。 [I/O マネージャー ルーチン](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551797(v=vs.85))します。

IRP に関連するルーチンの一覧は、次を参照してください。 [Irp](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

I/O マネージャーが 2 つのサブコンポーネント: プラグ アンド プレイのマネージャーと電源マネージャー。 プラグ アンド プレイし、電源管理のテクノロジの I/O 機能を管理します。 プラグ アンド プレイの管理の詳細については、次を参照してください。 [Windows カーネル モードのプラグ アンド プレイ Manager](windows-kernel-mode-plug-and-play-manager.md)と電源管理の詳細については、次を参照してください。 [Windows カーネル モードの電源マネージャー](windows-kernel-mode-power-manager.md)します。

 

 




