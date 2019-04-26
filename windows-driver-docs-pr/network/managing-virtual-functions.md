---
title: 仮想関数の管理
description: 仮想関数の管理
ms.assetid: 6B08B04D-C9A1-4159-9866-D179012191B2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31e39ae46525a657d36145ab137d2f78645c7975
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343520"
---
# <a name="managing-virtual-functions"></a>仮想関数の管理


このセクションでは、シングル ルート I/O 仮想化 (SR-IOV) をサポートするネットワーク アダプターの要件および PCI Express (PCIe) の仮想機能 (Vf) を管理するためのガイドラインについて説明します。

ここでは、次のトピックについて説明します。

[仮想関数の初期化と破棄の概要](overview-of-virtual-function-initialization-and-teardown.md)

[仮想関数のリソースの割り当て](allocating-resources-for-a-virtual-function.md)

[仮想関数のリソースの解放](freeing-resources-for-a-virtual-function.md)

[ネットワーク アダプターに仮想関数を列挙します。](enumerating-virtual-functions-on-a-network-adapter.md)

[仮想関数のパラメーターのクエリを実行します。](querying-the-parameters-of-a-virtual-function.md)

[仮想関数の PCI 構成領域へのアクセス](accessing-the-pci-configuration-space-of-a-virtual-function.md)

[仮想関数の電源状態の設定](setting-the-power-state-of-a-virtual-function.md)

[仮想関数をリセットします。](resetting-a-virtual-function.md)

SR-IOV 対応ネットワーク アダプターの VFs の詳細については、次を参照してください。 [SR-IOV 仮想機能 (Vf)](sr-iov-virtual-functions--vfs-.md)します。

**注**  だけで、PF ミニポート ドライバーは Vf などのネットワーク アダプターのハードウェア リソースを構成できます。 VF のミニポート ドライバーでは、SR-IOV 対応のアダプターのハードウェア リソースのほとんどを直接アクセスできません。 詳細については、次を参照してください。[書き込み SR-IOV VF ミニポート ドライバー](writing-sr-iov-vf-miniport-drivers.md)します。

 

 

 





