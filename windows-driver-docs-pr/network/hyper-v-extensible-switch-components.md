---
title: HYPER-V 拡張可能スイッチのコンポーネント
description: HYPER-V 拡張可能スイッチのコンポーネント
ms.assetid: 510A4D75-8DB4-46D7-BA54-248ED4FEC349
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cff31c4e67ebb02218729c2cc1afa4914bce076
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560214"
---
# <a name="hyper-v-extensible-switch-components"></a>HYPER-V 拡張可能スイッチのコンポーネント


Windows Server 2012 以降、HYPER-V 拡張可能スイッチは NDIS フィルター ドライバーのためのインターフェイスをサポートしています (と呼ばれる*HYPER-V 拡張可能スイッチの拡張機能*)、拡張可能スイッチ ドライバー スタック内でバインドします。 これにより、拡張機能を監視、変更、および拡張可能スイッチ ポートにパケットを転送できます。 これは、drop、リダイレクトすると、または HYPER-V パーティションによって使用されるポートにパケットを送信する拡張機能もできます。

拡張機能は、個々 の拡張可能スイッチのポートまたはスイッチ自体の上にパケット トラフィックに適用されるポリシーをプロビジョニングできます。 これにより、送信または送信されるパケットを拒否するパケットを許可する拡張機能です。

次の図は、NDIS 6.40 (Windows Server 2012 R2) と後で拡張可能スイッチ インターフェイスのコンポーネントを示しています。

![説明する図ハイパー\-ndis 6.40 およびそれ以降の v 拡張可能スイッチのアーキテクチャ](images/vswitcharchitecture-ndis640.png)

次の図は、NDIS 6.30 (Windows Server 2012) の拡張可能スイッチのインターフェイスのコンポーネントを示します。

![sr-iov 対応の合成デバイスのデータ パスを示す図](images/vswitcharchitecture.png)

このセクションには、拡張可能スイッチのコンポーネントを記述する次のトピックが含まれています。

[HYPER-V 拡張可能スイッチの拡張機能](hyper-v-extensible-switch-extensions.md)

[HYPER-V 拡張可能なスイッチ ポート](hyper-v-extensible-switch-ports.md)

[HYPER-V 拡張可能スイッチのネットワーク アダプター](hyper-v-extensible-switch-network-adapters.md)

[HYPER-V 拡張可能なスイッチ ポートとネットワーク アダプターの状態](hyper-v-extensible-switch-port-and-network-adapter-states.md)

 

 





