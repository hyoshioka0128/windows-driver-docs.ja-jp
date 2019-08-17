---
title: シングルルート i/o 仮想化 (SR-IOV) の概要
description: シングルルート i/o 仮想化 (SR-IOV) の概要
ms.assetid: E64DD4F0-D5F8-4FFF-931B-C04C5C42D000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 375d4c235ff4516de07125463e45960519d28fec
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565637"
---
# <a name="introduction-to-single-root-io-virtualization-sr-iov"></a>シングルルート i/o 仮想化 (SR-IOV) の概要


このセクションでは、NDIS シングルルート i/o 仮想化 (SR-IOV) インターフェイスについて説明します。 NDIS 6.30 以降では、SR-IOV インターフェイスは、Windows Server 2012 以降のバージョンの Windows Server で仮想化されたネットワークの Microsoft Hyper-v パフォーマンスの向上をサポートしています。

PCI-SIG の sr-iov 仕様では、複数の仮想マシン (Vm) が同じ PCIe 物理ハードウェアリソースを共有できるようにする PCI Express (PCIe) 仕様スイートの拡張機能を定義します。 このセクションでは、NDIS sr-iov インターフェイスについて説明し、PCIe sr-iov 仕様を実装する SR-IOV 対応のネットワークアダプター用に NDIS ミニポートドライバーを記述する方法について説明します。

ここでは、次のトピックについて説明します。

[シングルルート i/o 仮想化 (SR-IOV) の概要](overview-of-single-root-i-o-virtualization--sr-iov-.md)

[SR-IOV PF ミニポートドライバーを書き込んでいます](writing-sr-iov-pf-miniport-drivers.md)

[SR-IOV VF ミニポートドライバーを書き込んでいます](writing-sr-iov-vf-miniport-drivers.md)

[SR-IOV PF/VF バックチャネル通信](sr-iov-pf-vf-backchannel-communication.md)

[SR-IOV Oid](sr-iov-oids.md)

Sr-iov の詳細については、「PCI SIG の[シングルルート I/o 仮想化と共有 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742)の仕様」を参照してください。

 

 





