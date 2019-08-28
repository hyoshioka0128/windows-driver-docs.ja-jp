---
title: ネットワーク ドライバー設計ガイドのナビゲーション
description: ネットワーク ドライバー設計ガイドのナビゲーション
ms.assetid: 8d9cbf3c-5eec-4409-ab4c-595bb921832d
keywords:
- ネットワークドライバー WDK、ドキュメント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4832be8f00942e6d0682de8febaf6368fc963d2c
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063875"
---
# <a name="navigating-the-network-driver-design-guide"></a>ネットワーク ドライバー設計ガイドのナビゲーション





Microsoft Windows ベースのオペレーティングシステムでは、さまざまな種類のカーネルモードネットワークドライバーがサポートしています。 Windows Driver Kit (WDK) のドキュメントの「ネットワーク」セクションでは、これらのネットワークドライバーを記述する方法について説明します。 このトピックでは、サポートされるネットワークドライバーの種類と、各種類のネットワークドライバーを記述する前に読み取る必要があるネットワークセクションのセクションについて簡単に説明します。

このネットワークドライバー設計ガイドでは、次の Network Driver Interface Specification (NDIS) インターフェイスについて説明します。

-   NDIS 6.40。 Windows 8.1、Windows Server 2012 R2、およびそれ以降のバージョンの Windows でサポートされています。 NDIS 6.30 では、ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI) 1.12 がサポートされています。

    NDIS 6.30 の詳細については、「 [ndis 6.40 の概要](introduction-to-ndis-6-40.md)」を参照してください。

-   NDIS 6.30 は、windows 8、Windows Server 2012、およびそれ以降のバージョンの Windows でサポートされています。 NDIS 6.30 では、単一のルート/i/o 仮想化 (SR-IOV)、Hyper-v 拡張可能スイッチ、ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI) 1.1、およびその他のサービスがサポートされています。

    NDIS 6.30 の詳細については、「 [ndis 6.30 の概要](introduction-to-ndis-6-30.md)」を参照してください。

-   NDIS 6.20。 windows 7、Windows Server 2008 R2、およびそれ以降のバージョンの Windows でサポートされています。 NDIS 6.20 には、仮想マシンキュー (VMQ)、receive side スロットル、およびその他のサービスのサポートが含まれています。

    NDIS 6.20 の詳細については、「 [ndis 6.20 の概要](introduction-to-ndis-6-20.md)」を参照してください。

-   NDIS 6.1 は、Windows Vista Service Pack 1 (SP1)、Windows Server 2008、およびそれ以降のバージョンの Windows でサポートされています。 NDIS 6.1 には、ヘッダーデータの分割、直接 OID 要求、およびその他のサービスのサポートが含まれています。

    NDIS 6.1 の詳細については、「 [ndis 6.1 の概要](introduction-to-ndis-6-1.md)」を参照してください。

-   NDIS 6.0。 Windows Vista 以降のバージョンの Windows でサポートされています。 NDIS 6.0 では、以前のバージョンの NDIS では提供されていなかったフィルタードライバーと多くの追加サービスがサポートされています。 NDIS 6.0 には、ドライバーの初期化とネットワークデータ管理の主要な更新プログラムが含まれています。これには、実行時にドライバーを再構成する必要があることや、ネットワークパケットデータを処理するための[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)アーキテクチャなどがあります ランタイムの再構成のサポートの詳細については、「[ドライバースタックの管理](driver-stack-management.md)」を参照してください。 NDIS 6.0 でネットワークパケットデータを処理する方法の詳細については、「 [\_NET BUFFER Architecture](net-buffer-architecture.md)」を参照してください。

    NDIS 6.0 の詳細については、「 [ndis 6.0 の概要](introduction-to-ndis-6-0.md)」を参照してください。

Windows Vista 以降のバージョンのオペレーティングシステムでは、次の種類のカーネルモードの NDIS ベースのネットワークドライバーがサポートされています。

<a href="" id="miniport-drivers"></a>[ミニポートドライバー](learning-about-miniport-drivers.md)  
ミニポート*ドライバー*は、ミニポートアダプターを管理し、上位レベルのドライバー用のアダプターへのインターフェイスを提供します。 *ミニポートアダプター*は、物理デバイスまたは仮想デバイスを表すことができる概念エンティティです。 たとえば、ミニポートアダプターは、ネットワークインターフェイスカード (NIC) または中間ドライバーに関連付けられている仮想デバイスを表すことができます。

*接続指向ミニポート呼び出しマネージャー (MCM)、* *Windows Driver Model (WDM) ミニポートドライバー、* 中間ドライバーの上端など、多くの種類のミニポートドライバーがあります。

<a href="" id="protocol-drivers"></a>[プロトコルドライバー](learning-about-protocol-drivers.md)  
*プロトコルドライバー*は、ドライバースタックに高レベルのサービスを提供します。 プロトコルドライバーは、基になるミニポートアダプターにバインドされます。 *上位レベルのプロトコルドライバー*は、インターフェイス (場合によってはアプリケーション固有のインターフェイス) を上端に実装して、ネットワークのユーザーにサービスを提供します。 下端では、プロトコルドライバーは、ネットワークデータを受信し、次の下位のドライバーから受信データを受信するためのプロトコルインターフェイスを提供します。

プロトコルドライバーにはさまざまな種類があります。たとえば、*接続指向のコールマネージャー (MCM)、接続指向クライアント、* 中間ドライバーの下端などです。

<a href="" id="filter-drivers"></a>[ドライバーのフィルター](learning-about-filter-drivers.md)  
*フィルタードライバー*は、プロトコルドライバーとミニポートドライバーの間のインターフェイスに関する情報をフィルター処理します。 *フィルターモジュール*は、プロトコルドライバーとミニポートアダプター間のバインドでアタッチされ、通常は他のドライバーに対して透過的です。 フィルタードライバーは *、変更または監視フィルター*を実装できます。 たとえば、フィルタードライバーは、基になるミニポートアダプターによって提供されるサービスを拡張したり、単に統計を収集したりすることができます。

<a href="" id="intermediate-drivers"></a>[中間ドライバー](learning-about-intermediate-drivers.md)  
上位レベルのプロトコルドライバーとミニポートドライバーの間の*中間ドライバー*インターフェイス。 中間ドライバーは、上位のプロトコルドライバーにバインドするためのミニポートドライバーインターフェイスを上端に用意しています。 中間ドライバーは、基になるミニポートアダプターにバインドするプロトコルドライバーインターフェイスを下部に用意しています。 中間ドライバーは、通常、 *n*から*m*マルチプレクサーまでのサービスを実装するために使用されます。 たとえば、中間ドライバーは負荷分散とフェールオーバーソリューションを実装できます。

中間ドライバーは、*ミニポート中間ドライバー*として構成されている場合にも、ハードウェアを管理できます。

Windows ネットワークアーキテクチャとプログラミングに関する考慮事項の詳細については、「[カーネルモードドライバーのネットワークアーキテクチャ](network-architecture-for-kernel-mode-drivers.md)」および「[ネットワークドライバーのプログラミングに関する考慮事項](network-driver-programming-considerations.md)」を参照してください。

ネットワークコンポーネントのインストールに使用されるネットワーク INF ファイルの詳細については、「[ネットワークコンポーネントのインストール](installing-network-components.md)」を参照してください。 ネットワークドライバーが通知オブジェクトを必要とする場合 (バインドを制御する場合など) は、「[ネットワークコンポーネントのオブジェクトへの通知](notify-objects-for-network-components.md)」も参照してください。

次の追加ドライバーモデルを使用して、特定のハードウェアテクノロジとアーキテクチャを使用することができます。

<table>  
<colgroup> <col width="50%" /> <col width="50%" /> </colgroup>  
<thead>  
<tr class="header">  
<th align="left">テクノロジ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/" data-raw-source="[Scalable Networking](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)">スケーラブル ネットワーク</a></p></td>
<td align="left"><p>ネットワークアダプターに対するタスクのオフロードをサポートするネットワークテクノロジ。次に例を示します。</p>
<ul>
<li><p><a href="header-data-split.md" data-raw-source="[Header-Data Split](header-data-split.md)">ヘッダー-データを分割</a>します。これは、受信したイーサネットフレームのヘッダーとデータを別々のバッファーに分割するサービスです。</p></li>
<li><p><a href="ndis-receive-side-scaling2.md" data-raw-source="[Receive Side Scaling](ndis-receive-side-scaling2.md)">受信側のスケーリング</a>は、マルチプロセッサシステムのネットワークパフォーマンスを向上させるネットワークドライバーテクノロジです。</p></li>
<li><p><a href="ndis-tcp-chimney-offload.md" data-raw-source="[TCP Chimney Offload](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-tcp-chimney-offload)">Tcp Chimney オフロード</a>。 tcp プロトコル処理のデータ転送部分が、適切な機能を備えたネットワークアダプターにオフロードされます。</p></li>
<li><p><a href="tcp-ip-offload.md" data-raw-source="[TCP/IP Offload](tcp-ip-offload.md)">Tcp/ip オフロード</a>とは、タスクのオフロード、または適切な機能を備えたネットワークアダプターへの接続のことです。</p></li>
<li><p><a href="overview-of-network-direct-kernel-provider-interface--ndkpi-.md" data-raw-source="[Network Direct Kernel Provider Interface (NDKPI)](overview-of-network-direct-kernel-provider-interface--ndkpi-.md)">ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI)</a>。これにより、SMB サーバーやクライアントなどのカーネルモードの Windows コンポーネントは、独立系ハードウェアベンダー (ihv) によって提供されるリモートダイレクトメモリアクセス (RDMA) 機能を使用できるようになります。</p></li>
<li><p><a href="network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md" data-raw-source="[Network Virtualization using Generic Routing Encapsulation (NVGRE) Task Offload](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)">汎用ルーティングカプセル化 (NVGRE) タスクオフロードを使用したネットワーク仮想化</a>。これにより、汎用ルーティングカプセル化 (GRE) でカプセル化されたパケットを使用できるようになります。</p>
<ul>
<li>Large Send Offload (LSO)</li>
<li>仮想マシン キュー (VMQ)</li>
<li>送信 (Tx) チェックサムオフロード</li>
<li>受信 (Rx) チェックサムオフロード</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="virtualized-networking.md" data-raw-source="[Virtualized Networking](virtualized-networking.md)">仮想化ネットワーク</a></p></td>
<td align="left"><p>次のような、Hyper-v 仮想化環境をサポートするネットワークテクノロジ。</p>
<ul>
<li><p><a href="single-root-i-o-virtualization--sr-iov-.md" data-raw-source="[Single Root I/O Virtualization (SR-IOV)](single-root-i-o-virtualization--sr-iov-.md)">シングルルート i/o 仮想化 (SR-IOV)</a></p></li>
<li><p><a href="virtual-machine-queue--vmq--in-ndis-6-20.md" data-raw-source="[Virtual Machine Queue (VMQ)](virtual-machine-queue--vmq--in-ndis-6-20.md)">仮想マシンキュー (VMQ)</a></p></li>
<li><p><a href="hyper-v-extensible-switch.md" data-raw-source="[Hyper-V Extensible Switch](hyper-v-extensible-switch.md)">Hyper-v 拡張可能スイッチ</a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/" data-raw-source="[Wireless Networking](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)">ワイヤレス ネットワーキング</a></p></td>
<td align="left"><p>ネイティブ802.11 ワイヤレス LAN を含むネットワーク機能。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/" data-raw-source="[Network Module Registrar](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)">ネットワーク モジュール レジストラー</a></p></td>
<td align="left"><p>ドライバーがネットワークモジュールを相互に接続できるようにするシステム機能。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/" data-raw-source="[Winsock Kernel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)">Winsock カーネル</a></p></td>
<td align="left"><p>カーネルモードのネットワークプログラミングインターフェイス (NPI)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ip-helper.md" data-raw-source="[IP Helper](ip-helper.md)">IP ヘルパー</a></p></td>
<td align="left"><p>ドライバーがローカルコンピューターのネットワーク構成に関する情報を取得および変更できるようにする一連のユーティリティ関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="windows-filtering-platform-callout-drivers2.md" data-raw-source="[Windows Filtering Platform Callout Drivers](windows-filtering-platform-callout-drivers2.md)">Windows フィルタリング プラットフォーム コールアウト ドライバー</a></p></td>
<td align="left"><p>ネットワークデータの詳細な検査、パケットの変更、ストリームの変更、およびログ記録を可能にするカーネルモードインターフェイス。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="system-area-networks.md" data-raw-source="[System Area Networks](system-area-networks.md)">システム エリア ネットワーク</a></p></td>
<td align="left"><p>高パフォーマンスの接続指向ネットワークをサポートするために Windows ソケットダイレクトを使用するネットワーク接続の一種。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff570659(v=vs.85)" data-raw-source="[Remote NDIS (RNDIS)](https://docs.microsoft.com/previous-versions/ff570659(v=vs.85))">リモート NDIS (RNDIS)</a></p></td>
<td align="left"><p>システム指定のバスに依存しない、USB バス上のメッセージセットを定義するクラス仕様。</p></td>
</tr>
</tbody>
</table>

 

 

 





