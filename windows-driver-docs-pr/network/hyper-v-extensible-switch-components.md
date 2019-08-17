---
title: Hyper-v 拡張可能スイッチコンポーネントの概要
description: Hyper-v 拡張可能スイッチコンポーネントの概要
ms.assetid: 510A4D75-8DB4-46D7-BA54-248ED4FEC349
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4aa27402d33432b827e7861c8e36e7d0979aa4a
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565764"
---
# <a name="hyper-v-extensible-switch-components-overview"></a>Hyper-v 拡張可能スイッチコンポーネントの概要


Windows Server 2012 以降では、Hyper-v 拡張可能スイッチは、NDIS フィルタードライバー ( *hyper-v 拡張可能スイッチ拡張機能*) が拡張可能なスイッチドライバースタック内でバインドできるようにするインターフェイスをサポートしています。 これにより、拡張可能なスイッチポートにパケットを監視、変更、および転送できます。 これにより、拡張機能によって、Hyper-v パーティションで使用されるポートに対してパケットの削除、リダイレクト、発信を行うことができます。

拡張機能は、拡張可能な個々のスイッチポートまたはスイッチ自体を介してパケットトラフィックに適用されるポリシーを使用してプロビジョニングできます。 これにより、パケットの送信またはパケットの送信を拒否する拡張が可能になります。

次の図は、NDIS 6.40 (Windows Server 2012 R2) およびそれ以降の拡張可能スイッチインターフェイスのコンポーネントを示しています。

![ndis 6.40 以降\-の hyper-v 拡張可能スイッチアーキテクチャを示す図](images/vswitcharchitecture-ndis640.png)

次の図は、NDIS 6.30 (Windows Server 2012) 用の拡張可能スイッチインターフェイスのコンポーネントを示しています。

![sr-iov を使用した統合デバイスデータパスを示す図](images/vswitcharchitecture.png)

このセクションには、拡張可能なスイッチコンポーネントについて説明する次のトピックが含まれています。

[Hyper-v 拡張可能スイッチ拡張機能](hyper-v-extensible-switch-extensions.md)

[Hyper-v 拡張可能スイッチポート](hyper-v-extensible-switch-ports.md)

[Hyper-v 拡張可能スイッチネットワークアダプター](hyper-v-extensible-switch-network-adapters.md)

[Hyper-v 拡張可能スイッチポートとネットワークアダプターの状態](hyper-v-extensible-switch-port-and-network-adapter-states.md)

 

 





