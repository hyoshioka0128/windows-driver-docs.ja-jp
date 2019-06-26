---
title: RF 検出シーケンス
description: 次の図は、探索を開始するために、NFC CX によって実行される NCI 操作のシーケンスを示しています。
ms.assetid: 392F8A06-262D-4CF9-B510-C3FE86291026
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40a312190e7d84499c2ecc1940fdbfd5dcf07599
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386510"
---
# <a name="rf-discovery-sequence"></a>RF 検出シーケンス


次の図は、探索を開始するために、NFC CX によって実行される NCI 操作のシーケンスを示しています。 StateRfIdle から入力 StateRfDiscovery RF 探索シーケンスを開始をトリガーします。 この状態で実行される操作の主なセットは、RF 検出のパラメーターの構成のオプションの構成は、ルーティング テーブル、モードをリッスン、NCI のコマンドを検出、RF での探索を有効にするとします。 NFC のクライアント ドライバーは、SequencePreRfDiscStart を使用して、検出プロセスを最適化するために非標準の NCI コマンドを追加できます。

![探索を開始するために、NFC CX によって実行される、NCI の操作を表すシーケンス図](images/staterfdiscoverysequence.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC クラスの拡張機能 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

