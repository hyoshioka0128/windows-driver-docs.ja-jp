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
ms.openlocfilehash: 77af743b4f9469cc1e7db9048dd9242368301e7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348436"
---
# <a name="p2p-rf-data-exchange-sequence"></a>RF データ交換シーケンスの P2P


次の図は、StateRfDiscovered と StateRfDataXchg NFC DEP プロトコルの状態のシーケンスを示します。 NFC CX 必要 P2P 処理の NFC DEP RF インターフェイスをサポートするために NFCC であることに注意してください。 StateRfDiscovered への移行は、RF インターフェイスのアクティブ化の後に発生します。 複数のリモート エンドポイントまたは StateRfDiscovery で複数のプロトコルでは、場合は、NFC CX は、1 つのエンドポイントを選択します。 NFC-DEP ISO DEP 経由での優先順位は、相互運用性の NFC CX に実装されます。 StateRfDiscovered は、NFC CX がリモート デバイスが LLCP をサポートしているかをチェックする遷移状態です。 P2P モード、StateRfDataXchg 分かれて次の一連の操作: チェックにリモート デバイス LLCP をサポートしている、バインド、リッスン、および既定 SNEP のサーバーに接続を受け入れる場合は、既定のリモート SNEP サーバーへの接続を開きます。 ドライバーは、SNEP コマンドを使用して、アプリケーション レイヤーから使用可能な NDEF メッセージ要求を交換します。

![nfc dep rf データ シーケンスを交換します。](images/nfc-dep-rfdataexchangesequence.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC クラスの拡張機能 (CX) リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

