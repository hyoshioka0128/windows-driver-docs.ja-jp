---
title: シングル ルート I/O 仮想化 (SR-IOV)
description: シングル ルート I/O 仮想化 (SR-IOV)
ms.assetid: E64DD4F0-D5F8-4FFF-931B-C04C5C42D000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b1b288c0c8852a9b54089f269957512fe043f24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559864"
---
# <a name="single-root-io-virtualization-sr-iov"></a>シングル ルート I/O 仮想化 (SR-IOV)


このセクションでは、NDIS シングル ルート I/O 仮想化 (SR-IOV) のインターフェイスについて説明します。 NDIS 6.30 以降、SR-IOV インターフェイスは、Windows Server 2012 およびそれ以降のバージョンの Windows Server 上の仮想化ネットワークの Microsoft HYPER-V のパフォーマンスの向上をサポートします。

Pci-sig SR-IOV 仕様では、複数の仮想マシン (Vm) を同じ PCIe 物理ハードウェア リソースの共有を有効にする PCI Express (PCIe) 仕様のセットを拡張機能を定義します。 このセクションでは、NDIS、SR-IOV インターフェイスについて説明し、PCIe SR-IOV 仕様を実装する SR-IOV 対応のネットワーク アダプターの NDIS ミニポート ドライバーを記述するための手法について説明します。

ここでは、次のトピックについて説明します。

[シングル ルート I/O 仮想化 (SR-IOV) の概要](overview-of-single-root-i-o-virtualization--sr-iov-.md)

[SR-IOV PF ミニポート ドライバーの記述](writing-sr-iov-pf-miniport-drivers.md)

[SR-IOV VF ミニポート ドライバーの記述](writing-sr-iov-vf-miniport-drivers.md)

[SR-IOV PF/VF のバック チャネル通信](sr-iov-pf-vf-backchannel-communication.md)

[SR-IOV の Oid](sr-iov-oids.md)

SR-IOV の詳細については、PCI SIG を参照してください[シングル ルート I/O 仮想化および共有 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742)仕様。

 

 





