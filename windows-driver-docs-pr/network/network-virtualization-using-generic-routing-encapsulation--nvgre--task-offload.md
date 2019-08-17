---
title: 汎用ルーティングカプセル化を使用したネットワーク仮想化について (NVGRE)
description: このセクションでは、汎用ルーティングカプセル化 (NVGRE) タスクオフロードを使用したネットワーク仮想化について説明します。
ms.assetid: D1BE5659-4491-411B-9D32-9CB7A141A240
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd96a293f7351d2139acb157b8360eaec1929fc6
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565134"
---
# <a name="about-network-virtualization-using-generic-routing-encapsulation-nvgre"></a>汎用ルーティングカプセル化を使用したネットワーク仮想化について (NVGRE)

Hyper-v ネットワーク仮想化では、IP アドレスを仮想化するメカニズムとして、汎用ルーティングカプセル化 (NVGRE) を使用したネットワーク仮想化がサポートされています。 NVGRE では、仮想マシンのパケットは別のパケット内にカプセル化されます。 この新しい NVGRE 形式のパケットのヘッダーには、適切な送信元と送信先のプロバイダー領域 (PA) IP アドレスが含まれています。 また、新しいパケットの GRE ヘッダーに格納されている、24ビットの仮想サブネット ID (VSID) を備えています。

次の図は、GRE でカプセル化されたパケットを示しています。 ネットワーク上では、NVGRE でカプセル化されたパケットは IP over Ethernet パケットのように見えますが、外側の IP ヘッダーのペイロードは、GRE でカプセル化された IP パケット (イーサネットヘッダーを含む) である点が異なります。

![元のパケットと gre カプセル化のパケットの比較。 両方に mac (gre が内部 mac を含む)、ip ヘッダー (gre が内部 ip ヘッダーを含む)、tcp ヘッダー、および tcp ユーザーデータが含まれています。 さらに、gre カプセル化のパケットには、外部 mac、外部 ip ヘッダー、および gre が含まれています。](images/nvgre.png)

NDIS 6.30 (Windows Server 2012 以降で使用可能) では、NVGRE タスクオフロードが導入されています。これにより、NVGRE 形式のパケットを以下で使用できるようになります。

-   Large Send Offload (LSO)
-   仮想マシン キュー (VMQ)
-   送信 (Tx) チェックサムオフロード (IPv4、TCP、UDP)
-   受信 (Rx) チェックサムオフロード (IPv4、TCP、UDP)

**注:**   プロトコルドライバーが "混合モード" パケットをオフロードする可能性があります。これは、内部および外部の IP ヘッダーバージョンが異なるパケットを意味します。 たとえば、パケットには、IPv6 としての外部 IP ヘッダーと、IPv4 としての内部 IP ヘッダーを含めることができます。

 

また、プロトコルドライバーは、内部 TCP ヘッダーまたは UDP ヘッダーのない nvgre 形式のパケットをオフロードすることもできます。   たとえば、IP パケットは、インターネット制御メッセージプロトコル (ICMP) パケットである内部ペイロードを持つことができます。

 

NVGRE の詳細については、次のインターネットドラフトを参照してください。

-   [NVGRE汎用ルーティングカプセル化を使用したネットワーク仮想化](http://ietfreport.isoc.org/idref/draft-sridharan-virtualization-nvgre/)

NVGRE は、汎用ルーティングカプセル化 (GRE) に基づいています。 GRE の詳細については、次のリソースを参照してください。

-   [RFC 2784:汎用ルーティングカプセル化 (GRE)](https://tools.ietf.org/html/rfc2784)
-   [RFC 2890:GRE のキーおよびシーケンス番号の拡張機能](https://tools.ietf.org/html/rfc2890)

このセクションの内容:

-   [汎用ルーティングカプセル化 (NVGRE) タスクオフロードを使用したネットワーク仮想化の概要](overview-of-network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)
-   [Large Send Offload (LSO) での NVGRE のサポート](supporting-nvgre-in-large-send-offload--lso-.md)
-   [チェックサムオフロードでの NVGRE のサポート](supporting-nvgre-in-checksum-offload.md)
-   [RSS および VMQ 受信タスクのオフロードでの NVGRE のサポート](supporting-nvgre-in-rss-and-vmq-receive-task-offloads.md)
-   [受信パスでカプセル化されたパケットのトランスポートヘッダーを検索する](locating-the-transport-header-for-encapsulaged-packets-in-the-receive-path.md)
-   [ネットワークアダプターの NVGRE タスクオフロード機能を確認する](determining-the-nvgre-task-offload-capabilities-of-a-network-adapter.md)
-   [NVGRE タスクオフロード状態のクエリと変更](querying-and-changing-nvgre-task-offload-state.md)
-   [NVGRE タスクオフロード用の標準化された INF キーワード](standardized-inf-keywords-for-nvgre-task-offload.md)

## <a name="related-topics"></a>関連トピック


[チェックサムタスクのオフロード](offloading-checksum-tasks.md)

[大きな TCP パケットのセグメント化のオフロード](offloading-the-segmentation-of-large-tcp-packets.md)

[TCP/IP タスクオフロード](task-offload.md)

 

 






