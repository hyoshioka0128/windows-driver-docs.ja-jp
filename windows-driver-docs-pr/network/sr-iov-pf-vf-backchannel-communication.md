---
title: SR-IOV PF/VF バックチャネル通信
description: SR-IOV PF/VF バックチャネル通信
ms.assetid: 66D40452-1286-449E-BD6B-AFAD466E03A1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1416a113c4563a2c54963b5fc4930d9175cc88c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346038"
---
# <a name="sr-iov-pfvf-backchannel-communication"></a>SR-IOV PF/VF バックチャネル通信


シングル ルート I/O 仮想化 (SR-IOV) のインターフェイスは、通信チャネルを提供します。 または*backchannel*、ミニポート ドライバー、PCI Express (PCIe) 仮想機能 (VF) と PCIe 物理機能 (PF) の間。 各 VF ミニポート ドライバーは、PF ミニポート ドライバーに、バック チャネル経由で要求を発行できます。 PF のミニポート ドライバーは、個々 の VF のミニポート ドライバーのバック チャネル経由で状態の通知を発行できます。

バック チャネル インターフェイスを介して PF と VF のミニポート ドライバーの間で交換されるデータの使用では、 *VF 構成ブロック*します。 各 VF 構成ブロックは、各ブロックに独自の書式設定、長さ、およびブロック識別子がである、プロセス間通信 (IPC) メッセージと似た概念です。 独立系ハードウェア ベンダー (IHV) は、PF と VF ミニポート ドライバーの 1 つ以上の VF 構成ブロックを定義できます。

ここでは、次のトピックについて説明します。

[VF のミニポート ドライバーからのバック チャネル通信](backchannel-communication-from-a-vf-miniport-driver.md)

[PF のミニポート ドライバーからのバック チャネル通信](backchannel-communication-from-the-pf-miniport-driver.md)

 

 





