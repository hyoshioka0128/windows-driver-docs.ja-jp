---
title: NFC のアーキテクチャ
description: Windows での NFC スタックのアーキテクチャの概要図を以下に示します。 NFC UMDF ドライバーは、この仕様で説明されている DDIs を実装します。
ms.assetid: 0FA2BE92-05E1-40D1-AD1D-AE9ADF425E67
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e3ca359cba07b01e056dffe1f2670872be9eb5b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841696"
---
# <a name="nfc-architecture"></a>NFC のアーキテクチャ


Windows での NFC スタックのアーキテクチャの概要図を以下に示します。 NFC UMDF ドライバーは、この仕様で説明されている DDIs を実装します。

-   [近距離無線近接性 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) –近接メッセージ受け渡し用の発行/サブスクライブ機能を提供します。これには、近接メッセージのピアツーピア交換、NFC タグからのデータの受信と書き込みが含まれます。
-   [Secure ELEMENT DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) – NFC コントローラーに接続されているセキュリティで保護された要素 (SEs) を列挙するためのアクセスを提供し、セキュリティで保護された要素を外部閲覧者に公開し、nfcc とアプレットから上位のレイヤーにイベントを転送できるようにします。また、NFC チップのリッスンモードルーティング構成を構成および管理するためのアクセス。 また、リッスンモードで ISO/IEC 7816-4 APDUs を受信し、リモートデバイスに送信するためのアクセスも提供します。
-   [スマートカード DDI](https://docs.microsoft.com/previous-versions/dn905601(v=vs.85)) –カードの到着や出発をリッスンする機能、スマートカードへの要求の送信、スマートカード情報の取得を許可するなど、スマートカードと対話するための低レベルのアクセスを提供します。
-   [ラジオ管理 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) –コントロールパネル (CPL) アプリケーションにアクセスして、近接 (P2P および reader/writer モード) および secure 要素 (カードエミュレーションモード) の無線状態を設定します。

![一番上にあるアプリケーションから開始される NFC スタックと、ユーザーモードサービス、UMDF ドライバー、カーネルモード、ハードウェア下部のハードウェアを説明するフローチャート。](images/nfcarchitecture.png)

 

 
## <a name="related-topics"></a>関連トピック
 [NFC デバイス ドライバー インターフェイス (DDI) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
 
