---
title: NFCEE 検出シーケンス
ms.assetid: F6894EFD-4140-490B-B0BB-1A9BDA4DCECE
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
description: NFCEE 管理のさまざまな実装をサポートするための2つの操作モードを提供する NFC CX に関する情報。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59764d6422453e5ef191b16b2cac6fc58c3599aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843584"
---
# <a name="nfcee-discovery-sequence"></a>NFCEE 検出シーケンス


NCI 1.0 仕様の制限により、チップセットの製造元は NFCEE 管理のさまざまな実装を持っています。 これらの多様な実装をサポートするために、NFC CX は2つの操作モードを提供します。

-   **STANDARD NCI モード**–このモードでは、NFC CX は nfcc がすべての HCI ネットワークを通報できるようにします。 別の NFCEE\_は、他の方法で NTF\_検出します。 ただし、NFC CX では、この構成で1つの NFCEE をサポートすることが制限されています。 このモードの拡張機能では、NFCC が NFCEE ごとに HCI ネットワークを報告する場合、NFC CX は最初のネットワークを選択し、残りを破棄します。

-   **非標準 NCI モード**–このモードでは、NFC CX は nfcc がすべての HCI ネットワークを報告することを許可します。 また、ネットワーク上の子の NFCEE は、NTF\_DISCOVER\_検出されます。 ただし、この構成をサポートするには、NFC CX に2つの追加要件があります。 NFCEE で報告された\_の数は、子として\_RSP に含まれています。 また、子 NFCCs の HCI は HCI ホスト Id と一致している必要があります (標準では、UICC ホスト ID を0x2 にする必要があります)。

この構成での NFCCs のほとんどの実装では、NFCEE\_DISCOVER\_RSP の HCI network NFCEEID のみが報告されます。 ただし、NFC CX は実際の数を認識しないため、検出プロセスが完了した時点を特定できません。 NFC クライアントドライバーには、通常、報告する追加の技術を知るための独自のメカニズムがあります。 そのため、この要件を満たすために、NFC クライアントドライバーがトランスポート処理を使用して、応答の追加のために他の方法を追加するための小さな回避策を実装する必要があります。

![非標準の nci nfcee 検出シーケンス](images/nonstandardnci-nfceediscoverysequence.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
