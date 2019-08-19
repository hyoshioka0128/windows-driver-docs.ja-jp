---
title: SR-IOV PF/VF バックチャネル通信の概要
description: SR-IOV PF/VF バックチャネル通信の概要
ms.assetid: 66D40452-1286-449E-BD6B-AFAD466E03A1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 973626fc5f4a19a39892412b1c0797bba06d5dd1
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565636"
---
# <a name="sr-iov-pfvf-backchannel-communication-overview"></a>SR-IOV PF/VF バックチャネル通信の概要


シングルルート i/o 仮想化 (SR-IOV) インターフェイスは、PCI Express (PCIe) 仮想機能 (VF) と PCIe 物理機能 (PF) のミニポートドライバーの間に通信チャネル ( *backchannel*) を提供します。 各 VF ミニポートドライバーは、バックチャネル経由で PF ミニポートドライバーに要求を発行できます。 PF ミニポートドライバーは、バックチャネル経由で個別の VF ミニポートドライバーに状態通知を発行できます。

Backchannel インターフェイス経由で PF および VF ミニポートドライバー間で交換されるデータには、 *VF 構成ブロック*を使用する必要があります。 各 VF 構成ブロックは、概念的にはプロセス間通信 (IPC) メッセージと似ていますが、各ブロックには専用の形式、長さ、ブロック識別子があります。 独立系ハードウェアベンダー (IHV) は、PF および VF ミニポートドライバー用に1つまたは複数の VF 構成ブロックを定義できます。

ここでは、次のトピックについて説明します。

[VF ミニポートドライバーからのバックチャネル通信](backchannel-communication-from-a-vf-miniport-driver.md)

[PF ミニポートドライバーからのバックチャネル通信](backchannel-communication-from-the-pf-miniport-driver.md)

 

 





