---
title: RF データ交換シーケンスの P2P
description: 次の図は、NFC-DEP プロトコルの StateRfDiscovered および StateRfDataXchg の状態シーケンスを示しています。
ms.assetid: FF77D322-47AE-412C-9924-110FB9E8F9F5
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 339531ecf27a1ba8b6904b8ea8118fabb31853c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845265"
---
# <a name="p2p-rf-data-exchange-sequence"></a>RF データ交換シーケンスの P2P


次の図は、NFC-DEP プロトコルの StateRfDiscovered および StateRfDataXchg の状態シーケンスを示しています。 NFC CX では、P2P 処理のために NFC-DEP RF インターフェイスをサポートするために NFCC が必要であることに注意してください。 検出された StateRfDiscovered 遷移は、RF インターフェイスのアクティブ化の後に発生します。 StateRfDiscovery に複数のリモートエンドポイントまたは複数のプロトコルがある場合、NFC CX は単一のエンドポイントを選択します。 NFC の優先-DEP を使用した DEP は、相互運用性を向上させるために、NFC CX に実装されています。 StateRfDiscovered は、リモートデバイスで LLCP がサポートされているかどうかを NFC CX がチェックする移行状態です。 P2P モードでは、StateRfDataXchg は次の一連の操作に分割されます。リモートデバイスが LLCP をサポートしているかどうかを確認し、既定の SNEP サーバーで接続を受信して受け入れる、リモートの既定の SNEP サーバーへの接続を開きます。 ドライバーは、SNEP コマンドを使用して、アプリケーションレイヤーから利用可能なすべての NDEF メッセージ要求を交換します。

![nfc-dep rf データ交換シーケンス](images/nfc-dep-rfdataexchangesequence.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

