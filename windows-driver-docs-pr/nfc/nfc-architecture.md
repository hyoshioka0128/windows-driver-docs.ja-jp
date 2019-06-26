---
title: NFC のアーキテクチャ
description: Windows 上の NFC スタックの大まかなアーキテクチャの図は、後でさらに表示されます。 NFC UMDF ドライバーでは、この仕様で説明されている Ddi を実装します。
ms.assetid: 0FA2BE92-05E1-40D1-AD1D-AE9ADF425E67
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 382be44e5d0b65bb3235b1d2eb3fd2efa49a12c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383580"
---
# <a name="nfc-architecture"></a>NFC のアーキテクチャ


Windows 上の NFC スタックの大まかなアーキテクチャの図は、後でさらに表示されます。 NFC UMDF ドライバーでは、この仕様で説明されている Ddi を実装します。

-   [フィールドの近接 DDI をほぼ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)– 近接メッセージを渡す近接メッセージの交換をピア ツー ピアとの受信など、NFC タグからデータを書き込む提供パブリッシュ/サブスクライブ機能。
-   [要素 DDI をセキュリティで保護された](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)– NFC コント ローラーに接続されているセキュリティで保護された要素 (SEs) を列挙するためにアクセスを提供します、により、セキュリティで保護されたリーダーの外部に公開される要素および NFCC とアプレットから上位の層へのイベントの転送を許可しても構成および NFC チップ リッスン モードのルーティング構成の管理へのアクセスを提供します。 アクセスも提供 ISO/IEC を送受信するデバイスをリモートにリッスン モードで 7816 4 Apdu します。
-   [スマート カード DDI](https://docs.microsoft.com/previous-versions/dn905601(v=vs.85)) – 出発/カード到着をリッスンできるようにスマート カードと対話するための低レベル アクセスを提供します、により、スマート カードへの転送を要求でき、スマート カードの情報を取得します。
-   [無線管理 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index) – 近接 (P2P および読み取り/書き込みモード) とセキュリティで保護された要素 (カードのエミュレーション モード) のオプションの状態を設定するコントロール パネル (CPL) アプリケーションへのアクセスを提供します。

![アプリケーションから最下部から上、ユーザー モード サービス、UMDF ドライバー、カーネル モード、ハードウェアの NFC スタックを示すフローチャートです。](images/nfcarchitecture.png)

 

 
## <a name="related-topics"></a>関連トピック
 [NFC デバイス ドライバー インターフェイス (DDI) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
 
