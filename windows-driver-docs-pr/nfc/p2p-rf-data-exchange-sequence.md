---
title: RF データ交換シーケンスの P2P
description: 次の図は、StateRfDiscovered と StateRfDataXchg NFC DEP プロトコルの状態のシーケンスを示します。
ms.assetid: FF77D322-47AE-412C-9924-110FB9E8F9F5
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 296717e4a967d7185bf42f07591c0b7cf80c44f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384199"
---
# <a name="p2p-rf-data-exchange-sequence"></a>RF データ交換シーケンスの P2P


次の図は、StateRfDiscovered と StateRfDataXchg NFC DEP プロトコルの状態のシーケンスを示します。 NFC CX 必要 P2P 処理の NFC DEP RF インターフェイスをサポートするために NFCC であることに注意してください。 StateRfDiscovered への移行は、RF インターフェイスのアクティブ化の後に発生します。 複数のリモート エンドポイントまたは StateRfDiscovery で複数のプロトコルでは、場合は、NFC CX は、1 つのエンドポイントを選択します。 NFC-DEP ISO DEP 経由での優先順位は、相互運用性の NFC CX に実装されます。 StateRfDiscovered は、NFC CX がリモート デバイスが LLCP をサポートしているかをチェックする遷移状態です。 P2P モード、StateRfDataXchg 分かれて次の一連の操作: チェックにリモート デバイス LLCP をサポートしている、バインド、リッスン、および既定 SNEP のサーバーに接続を受け入れる場合は、既定のリモート SNEP サーバーへの接続を開きます。 ドライバーは、SNEP コマンドを使用して、アプリケーション レイヤーから使用可能な NDEF メッセージ要求を交換します。

![nfc dep rf データ シーケンスを交換します。](images/nfc-dep-rfdataexchangesequence.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC クラスの拡張機能 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

