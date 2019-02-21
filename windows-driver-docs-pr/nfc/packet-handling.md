---
title: NCI のパケットの処理
description: 場合によっては、NFC CX によって定義されたシーケンスの NFC クライアント ドライバー、カスタム ロジックを追加するための十分なしない場合があります。
ms.assetid: 48BD5100-A1D4-4844-B53A-DAC73FDBB089
keywords:
- NFC
- 通信の近く
- proximity
- フィールドの近接近く
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5fb6a55e4820016de798c535a1b6745c5260ae0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538176"
---
# <a name="nci-packet-handling"></a>NCI のパケットの処理


場合によっては、NFC CX によって定義されたシーケンスの NFC クライアント ドライバー、カスタム ロジックを追加するための十分なしない場合があります。 このような場合は、NCI のすべてのパケットが交換されるため、NFC CX (トランスポート層とやり取りを処理) する NFC クライアント ドライバーによって NFC コント ローラーとでは、これにより、NFC クライアント ドライバーの間での他の NCI パケットを挿入する機会CX および NFCC で交換される標準の NCI パケット。 ただし、NFC のクライアント ドライバーでは、次の要件は満たさ要件以外にもこの機能拡張ポイントを利用する場合 (1) と (2)、シーケンスの機能拡張で指定したを確認する必要があります。

-   NFC クライアント ドライバーで応答とを通じて NFC CX によって送信された NCI コマンドに関連付けられた通知を送信する必要がこれらの追加 NCI パケットの交換が完了したら、 [ **NfcCxNciReadNotification**](https://msdn.microsoft.com/library/windows/hardware/dn905613)コールバック。

-   NFC CX の論理のチャネルの管理で、チャネルごとのフロー制御が実行されるため、NFC のクライアント ドライバーは、これには影響を与えるロジックを実行しないでください。 そのため、NFC のクライアント ドライバーがその知識がなくても、CX によって開かれた論理のチャネルでの追加のデータ パケットを送信しないことをお勧めします。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC クラスの拡張機能 (CX) リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

