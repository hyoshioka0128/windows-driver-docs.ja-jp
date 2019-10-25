---
title: NDIS 6.40 の概要
description: このセクションでは、NDIS 6.40 について説明し、その主要な設計の追加について説明します。 NDIS 6.40 は Windows 8.1 および Windows Server 2012 R2 以降に含まれています。
ms.assetid: 46DB94AA-DBAD-49E0-A1F0-FEB095E26F2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 934417f92d978fe513a5298c6ec71c2a9b90a789
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844171"
---
# <a name="introduction-to-ndis-640"></a>NDIS 6.40 の概要


このセクションでは、Network Driver Interface Specification (NDIS) 6.40 を紹介し、主な設計の追加について説明します。 NDIS 6.40 は、Windows 8.1 および Windows Server 2012 R2 以降のオペレーティングシステムに含まれています。

## <a name="feature-updates"></a>機能更新プログラム


Windows 8.1 と Windows Server 2012 R2 では、次の機能に対するマイナーな更新が導入されています。

### <a name="ndkpi"></a>NDKPI

NDKPI 1.2 では、NDKPI DDI に次の新しい要素が追加されます。

- *Ndksendandinvalidate* ([*NDK\_FN\_SEND\_および\_無効化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send_and_invalidate)) 関数
- *NdkGetCqResultsEx* ([*NDK\_FN\_GET\_CQ\_RESULTS\_EX*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_get_cq_results_ex)) 関数
- [**NDK\_RESULT\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_result_ex)構造体
- 新しい要求のコールバック*フラグ*値: **NDK\_OP\_フラグ\_遅延**
- 新しい[**ndk\_アダプターの\_情報**](https://docs.microsoft.com/windows/desktop/api/ndkinfo/ns-ndkinfo-_ndk_adapter_info)**adapterflags**値: **NDK\_アダプター\_フラグ\_RDMA\_読み取り\_ローカル\_\_サポートされているを無効**にします

### <a name="native-80211-wireless-lan"></a>ネイティブ802.11 ワイヤレス LAN

IEEE 802.11 ac の非常に高いスループット (VHT) PHY がサポートされるようになりました。 次の DDI 要素が更新されました。

- [**DOT11\_PHY\_TYPE 列挙型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/windot11/ne-windot11-_dot11_phy_type)
- [OID\_DOT11\_現在の\_チャネル](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-current-channel)
- [OID\_DOT11\_サポート\_PHY\_型](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-supported-phy-types)
- [OID\_DOT11\_サポート\_OFDM\_FREQUENCY\_LIST](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-supported-ofdm-frequency-list)

## <a name="sample-and-documentation-updates"></a>サンプルとドキュメントの更新

[Hyper-v 拡張可能スイッチ転送拡張機能のサンプル](https://go.microsoft.com/fwlink/p/?LinkId=617913)が、ハイブリッド転送を実装するように更新されました。

次のドキュメントセクションが追加または大幅に拡張されています。

-   [Ndis 6. x ドライバーを NDIS 6.30 に移植する](porting-ndis-6-x-drivers-to-ndis-6-30.md)
-   [ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)設計ガイド
-   [汎用ルーティングカプセル化 (NVGRE) タスクオフロードを使用したネットワーク仮想化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)
-   [受信セグメント合体 (RSC)](receive-segment-coalescing--rsc-.md)設計ガイド
-   [Hyper-v 拡張可能スイッチ拡張機能の作成はじめに](getting-started-writing-a-hyper-v-extensible-switch-extension.md)
-   [NVGRE タスクオフロードのリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

NetDMA インターフェイスは、Windows 8 および Windows Server 2012 以降ではサポートされていません。 これが反映されるように、ドキュメントが更新されました。

ここでは、次のトピックについて説明します。

- [NDIS 6.40 ドライバーの実装](implementing-an-ndis-6-40-driver.md)
- [NDIS 6.40 データ構造体の使用](using-ndis-6-40-data-structures.md)
- [NDIS 6.40 ドライバーのコンパイル](compiling-an-ndis-6-40-driver.md)

 

 





