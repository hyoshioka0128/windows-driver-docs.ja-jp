---
title: 仮想関数の PCI 構成領域へのアクセス
description: 仮想関数の PCI 構成領域へのアクセス
ms.assetid: 727E6FC5-F61F-4CB0-B6EB-9B372F2C59E1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 529a8dcfd23614f9edf881302cb5209b6f9644ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367951"
---
# <a name="accessing-the-pci-configuration-space-of-a-virtual-function"></a>仮想関数の PCI 構成領域へのアクセス


このセクションでは、PCI Express (PCIe) 仮想機能 (Vf) の PCI 構成領域からデータにアクセスするためのガイドラインについて説明します。 VFs では、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターのハードウェア機能です。

ここでは、次のトピックについて説明します。

[仮想関数の PCI 構成データを照会します。](overview-of-virtual-function-initialization-and-teardown.md)

[仮想関数の PCI 構成データの設定](allocating-resources-for-a-virtual-function.md)

SR-IOV 対応ネットワーク アダプターの VFs の詳細については、次を参照してください。 [SR-IOV 仮想機能 (Vf)](sr-iov-virtual-functions--vfs-.md)します。

**注**  だけで、PF ミニポート ドライバーは VF の PCI 構成領域を構成できます。 VF のミニポート ドライバーは、ほとんどの構成領域の PCI などの SR-IOV 対応のアダプターのハードウェア リソースに直接アクセスできません。 詳細については、次を参照してください。[書き込み SR-IOV VF ミニポート ドライバー](writing-sr-iov-vf-miniport-drivers.md)します。

 

 

 





