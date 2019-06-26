---
title: NFC クライアント ドライバーの電源の管理要件
ms.assetid: FBA0821B-859F-4A44-998E-E00162FBD265
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
description: コネクト スタンバイの NFP デバイスの要件を満たすについて説明します。 プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 740b1f070e12955636d8ede47df663fd782e328a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383575"
---
# <a name="nfc-client-driver-power-management-requirements"></a>NFC クライアント ドライバーの電源の管理要件


NFC クライアント ドライバーでは、D0 と D3 の能力を NFP プラットフォームのデバイスをコネクテッド スタンバイの要件を満たすために、次のようにコールバックを処理を実装する必要があります。

-   NFC のクライアント ドライバーは、ドライバーが、D3 から送信されているときにことを確認する必要があります&gt;d0 が 100 ミリ秒未満で再開できます。 これは、NFC 操作が上で画面を切り替えるには、すぐに場所に取るようにします。

-   NFC のクライアント ドライバーは、電力消費量が D3 状態のときに 1mW より小さいことを確認もする必要があります。 これは、画面がオフのときに重要な電力消費量がないようにします。

これらの目標を満たすためには、次は NFC クライアント ドライバーの推奨されます。

-   電源削除または電源を切ったハードに移動してこれらの要件を満たす NFC コント ローラーはお勧めします NFC クライアント ドライバーでは、D0 の中に、チップセットを再初期化&gt;D3 し d3 -&gt; D0 遷移します。

-   NFC を修正プログラムを必要とするコント ローラーをダウンロードして非揮発性 (ベースの RAM) がないのため、メモリ D0 の中にスタンバイ モードを無効にして NFC クライアント ドライバーを有効にするお勧めします&gt;D3 および D3 -&gt; D0 遷移それぞれします。 完全な初期化が D3Final - からときに (HostActionStart) が行われて&gt;D0 - から際 D0 と後処理 (HostActionStop) に行われますが&gt;D3Final します。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC クラスの拡張機能 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
