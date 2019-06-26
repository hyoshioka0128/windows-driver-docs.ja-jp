---
title: ネットワーク ドライバー設計ガイドの使用
description: ネットワーク ドライバー設計ガイドの使用
ms.assetid: 8d9cbf3c-5eec-4409-ab4c-595bb921832d
keywords:
- ネットワーク ドライバー WDK ドキュメント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0abdeee8ba22722f9eeb34c1a9558806adec16fe
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391407"
---
# <a name="using-the-network-driver-design-guide"></a>ネットワーク ドライバー設計ガイドの使用





Microsoft Windows ベースのオペレーティング システムでは、複数の種類のネットワークのカーネル モード ドライバーをサポートします。 Windows Driver Kit (WDK) ドキュメントのネットワーク セクションでは、これらのネットワーク ドライバーを記述する方法について説明します。 このトピックでは簡単なネットワーク ドライバーのサポートされている型について説明し、ネットワーク ドライバーの種類ごとに書き込む前に確認してください [ネットワーク] のセクションについて説明します。

このネットワーク ドライバー設計のガイドでは、次の Network Driver Interface Specification (NDIS) インターフェイスをドキュメントします。

-   NDIS 6.40: Windows 8.1、Windows Server 2012 R2、および以降のバージョンの Windows ではサポートされています。 NDIS 6.30 のネットワーク直接カーネル プロバイダー インターフェイス (NDKPI) 1.12 をサポートしています。

    NDIS 6.30 の詳細については、次を参照してください。 [NDIS 6.40 概要](introduction-to-ndis-6-40.md)します。

-   NDIS 6.30: Windows 8、Windows Server 2012、および以降のバージョンの Windows ではサポートされています。 NDIS 6.30 には、1 つのルート/入出力仮想化 (SR-IOV)、HYPER-V 拡張可能スイッチ、ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI) 1.1、およびその他のサービスのサポートが含まれています。

    NDIS 6.30 の詳細については、次を参照してください。 [NDIS 6.30 概要](introduction-to-ndis-6-30.md)します。

-   NDIS 6.20: Windows 7、Windows Server 2008 R2、および以降のバージョンの Windows ではサポートされています。 受信側のスロットル、およびその他のサービス、NDIS 6.20 が動作には仮想マシン キュー (VMQ) のサポートが含まれます。

    NDIS 6.20 が動作の詳細については、次を参照してください。 [NDIS 6.20 が動作の概要](introduction-to-ndis-6-20.md)します。

-   NDIS 6.1 には、Windows Vista Service Pack 1 (SP1)、Windows Server 2008、および以降のバージョンの Windows ではサポートされています。 NDIS 6.1 には、ヘッダー データの分割、直接 OID 要求、およびその他のサービスのサポートが含まれています。

    NDIS 6.1 の詳細については、次を参照してください。 [NDIS 6.1 概要](introduction-to-ndis-6-1.md)します。

-   NDIS 6.0 には、Windows Vista および Windows の以降のバージョンでサポートされます。 NDIS 6.0 には、フィルター ドライバーのサポートおよびが以前のバージョンの NDIS で指定されていない多くの追加サービスが含まれます。 NDIS 6.0 には、ドライバーの初期化とネットワーク データの管理に必要なドライバーの再構成時のサポートなどの主要な更新プログラムが含まれていますと[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)ネットワーク パケット データを処理するためのアーキテクチャです。 ランタイムの再構成のサポートに関する詳細については、次を参照してください。[ドライバー スタック管理](driver-stack-management.md)します。 NDIS 6.0 でのネットワーク パケット データを処理する方法の詳細を参照してください。 [NET\_バッファー アーキテクチャ](net-buffer-architecture.md)します。

    NDIS 6.0 の詳細については、次を参照してください。 [NDIS 6.0 の概要](introduction-to-ndis-6-0.md)します。

Windows Vista およびそれ以降のオペレーティング システム バージョンは、NDIS ベースのネットワークのカーネル モード ドライバーの次の種類をサポートします。

<a href="" id="miniport-drivers"></a>[ミニポート ドライバー](learning-about-miniport-drivers.md)  
A*ミニポート ドライバー*ミニポート アダプターを管理しより高度なドライバーのアダプターにインターフェイスを提供します。 A*ミニポート アダプター*は物理デバイスまたは仮想デバイスのいずれかを表す概念エンティティです。 たとえば、ミニポート アダプターでは、ネットワーク インターフェイス カード (NIC) または中間のドライバーに関連付けられている仮想デバイスを表すことができます。

ミニポート ドライバーでは、多くのバリエーションとして、*接続指向ミニポート コール マネージャー (MCM)* 、*ミニポート ドライバーを Windows Driver Model (WDM)、* と中間のドライバーの上端。

<a href="" id="protocol-drivers"></a>[プロトコル ドライバー](learning-about-protocol-drivers.md)  
A*プロトコル ドライバー*ドライバー スタックでの高度なサービスを提供します。 プロトコル ドライバーは、基になるミニポート アダプターにバインドします。 *上位レベルのプロトコル ドライバー*ネットワークのユーザーにサービスを提供する、上端にある、特定のアプリケーション インターフェイス可能性があるインターフェイスを実装します。 下の端には、プロトコル ドライバーは、ネットワーク データを渡すし、次の下位ドライバーからデータを受信するプロトコル インターフェイスを提供します。

などのプロトコル ドライバーでは、多くのバリエーションがある、*接続指向のコール マネージャー (MCM)、接続指向のクライアントでは、* と中間のドライバーの下端。

<a href="" id="filter-drivers"></a>[フィルター ドライバー](learning-about-filter-drivers.md)  
A*フィルター ドライバー*プロトコルおよびミニポートのドライバーの間のインターフェイスに関する情報をフィルター処理します。 *モジュールをフィルター処理*プロトコル ドライバーとミニポート アダプター間のバインドに関連付けられているし、は一般に、その他のドライバーに対して透過的です。 フィルター ドライバーを実装できます*フィルターの監視を変更または*します。 たとえば、フィルター ドライバーは、基になるミニポート アダプターを提供するサービスを強化または単に統計情報を収集できます。

<a href="" id="intermediate-drivers"></a>[中間ドライバー](learning-about-intermediate-drivers.md)  
*中間ドライバー*上位レベルのプロトコルおよびミニポートのドライバーの間のインターフェイス。 中間のドライバーでは、その上端関連プロトコル ドライバーにバインドするでミニポート ドライバー インターフェイスを提供します。 中間のドライバーでは、基になるミニポート アダプターにバインドする、下端にあるプロトコル ドライバー インターフェイスを提供します。 中間のドライバーが実装するために通常使用*n*に*m*マルチプレクサー サービス。 たとえば、中間のドライバーでは、負荷分散とフェールオーバー ソリューションを実装できます。

として構成されている場合に、中間ドライバーはハードウェアを管理もできる、*ミニポート中間ドライバー*します。

詳細については、Windows ネットワーク アーキテクチャおよびプログラミングの考慮事項を参照してください[カーネル モード ドライバー用のネットワーク アーキテクチャ](network-architecture-for-kernel-mode-drivers.md)と[ネットワーク ドライバーのプログラミングに関する考慮事項](network-driver-programming-considerations.md)します。

使用して、ネットワーク コンポーネントをインストール、ネットワーク INF ファイルの詳細については、次を参照してください。[ネットワーク コンポーネントをインストール](installing-network-components.md)します。 ネットワーク ドライバーには、通知オブジェクト - が必要な場合などのバインディング - を制御するもを参照してください[ネットワーク コンポーネントの通知オブジェクト](notify-objects-for-network-components.md)します。

次の追加のドライバー モデルは、特定のハードウェア テクノロジとアーキテクチャを使用して利用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">テクノロジ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/" data-raw-source="[Scalable Networking](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)">スケーラブル ネットワーク</a></p></td>
<td align="left"><p>ネットワーク アダプターを次のようにタスクのオフロードをサポートするネットワーク テクノロジ:</p>
<ul>
<li><p><a href="header-data-split.md" data-raw-source="[Header-Data Split](header-data-split.md)">ヘッダー データの分割</a>ヘッダーとのデータを分割するサービスを別のバッファーにイーサネット フレームを受信します。</p></li>
<li><p><a href="ndis-receive-side-scaling2.md" data-raw-source="[Receive Side Scaling](ndis-receive-side-scaling2.md)">Receive Side Scaling</a>、マルチプロセッサ システムでのネットワーク パフォーマンスを向上させるネットワーク ドライバー テクノロジです。</p></li>
<li><p><a href="ndis-tcp-chimney-offload.md" data-raw-source="[TCP Chimney Offload](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-tcp-chimney-offload)">TCP Chimney オフロード</a>の処理を適切な機能を備えたネットワーク アダプターを TCP プロトコルのデータ転送の一部をオフロードします。</p></li>
<li><p><a href="tcp-ip-offload.md" data-raw-source="[TCP/IP Offload](tcp-ip-offload.md)">TCP/IP Offload</a>タスクの適切な機能を備えたネットワーク アダプターへの接続をオフロードします。</p></li>
<li><p><a href="overview-of-network-direct-kernel-provider-interface--ndkpi-.md" data-raw-source="[Network Direct Kernel Provider Interface (NDKPI)](overview-of-network-direct-kernel-provider-interface--ndkpi-.md)">ネットワークのダイレクト カーネル プロバイダー インターフェイス (NDKPI)</a>、SMB サーバーとクライアント、独立系ハードウェア ベンダー (Ihv) によって提供されるリモート ダイレクト メモリ アクセス (RDMA) 機能を使用するなどのカーネル モードの Windows コンポーネントを有効にします。</p></li>
<li><p><a href="network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md" data-raw-source="[Network Virtualization using Generic Routing Encapsulation (NVGRE) Task Offload](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)">ネットワーク仮想化の Generic Routing Encapsulation (NVGRE) タスク オフロードを使用して</a>、Generic Routing Encapsulation GRE カプセル化パケットを使用できるようにします。</p>
<ul>
<li>Large Send Offload (LSO)</li>
<li>仮想マシン キュー (VMQ)</li>
<li>送信 (テキサス州) チェックサム オフロード</li>
<li>受信 (Rx) チェックサム オフロード</li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="virtualized-networking.md" data-raw-source="[Virtualized Networking](virtualized-networking.md)">仮想化ネットワーク</a></p></td>
<td align="left"><p>ネットワーク接続など、次の HYPER-V 仮想化環境をサポートするテクノロジ。</p>
<ul>
<li><p><a href="single-root-i-o-virtualization--sr-iov-.md" data-raw-source="[Single Root I/O Virtualization (SR-IOV)](single-root-i-o-virtualization--sr-iov-.md)">シングル ルート I/O 仮想化 (SR-IOV)</a></p></li>
<li><p><a href="virtual-machine-queue--vmq--in-ndis-6-20.md" data-raw-source="[Virtual Machine Queue (VMQ)](virtual-machine-queue--vmq--in-ndis-6-20.md)">仮想マシン キュー (VMQ)</a></p></li>
<li><p><a href="hyper-v-extensible-switch.md" data-raw-source="[Hyper-V Extensible Switch](hyper-v-extensible-switch.md)">HYPER-V 拡張可能スイッチ</a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/" data-raw-source="[Wireless Networking](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)">ワイヤレス ネットワーキング</a></p></td>
<td align="left"><p>ネットワークを含むネイティブ 802.11 ワイヤレス LAN 機能。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/" data-raw-source="[Network Module Registrar](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)">ネットワーク モジュール レジストラー</a></p></td>
<td align="left"><p>ネットワーク モジュールを相互に接続するためのドライバーを許可するシステム機能。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/" data-raw-source="[Winsock Kernel](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)">Winsock カーネル</a></p></td>
<td align="left"><p>カーネル モード ネットワーク プログラミング インターフェイス (NPI)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ip-helper.md" data-raw-source="[IP Helper](ip-helper.md)">IP ヘルパー</a></p></td>
<td align="left"><p>ドライバーを取得し、ローカル コンピューターのネットワーク構成に関する情報を変更できるようにするユーティリティ関数のセット。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="windows-filtering-platform-callout-drivers2.md" data-raw-source="[Windows Filtering Platform Callout Drivers](windows-filtering-platform-callout-drivers2.md)">Windows フィルタリング プラットフォーム コールアウト ドライバー</a></p></td>
<td align="left"><p>カーネル モード インターフェイスにより、詳細な検査、パケットの変更、ストリームの変更、およびネットワーク データのログ記録です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="system-area-networks.md" data-raw-source="[System Area Networks](system-area-networks.md)">システム エリア ネットワーク</a></p></td>
<td align="left"><p>高パフォーマンス、接続指向ネットワークをサポートする Windows Sockets ダイレクトを使用するネットワーク接続の種類。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff570659(v=vs.85)" data-raw-source="[Remote NDIS (RNDIS)](https://docs.microsoft.com/previous-versions/ff570659(v=vs.85))">リモート NDIS (RNDIS)</a></p></td>
<td align="left"><p>USB バス経由で設定するシステム提供、バスに依存しないメッセージを定義するクラスの指定。</p></td>
</tr>
</tbody>
</table>

 

 

 





