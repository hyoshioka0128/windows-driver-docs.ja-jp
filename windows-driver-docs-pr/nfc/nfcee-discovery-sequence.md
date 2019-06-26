---
title: NFCEE 検出シーケンス
ms.assetid: F6894EFD-4140-490B-B0BB-1A9BDA4DCECE
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
description: NFCEE 管理のさまざまな実装をサポートするために操作の 2 つのモードを提供する NFC CX について説明します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6b532c0ba21ed19bc52285309675407ab80af9e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383558"
---
# <a name="nfcee-discovery-sequence"></a>NFCEE 検出シーケンス


チップセット メーカーでは、NCI 1.0 仕様の制限、により NFCEE 管理のさまざまな実装があります。 これらのさまざまな実装をサポートするためには、NFC CX には、2 つの操作モードが用意されています。

-   **標準の NCI モード**– このモードで NFC CX により、すべての NFCEEs の 1 つの HCI ネットワークを報告する NFCC。 個別 NFCEE がない\_DISCOVER\_の他の NFCEEs NTF します。 NFC CX は、ただし、この構成では 1 つ NFCEE をサポートするために制限されます。 NFCC NFCEE、NFC CX あたり HCI ネットワークが報告された場合、このモードの拡張機能は、最初の選択し、残りを破棄します。

-   **非標準の NCI モード**– このモードで NFC CX により、すべての NFCEEs の 1 つの HCI ネットワークを報告する NFCC します。 また、その NFCEE で別々 にネットワーク上で子 NFCEEs を報告\_DISCOVER\_NTF します。 ただし、NFC CX には、この構成をサポートするための 2 つの追加要件があります。 NFCEE NFCEEs の数が報告される\_DISCOVER\_RSP がはるかに子 NFCEEs を含めます。 また、子 NFCCs の NFCEEIDs は HCI のホスト Id を一致する必要があります (HCI 標準には、ある 0x2 UICC ホスト ID が必要です)。

この構成で NFCCs のほとんどの実装が HCI のネットワークでその NFCEE NFCEEID のみをレポート\_DISCOVER\_RSP します。 ただし、NFC CX は実際の数を認識しないため、その検出プロセスが完了したときを判断できません。 NFC クライアント ドライバーには、通常、報告が追加 NFCEEs を把握する独自のメカニズムがあります。 そのため、NFC クライアント ドライバーできます実装を処理するトランスポートで、ちょっとした回避策を追加するこの要件を満たすために、応答に追加 NFCEEs します。

![非標準 nci nfcee 探索シーケンス](images/nonstandardnci-nfceediscoverysequence.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC クラスの拡張機能 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
