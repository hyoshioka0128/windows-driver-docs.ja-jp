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
ms.openlocfilehash: 92f1fd3dafd4d6c324589f1575a873945bcdce4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578645"
---
# <a name="rf-discovery-sequence"></a>RF 検出シーケンス


次の図は、探索を開始するために、NFC CX によって実行される NCI 操作のシーケンスを示しています。 StateRfIdle から入力 StateRfDiscovery RF 探索シーケンスを開始をトリガーします。 この状態で実行される操作の主なセットは、RF 検出のパラメーターの構成のオプションの構成は、ルーティング テーブル、モードをリッスン、NCI のコマンドを検出、RF での探索を有効にするとします。 NFC のクライアント ドライバーは、SequencePreRfDiscStart を使用して、検出プロセスを最適化するために非標準の NCI コマンドを追加できます。

![探索を開始するために、NFC CX によって実行される、NCI の操作を表すシーケンス図](images/staterfdiscoverysequence.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC クラスの拡張機能 (CX) リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

