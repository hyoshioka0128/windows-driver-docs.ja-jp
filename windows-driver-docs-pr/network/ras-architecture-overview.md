---
title: RAS アーキテクチャの概要
description: RAS アーキテクチャの概要
ms.assetid: 1ff285d7-2aed-46e1-979e-3b77614dcbf5
keywords:
- リモートアクセスサービスの WDK ネットワーク
- RAS WDK ネットワーク
- アーキテクチャ WDK WAN、RAS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81cf2de93954b2bdd7d730f2a80bb30d2cc45099
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843473"
---
# <a name="ras-architecture-overview"></a>RAS アーキテクチャの概要





リモートアクセスサービス (RAS) を使用すると、リモートワークステーションが lan へのダイヤルアップ接続を確立し、リモートワークステーションが LAN 上にあるかのように LAN 上のリソースにアクセスできます。 WAN ミニポートドライバーは、RAS とワイドエリアネットワーク (WAN) カード (ISDN、x.25、切り替え56アダプターなど) との間のインターフェイスを提供します。

システムで提供される主要なコンポーネントには、次のようなものがあります。

-   [NDISWAN](#ddk-ndiswan-ng)

-   [TAPI サービス](#ddk-tapi-service-ng)

-   [NDPROXY](#ddk-ndproxy-ng)

-   [NDISTAPI](#ddk-ndistapi-ng)

開発者は、TAPI 対応アプリケーションと WAN ミニポートドライバーを提供します。 Conmwan 開発者は、WAN クライアントプロトコルドライバー、ミニポートコールマネージャー (MCM)、または別の呼び出しマネージャーを提供することもできます。

次の図は、RAS アーキテクチャを示しています。

![ras アーキテクチャを示す図](images/condsras.png)

以下のセクションでは、RAS アーキテクチャのコンポーネントについて簡単に説明します。

### <a name="ras-and-tapi-components"></a>RAS および TAPI コンポーネント

前の図の右側にあるコンポーネントは、TAPI 関連の呼び出し管理操作を実装します。たとえば、呼び出しと接続の設定や解除などです。 これらの操作の詳細は、WAN モデル (NDIS WAN または CoNDIS WAN) によって異なります。

### <a href="" id="ddk-ras-functions-ng"></a>RAS 機能

ユーザーモードのアプリケーションは、RAS 機能を呼び出して、リモートコンピューターとの RAS 接続を確立します。 RAS 接続が確立されると、このようなアプリケーションは、Microsoft Windows Sockets、NetBIOS、名前付きパイプ、RPC などの標準的なネットワークインターフェイスを使用してネットワークサービスに接続できます。

### <a href="" id="ddk-tapi-aware-applications-ng"></a>TAPI 対応アプリケーション

テレフォニー通信に対応している TAPI 対応アプリケーションは、アプリケーションとサービスの両方のプロセスで実行されます。 サービスプロバイダーは、特定のデバイスと通信します。 TAPI 対応アプリケーションは、TAPI インターフェイス (Tapi32) を介してサービスプロバイダーと通信します。 これらのサービスプロバイダーは、 [TAPI サービス](#ddk-tapi-service-ng)プロセスで実行されます。

### <a href="" id="ddk-tapi-service-ng"></a>TAPI サービス

TAPI サービス (Tapisrv) プロセスでは、サービスプロバイダーのテレフォニーサービスプロバイダーインターフェイス (TSPI) が[tapi 対応アプリケーション](#ddk-tapi-aware-applications-ng)に提示されます。 これらのサービスプロバイダーは、TAPI サービスプロセスのコンテキストで実行される Dll です。

オペレーティングシステムは、ユーザーモードアプリケーションとの通信に NDIS WAN または CoNDIS WAN ミニポートドライバーが使用するサービスプロバイダーを提供します。 NDIS WAN ミニポートドライバー用のサービスプロバイダーは[Kmddsp](#ddk-kmddsp-ng)です。 CoNDIS WAN ミニポートドライバー (および MCMs) のサービスプロバイダーは、 [Ndptsp](#ddk-ndptsp-ng)です。

### <a href="" id="ddk-kmddsp-ng"></a>KMDDSP

KMDDSP (Kmddsp. tsp) は、TAPI サービスプロセスのコンテキストで実行されるサービスプロバイダーの DLL です。 KMDDSP は、tapi サービスが[tapi 対応アプリケーション](#ddk-tapi-aware-applications-ng)に提示する tspi インターフェイスを提供します。これにより、 [ndistapi](#ddk-ndistapi-ng)はユーザーモードアプリケーションと通信できるようになります。

KMDDSP は NDISTAPI と連携して、ユーザーモード要求を対応する TAPI Oid (OID\_TAPI\_*Xxx*) に変換します。 TAPI Oid の詳細については、「 [Tapi オブジェクト](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff564235(v=vs.85))」を参照してください。

### <a href="" id="ddk-ndptsp-ng"></a>NDPTSP

NDPTSP (Ndptsp. tsp) は、TAPI サービスプロセスのコンテキストで実行されるサービスプロバイダーの DLL です。 NDPTSP は、tapi サービスが TAPI 対応アプリケーションに提示する TSPI インターフェイスを提供します。これにより、 [Ndproxy](#ddk-ndproxy-ng)はユーザーモードアプリケーションと通信できるようになります。

NDPTSP は NDPROXY と連携して、ユーザーモード要求を TAPI 接続指向 Oid (OID\_CO\_TAPI\_*Xxx*) に変換します。 TAPI 接続指向の Oid の詳細については、「 [Tapi Extensions For Connection 志向 NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/tapi-extension-oids-for-connection-oriented-ndis)」を参照してください。

### <a href="" id="ddk-ndistapi-ng"></a>NDISTAPI

NDISTAPI (Ndistapi) は、 [Kmddsp](#ddk-kmddsp-ng)からの tapi 要求を受信し、 [**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)を呼び出して、対応する TAPI oid を NDIS WAN ミニポートドライバーにルーティングします。 NDISTAPI の詳細については、「 [Ndistapi の概要](ndistapi-overview.md)」を参照してください。

### <a href="" id="ddk-ndproxy-ng"></a>NDPROXY

NDPROXY (Ndproxy .sys) は、 [Ndptsp](#ddk-ndptsp-ng)が提供する tspi インターフェイスを介して TAPI と通信します。 NDPROXY は、NDIS と NDISWAN を介して通信し、WAN ミニポートドライバー、MCMs、および call manager を使用します。

NDPROXY の詳細については、「 [Ndproxy の概要](ndproxy-overview.md)」を参照してください。

### <a name="driver-stack"></a>ドライバースタック

### <a href="" id="ddk-wan-transports-ng"></a>WAN トランスポート

RAS システムコンポーネントは、PPP 認証 (PAP、CHAP) やネットワーク構成プロトコルドライバー (IPCP、IPXCP、NBFCP、LCP など) などのトランスポートを提供します。 WAN ミニポートドライバー (または MCM) は、PPP メディア固有のフレームのみを実装します。

### <a href="" id="ddk-ndiswan-ng"></a>NDISWAN

NDISWAN (Ndiswan) は、NDIS 中間ドライバーです。 NDISWAN は、上部のエッジにある NDIS プロトコルドライバーと、低速の[WAN ミニポートドライバー](wan-miniport-drivers.md)にバインドします。

NDISWAN は、PPP プロトコル/リンクフレーミング、圧縮/圧縮解除、暗号化/復号化を提供します。 NDISWAN インターフェイスは、NDIS WAN と CoNDIS WAN ミニポートドライバーの両方を備えています。

NDISWAN の詳細については、「 [NDISWAN の概要](ndiswan-overview.md)」を参照してください。

### <a href="" id="ddk-serial-driver-ng"></a>シリアルドライバー

Serial driver コンポーネントは、内部シリアルポートまたはマルチポートシリアルカード用の標準デバイスドライバーです。 Microsoft Windows 2000 以降に含まれる非同期 WAN ミニポートドライバーは、モデム通信用の内部シリアルドライバーを使用します。 シリアルドライバーと同じ機能をエクスポートするドライバーは、組み込みの非同期 WAN ミニポートドライバーとやり取りできます。

**注**x.25 ベンダー  、x.25 インターフェイスカード用のシリアルドライバーエミュレーターを実装できます。 この場合、x.25 カード上の各仮想回線は、x.25 パケットアセンブラ/逆アセンブラー (埋め込み) がアタッチされたシリアルポートとして表示されます。 接続インターフェイスは、DTR、DCD、CTS、RTS、DSR などのシリアル信号を正しくエミュレートする必要があります。
また、x.25 カード用のシリアルドライバーエミュレーターを実装する x.25 ベンダーは、Pad の .inf ファイルでパッドのエントリを作成する必要があります。 このファイルには、x.25 パッドを介して接続するために必要なコマンド/応答スクリプトが含まれています。 Pad の .inf ファイルの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

### <a name="wan-miniport-driver"></a>WAN ミニポートドライバー

WAN ミニポートドライバーは、 [NDISWAN](#ddk-ndiswan-ng)と wan nic 間のインターフェイスを提供します。

WAN ミニポートドライバーは、NDIS WAN ミニポートドライバーまたは CoNDIS WAN ミニポートドライバーとして実装できます。 アプリケーションに最も適したミニポートドライバーモデルを選択する方法の詳細については、「 [WAN ドライバーモデルの選択](choosing-a-wan-driver-model.md)」を参照してください。

 

 





