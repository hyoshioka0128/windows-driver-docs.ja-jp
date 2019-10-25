---
title: NCI のパケットの処理
description: 場合によっては、NFC CX によって定義されたシーケンスが、NFC クライアントドライバーがそのカスタムロジックを追加するのに十分でない可能性があります。
ms.assetid: 48BD5100-A1D4-4844-B53A-DAC73FDBB089
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 668e3ca49c98070b6e2f65a77084712c354001e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831570"
---
# <a name="nci-packet-handling"></a>NCI のパケットの処理


場合によっては、NFC CX によって定義されたシーケンスが、NFC クライアントドライバーがそのカスタムロジックを追加するのに十分でない可能性があります。 このような場合、すべての NCI パケットが nfc クライアントドライバー (トランスポート層との通信を処理する) を介して nfc CX によって交換されるので、これにより、NFC クライアントドライバーは、NCI パケットをCX と NFCC によって交換される標準の NCI パケット。 ただし、「シーケンス拡張」セクションで指定されている要件 (1) と (2) に加えて、この機能拡張ポイントを利用する場合、NFC クライアントドライバーは次の要件を満たしている必要があります。

-   これらの追加の NCI パケットの交換が完了すると、NFC クライアントドライバーは、 [**Nfccxncireadnotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxncireadnotification)コールバックを介して、nfc CX によって送信された NCI コマンドに関連付けられた応答と通知を送信する必要があります。

-   チャネルごとのフロー制御は、NFC CX の論理チャネル管理で実行されるため、NFC クライアントドライバーは、これに影響を与えるロジックを実行してはなりません。 そのため、NFC クライアントドライバーは、その情報を使用せずに、CX によって開かれた論理チャネル上で、追加のデータパケットを送信しないことをお勧めします。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

