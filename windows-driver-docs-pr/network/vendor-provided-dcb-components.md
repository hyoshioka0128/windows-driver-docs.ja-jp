---
title: ベンダー提供の DCB コンポーネント
description: ベンダー提供の DCB コンポーネント
ms.assetid: 864BB701-352A-4F61-934C-3E4E8EEE02C5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7c0d9a528753533e56946315f5f962c10a644c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530062"
---
# <a name="vendor-provided-dcb-components"></a>ベンダー提供の DCB コンポーネント


このセクションでは、NDIS サービスの品質 (QoS) のアーキテクチャの IEEE 802.1 データ センター ブリッジング (DCB) の一部である、さまざまなコンポーネントについて説明します。 これらのコンポーネントは、次の図に表示されます。

![デバイスのインストール コンポーネント](images/dcb.png)

相手先ブランド供給 (Oem) の提供し、する独立系ハードウェア ベンダー (Ihv) ダイアグラム表す DCB コンポーネントで、網掛けボックスします。 次の一覧には、これらのコンポーネントについて説明します。

<a href="" id="link-layer-discovery-protocol--lldp--agent"></a>リンク層探索プロトコル (LLDP) エージェント  
以降では、Windows Server 2012、IEEE 802.1 qaz をサポートするベンダー DCB Exchange (DCBX) プロトコルは DCBX を実行する IEEE 802.1Qab LLDP プロトコルのサポートを提供できます。 この LLDP サポートは、ミニポート ドライバーまたは LLDP エージェントのいずれかを指定できます。

通常、LLDP エージェントと DCB 対応のミニポート ドライバーが、プライベートなコントロール パス経由で通信プライベート I/O 制御 (IOCTL) などのインターフェイスです。

LLDP エージェントをベンダーに提供する場合、エージェントがユーザー モード ネットワーク パケットの処理に関連する一般的な安定性のリスクを軽減するために内にあることを強くお勧めします。

<a href="" id="fibre-channel-over-ethernet--fcoe--initiator"></a>Fibre Channel over Ethernet (FCoE) イニシエーター  
Windows オペレーティング システムは、FCoE をネイティブ サポートしていません。 FCoE をサポートするために、ベンダーは、リモートの記憶域デバイスへの接続に使用される FCoE イニシエーター スタックを提供する必要があります。

<a href="" id="dcb-capable-miniport-driver-and-network-adapter"></a>DCB 対応のミニポート ドライバーとネットワーク アダプター  
DCB の NDIS QoS をサポートするために、ミニポート ドライバーとネットワーク アダプターする必要がありますサポートで説明する要件[データ センター ブリッジングの NDIS QoS の要件](ndis-qos-requirements-for-data-center-bridging.md)します。

 

 





