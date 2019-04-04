---
title: RAS アーキテクチャの概要
description: RAS アーキテクチャの概要
ms.assetid: 1ff285d7-2aed-46e1-979e-3b77614dcbf5
keywords:
- リモート アクセス サービスの WDK ネットワーク
- ネットワーク RAS WDK
- アーキテクチャの WDK WAN RAS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9901d484f64a3a1eb56dff45c2758f3b49500400
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537919"
---
# <a name="ras-architecture-overview"></a>RAS アーキテクチャの概要





リモート アクセス サービス (RAS) は、リモートのワークステーションの場合、リモートのワークステーションが、LAN 上同じように、LAN 上の LAN とアクセスのリソースへのダイヤルアップ接続を確立するために使用できます。 WAN ミニポート ドライバーでは、RAS および ISDN、X.25、および交換 56 アダプターなどのワイド エリア ネットワーク (WAN) カードの間のインターフェイスを提供します。

RAS アーキテクチャの主要システム提供のコンポーネントを以下に示します。

-   [NDISWAN](#ddk-ndiswan-ng)

-   [TAPI サービス](#ddk-tapi-service-ng)

-   [NDPROXY](#ddk-ndproxy-ng)

-   [NDISTAPI](#ddk-ndistapi-ng)

開発者提供 TAPI 対応アプリケーションと WAN ミニポート ドライバー。 いる CoNDIS WAN の開発者は、WAN クライアント プロトコルのドライバー、ミニポート コール マネージャー (MCM)、または別のコール マネージャーも提供できます。

次の図は、RAS アーキテクチャを示します。

![ras アーキテクチャを示す図](images/condsras.png)

次のセクションには、RAS アーキテクチャのコンポーネントについて簡単に説明します。

### <a name="ras-and-tapi-components"></a>RAS and TAPI コンポーネント

前述の右側にあるコンポーネントは、TAPI に関連する呼び出しの実装を設定して、呼び出しと接続の破棄など、管理操作を図します。 これらの操作の詳細については、WAN のモデル (NDIS WAN またはいる CoNDIS WAN) によって異なります。

### <a href="" id="ddk-ras-functions-ng"></a>RAS 関数

ユーザー モード アプリケーションでは、リモート コンピューターと RAS 接続するために RAS 関数を呼び出します。 RAS 接続が確立されると、このようなアプリケーションは、Microsoft Windows Sockets、NetBIOS、名前付きパイプ、RPC などの標準のネットワーク インターフェイスを使用してネットワーク サービスに接続できます。

### <a href="" id="ddk-tapi-aware-applications-ng"></a>TAPI 対応アプリケーション

テレフォニーの通信が可能には、TAPI 対応のアプリケーションは、アプリケーションとサービスのプロセスの両方で実行します。 サービス プロバイダーは、特定のデバイスと通信します。 TAPI 対応のアプリケーションは、そのサービス プロバイダーと TAPI インターフェイス (Tapi32.dll) を介して通信します。 これらのサービス プロバイダーで実行、 [TAPI サービス](#ddk-tapi-service-ng)プロセス。

### <a href="" id="ddk-tapi-service-ng"></a>TAPI サービス

TAPI サービス (Tapisrv.exe) のプロセスはテレフォニー サービス プロバイダー インターフェイス (TSPI) をサービス プロバイダーの[TAPI 対応アプリケーション](#ddk-tapi-aware-applications-ng)します。 これらのサービス プロバイダーは、TAPI サービス プロセスのコンテキストで実行される Dll です。

オペレーティング システムでは、NDIS WAN またはいる CoNDIS WAN ミニポート ドライバーがユーザー モード アプリケーションとの通信に使用するサービス プロバイダーが用意されています。 NDIS WAN ミニポート ドライバーのサービス プロバイダーが[KMDDSP](#ddk-kmddsp-ng)します。 いる CoNDIS WAN ミニポート ドライバー (および MCMs) サービス プロバイダーが[NDPTSP](#ddk-ndptsp-ng)します。

### <a href="" id="ddk-kmddsp-ng"></a>KMDDSP

KMDDSP (Kmddsp.tsp) は、サービス プロバイダー、TAPI サービス プロセスのコンテキストで実行されている DLL です。 KMDDSP TAPI サービスに提示する TSPI インターフェイスを提供する[TAPI 対応アプリケーション](#ddk-tapi-aware-applications-ng)ように[NDISTAPI](#ddk-ndistapi-ng)ユーザー モード アプリケーションと通信できます。

ユーザー モードの要求を対応する TAPI Oid に変換する NDISTAPI 連携 KMDDSP (OID\_TAPI\_*Xxx*)。 TAPI Oid の詳細については、[TAPI オブジェクト](https://msdn.microsoft.com/library/windows/hardware/ff564235)を参照してください。

### <a href="" id="ddk-ndptsp-ng"></a>NDPTSP

NDPTSP (Ndptsp.tsp) は、サービス プロバイダー、TAPI サービス プロセスのコンテキストで実行されている DLL です。 NDPTSP TAPI サービスは、TAPI 対応のアプリケーションに提示する TSPI インターフェイスを提供するように[NDPROXY](#ddk-ndproxy-ng)ユーザー モード アプリケーションと通信できます。

TAPI 接続指向の Oid をユーザー モードの要求を変換する NDPROXY 連携 NDPTSP (OID\_CO\_TAPI\_*Xxx*)。 TAPI の詳細については、Oid を接続指向に、参照してください[Connection-Oriented NDIS の TAPI 拡張](https://msdn.microsoft.com/library/windows/hardware/ff570924)します。

### <a href="" id="ddk-ndistapi-ng"></a>NDISTAPI

NDISTAPI (Ndistapi.sys) から発行される TAPI 要求を受信する[KMDDSP](#ddk-kmddsp-ng)号餧ェヒェマル[ **NdisOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563710) NDIS WAN ミニポート ドライバーに対応する TAPI Oid をルーティングします。 NDISTAPI の詳細については、[NDISTAPI 概要](ndistapi-overview.md)を参照してください。

### <a href="" id="ddk-ndproxy-ng"></a>NDPROXY

NDPROXY (Ndproxy.sys) と通信、TSPI を通じて TAPI インターフェイス[NDPTSP](#ddk-ndptsp-ng)を提供します。 NDPROXY は、NDIS を通じて NDISWAN いる CoNDIS WAN ミニポート ドライバー、MCMs、コール マネージャーと通信します。

NDPROXY の詳細については、[NDPROXY 概要](ndproxy-overview.md)を参照してください。

### <a name="driver-stack"></a>ドライバー スタック

### <a href="" id="ddk-wan-transports-ng"></a>WAN のトランスポート

RAS システム コンポーネントは、PPP 認証 (PAP、CHAP)、およびネットワークなどのトランスポート構成プロトコル ドライバー (IPCP、IPXCP、NBFCP、LCP、およびなど) を提供します。 WAN ミニポート ドライバー (または MCM) は、PPP メディア固有のフレームのみを実装します。

### <a href="" id="ddk-ndiswan-ng"></a>NDISWAN

NDISWAN (Ndiswan.sys) は、NDIS intermediate ドライバーです。 上端で NDIS プロトコル ドライバーにバインドする NDISWAN と[WAN ミニポート ドライバー](wan-miniport-drivers.md)下端にあります。

NDISWAN は、PPP フレームのプロトコル/リンク、圧縮/圧縮解除、および暗号化/暗号化解除を提供します。 NDISWAN は、NDIS WAN といる CoNDIS WAN ミニポート ドライバーと連動します。

NDISWAN の詳細については、[NDISWAN 概要](ndiswan-overview.md)を参照してください。

### <a href="" id="ddk-serial-driver-ng"></a>シリアル ドライバー

シリアル ドライバー コンポーネントは、内部のシリアル ポートまたはマルチポート シリアル カード用の標準的なデバイス ドライバーです。 Microsoft Windows 2000 以降に含まれる非同期の WAN ミニポート ドライバーでは、モデム間の通信の内部シリアル ドライバーを使用します。 シリアル ドライバーとして同じ関数をエクスポートするすべてのドライバーは、組み込みの非同期 WAN ミニポート ドライバーと対話できます。

**注**  X.25 ベンダーは、X.25 インターフェイス カードのシリアル ドライバーのエミュレーターを実装できます。 この場合、X.25 カードの各仮想回線は、シリアル ポート、X.25 パケット アセンブラー/逆アセンブラー (パッド) に接続されているとして表示されます。 接続インターフェイスは、シリアル信号 DTR、DCD、CTS、RTS、DSR などをエミュレート正しくする必要があります。
X.25 カードのシリアル ドライバーのエミュレーターを実装する X.25 ベンダーでは、そのパッド Pad.inf ファイル内のエントリを加える必要があります。 このファイルには、X.25 パッド経由の接続に必要なコマンド/応答スクリプトが含まれています。 Pad.inf ファイルに関する詳細については、Microsoft Windows SDK のドキュメントを参照してください。

 

### <a name="wan-miniport-driver"></a>WAN ミニポート ドライバー

WAN ミニポート ドライバーの間のインターフェイスを提供する[NDISWAN](#ddk-ndiswan-ng)と WAN Nic です。

WAN ミニポート ドライバーは、NDIS WAN ミニポート ドライバーまたはいる CoNDIS WAN ミニポート ドライバーとして実装できます。 詳細については、アプリケーションに最も適したミニポート ドライバー モデルの選択は、[WAN ドライバー モデルを選択する](choosing-a-wan-driver-model.md)を参照してください。

 

 





