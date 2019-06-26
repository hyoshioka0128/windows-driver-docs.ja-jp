---
title: NCI のパケットの処理
description: 場合によっては、NFC CX によって定義されたシーケンスの NFC クライアント ドライバー、カスタム ロジックを追加するための十分なしない場合があります。
ms.assetid: 48BD5100-A1D4-4844-B53A-DAC73FDBB089
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c039455cd70cfbfa972f563fc4ef82ec5f7174c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373817"
---
# <a name="nci-packet-handling"></a>NCI のパケットの処理


場合によっては、NFC CX によって定義されたシーケンスの NFC クライアント ドライバー、カスタム ロジックを追加するための十分なしない場合があります。 このような場合は、NCI のすべてのパケットが交換されるため、NFC CX (トランスポート層とやり取りを処理) する NFC クライアント ドライバーによって NFC コント ローラーとでは、これにより、NFC クライアント ドライバーの間での他の NCI パケットを挿入する機会CX および NFCC で交換される標準の NCI パケット。 ただし、NFC のクライアント ドライバーでは、次の要件は満たさ要件以外にもこの機能拡張ポイントを利用する場合 (1) と (2)、シーケンスの機能拡張で指定したを確認する必要があります。

-   NFC クライアント ドライバーで応答とを通じて NFC CX によって送信された NCI コマンドに関連付けられた通知を送信する必要がこれらの追加 NCI パケットの交換が完了したら、 [ **NfcCxNciReadNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxncireadnotification)コールバック。

-   NFC CX の論理のチャネルの管理で、チャネルごとのフロー制御が実行されるため、NFC のクライアント ドライバーは、これには影響を与えるロジックを実行しないでください。 そのため、NFC のクライアント ドライバーがその知識がなくても、CX によって開かれた論理のチャネルでの追加のデータ パケットを送信しないことをお勧めします。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC クラスの拡張機能 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

