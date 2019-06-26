---
title: NVGRE タスク オフロード
description: このセクションでは、Network Virtualization using Generic Routing Encapsulation (NVGRE) タスク オフロードをについて説明します
ms.assetid: D1BE5659-4491-411B-9D32-9CB7A141A240
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d0fb599d7766d119fa8ba2c998f0eb8645f8817
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371219"
---
# <a name="network-virtualization-using-generic-routing-encapsulation-nvgre-task-offload"></a>汎用ルーティング カプセル化 (NVGRE) タスク オフロードを使用したネットワークの仮想化

HYPER-V ネットワーク仮想化では、Generic Routing Encapsulation (NVGRE) を IP アドレスを仮想化メカニズムとして使用するネットワーク仮想化をサポートします。 Nvgre で仮想マシンのパケットに別のパケット カプセル化します。 この新しい、NVGRE でフォーマットされたパケットのヘッダーは、適切なソースと変換先プロバイダーの領域 (PA) の IP アドレスを持ちます。 さらに、24 ビット仮想サブネット ID (VSID)、新しいパケットの GRE ヘッダーに格納されているがあります。

次の図は、GRE カプセル化パケットを示します。 は、NVGRE カプセル化パケットは外部の IP ヘッダーのペイロード (イーサネット ヘッダーを含む)、GRE カプセル化された IP パケットがある点が、IP over Ethernet のパケットのようになります。

![元のパケットと gre カプセル化パケットを比較します。 mac を含む (gre を含む内部 mac)、ip ヘッダー (gre を含む内部の ip ヘッダー)、tcp ヘッダー、および tcp ユーザー データ。 さらに、gre のカプセル化パケットには、外部の mac、外部の ip ヘッダー、および gre が含まれています。](images/nvgre.png)

NDIS 6.30 (Windows Server 2012 で使用可能な以降) では、NVGRE でフォーマットされたパケットを使用することができます NVGRE タスク オフロード、導入されています。

-   Large Send Offload (LSO)
-   仮想マシン キュー (VMQ)
-   送信 (テキサス州) チェックサム オフロード (IPv4、TCP、UDP)
-   受信 (Rx) チェックサム オフロード (IPv4、TCP、UDP)

**注**  内側と外側の IP ヘッダーのバージョンの異なるパケットをつまり、オフロード「混合モード」パケットのプロトコル ドライバー可能性があります。 たとえば、パケットは、外部の IP ヘッダーと IPv6 と IPv4 の内部 IP ヘッダー可能性があります。

 

**注**  がプロトコル ドライバー内部の TCP または UDP ヘッダーを持たない NVGRE 形式のパケットをオフロードすることもできます。 たとえば、IP パケットには、インターネット制御メッセージ プロトコル (ICMP) パケットである内部のペイロード可能性があります。

 

NVGRE の詳細については、次のインターネット ドラフトを参照してください。

-   [NVGRE:Generic Routing Encapsulation によるネットワーク仮想化](http://ietfreport.isoc.org/idref/draft-sridharan-virtualization-nvgre/)

NVGRE は、Generic Routing Encapsulation (GRE) に基づいています。 GRE の詳細については、次のリソースを参照してください。

-   [RFC 2784:汎用ルーティング カプセル化 (GRE)](https://tools.ietf.org/html/rfc2784)
-   [RFC 2890:GRE をキーとシーケンス番号の拡張機能](https://tools.ietf.org/html/rfc2890)

このセクションの内容:

-   [Generic Routing Encapsulation (NVGRE) タスク オフロードを使用してネットワーク仮想化の概要](overview-of-network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)
-   [大量送信オフロード (LSO) で NVGRE をサポートしています。](supporting-nvgre-in-large-send-offload--lso-.md)
-   [チェックサム オフロードで NVGRE をサポートしています。](supporting-nvgre-in-checksum-offload.md)
-   [NVGRE サポートの RSS および VMQ 受信タスク オフロード](supporting-nvgre-in-rss-and-vmq-receive-task-offloads.md)
-   [内のパケットをカプセル化されたトランスポート ヘッダーを検索する、パスが表示されます。](locating-the-transport-header-for-encapsulaged-packets-in-the-receive-path.md)
-   [ネットワーク アダプターの NVGRE タスク オフロード機能を判断します。](determining-the-nvgre-task-offload-capabilities-of-a-network-adapter.md)
-   [クエリを実行して、NVGRE タスク オフロードの状態を変更します。](querying-and-changing-nvgre-task-offload-state.md)
-   [NVGRE タスク オフロード用の標準化された INF キーワード](standardized-inf-keywords-for-nvgre-task-offload.md)

## <a name="related-topics"></a>関連トピック


[チェックサム タスクをオフロードします。](offloading-checksum-tasks.md)

[大きな TCP パケットのセグメント化をオフロード](offloading-the-segmentation-of-large-tcp-packets.md)

[TCP/IP タスク オフロード](task-offload.md)

 

 






