---
title: IPsec Offload Version 2 でのセキュリティ アソシエーションの管理
description: IPsec Offload Version 2 でのセキュリティ アソシエーションの管理
ms.assetid: aaa352c1-fb70-4c96-adda-9710347e2442
keywords:
- IPsecOV2 WDK TCP/IP トランスポート、セキュリティ アソシエーション
- セキュリティ アソシエーション WDK IPsec オフロードします。
- SAs の WDK IPsec オフロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: deecaf4b56ddcf841a0b38fed885a0504e2a9657
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572412"
---
# <a name="managing-security-associations-in-ipsec-offload-version-2"></a>IPsec Offload Version 2 でのセキュリティ アソシエーションの管理

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




トランスポートは、NIC が IPsec オフロード バージョン 2 (IPsecOV2) を実行できることを決定後、TCP/IP 操作 (を参照してください[レポート NIC の IPsec オフロード バージョン 2 機能](reporting-a-nic-s-ipsec-offload-version-2-capabilities.md))、トランスポート、要求、NIC のミニポート ドライバーを追加します。または、トランスポートは、NIC に IPsec タスク オフロードできます前に NIC に複数のセキュリティ アソシエーション (Sa) SAs を追加した後、TCP/IP トランスポートも削除または更新できます。 IPsecOV2 インターフェイスには、追加、削除、および更新プログラムの Oid の直接の OID の NDIS インターフェイスが必要です。

**注**  NDIS NDIS 6.1 と以降のドライバーの直接の OID 要求インターフェイスを提供します。 [OID の直接の要求パス](https://msdn.microsoft.com/library/windows/hardware/ff564736)クエリを実行したり、頻繁に設定されている OID 要求をサポートします。

 

ミニポート ドライバーが、TCP/IP をトランスポート設定の NIC に 1 つ以上の SAs を追加することを要求する、 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569812) OID。 ミニポート ドライバーが、受信、 [ **IPSEC\_オフロード\_V2\_追加\_SA** ](https://msdn.microsoft.com/library/windows/hardware/ff556977)構造体し、SA で処理を IPsecOV2 の NIC を構成します。 OID に正常に設定されている\_TCP\_タスク\_IPSEC\_オフロード\_V2\_追加\_SA、ミニポート ドライバーでオフロード SA を識別するハンドルを初期化します、IPSEC\_オフロード\_V2\_追加\_SA 構造体。 トランスポートは、ミニポート ドライバーに後続の要求でこのハンドルを使用して (つまり、または変更または削除、SA への呼び出しで、送信パス上)。 詳細については、送信パスで SA ハンドルを使用して、[IPsec オフロード バージョン 2 でのネットワーク データの送信](sending-network-data-with-ipsec-offload-version-2.md)を参照してください。

ミニポート ドライバーは、SAs でサポートできる NIC の数を報告、 **SaOffloadCapacity**のメンバー、 [ **NDIS\_IPSEC\_オフロード\_V2**](https://msdn.microsoft.com/library/windows/hardware/ff565808)構造体。

ミニポート ドライバーを設定できる、 **SaDeleteReq**フラグ、 [ **NDIS\_IPSEC\_オフロード\_V2\_NET\_バッファー\_一覧\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565818)受信パケットの構造体。 TCP/IP トランスポートは発行後[OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_削除\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569813)を削除する 1 つの時間、パケットの受信に使用された着信 SA と 1 回もう一度削除された着信 SA に対応する送信の SA を削除します。

TCP/IP トランスポート問題[OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_削除\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569813)する受信の SAs を削除する、パケットを受信し、削除された着信 Sa に対応する送信の SAs を削除します。 対応する OID を受信する前に NIC がこれらの SAs を削除する必要があります\_TCP\_タスク\_IPSEC\_オフロード\_V2\_削除\_SA 要求。

TCP/IP トランスポートの設定、 [OID\_TCP\_タスク\_IPSEC\_オフロード\_V2\_UPDATE\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569814)を要求する OID ミニポートドライバーは、sa 拡張シーケンス番号 (ESN) を持つより高い順位ビットで NIC を更新します。 ESN、サポートされる nic のドライバーがに従って NIC で指定された SA のシーケンス番号を更新する必要があります、ミニポート ドライバーはこの要求を受け取る、 [ **IPSEC\_オフロード\_V2\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff556984)列挙値で指定されている、**操作**のメンバー、 [ **IPSEC\_オフロード\_V2\_UPDATE\_SA** ](https://msdn.microsoft.com/library/windows/hardware/ff556990)構造体。

 

 





