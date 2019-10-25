---
title: RF 検出シーケンス
description: 次の図は、検出を開始するために NFC CX によって実行される一連の NCI 操作を示しています。
ms.assetid: 392F8A06-262D-4CF9-B510-C3FE86291026
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fb19b87ab12200f532f816aaa7f838c062a1ddf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834017"
---
# <a name="rf-discovery-sequence"></a>RF 検出シーケンス


次の図は、検出を開始するために NFC CX によって実行される一連の NCI 操作を示しています。 StateRfIdle から入力された StateRfDiscovery は、開始 RF 検出シーケンスをトリガーします。 この状態で実行される主な操作のセットは、RF 検出パラメーターの構成、リッスンモードルーティングテーブルのオプションの構成、RF discover NCI コマンドを使用した探索の有効化です。 NFC クライアントドライバーでは、SequencePreRfDiscStart を使用して、非標準の NCI コマンドを追加して、検出プロセスを最適化できます。

![検出を開始するために NFC CX によって実行される NCI 操作を示すシーケンス図](images/staterfdiscoverysequence.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

