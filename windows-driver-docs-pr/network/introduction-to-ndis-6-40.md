---
title: NDIS 6.40 の概要
description: このセクションでは、NDIS 6.40 を紹介し、その主要な設計の追加機能について説明します。 NDIS 6.40 は、Windows 8.1 と Windows Server 2012 R2 に含まれる以降です。
ms.assetid: 46DB94AA-DBAD-49E0-A1F0-FEB095E26F2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4d3253b9acb6a29120d31915b067efca58c421a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571812"
---
# <a name="introduction-to-ndis-640"></a>NDIS 6.40 の概要


このセクションでは、Network Driver Interface Specification (NDIS) 6.40 を紹介し、その主要な設計の追加機能について説明します。 Windows 8.1 と Windows Server 2012 R2 以降のオペレーティング システムでは、NDIS 6.40 が含まれます。

## <a name="feature-updates"></a>機能更新プログラム


Windows 8.1 および Windows Server 2012 R2 は、次の機能にマイナー更新プログラムを導入します。

### <a name="ndkpi"></a>NDKPI

NDKPI 1.2 には、NDKPI DDI に、次の新しい要素が追加されます。

- *NdkSendAndInvalidate* ([*NDK\_FN\_送信\_AND\_INVALIDATE*](https://msdn.microsoft.com/library/windows/hardware/dn265507)) 関数
- *NdkGetCqResultsEx* ([*NDK\_FN\_取得\_CQ\_結果\_EX*](https://msdn.microsoft.com/library/windows/hardware/dn265506)) 関数
- [**NDK\_結果\_EX** ](https://msdn.microsoft.com/library/windows/hardware/dn265509)構造体
- 新しい要求のコールバック*フラグ*値。**NDK\_OP\_FLAG\_DEFER**
- 新しい[ **NDK\_アダプター\_情報**](https://msdn.microsoft.com/library/windows/hardware/hh439851)**AdapterFlags**値。**NDK\_ADAPTER\_FLAG\_RDMA\_READ\_LOCAL\_INVALIDATE\_SUPPORTED**

### <a name="native-80211-wireless-lan"></a>ネイティブの 802.11 ワイヤレス LAN

IEEE 802.11 ac が非常に高いスループット (VHT) PHY になりました。 次の DDI 要素が更新されました。

- [**DOT11\_PHY\_型**](https://msdn.microsoft.com/library/windows/hardware/ff548741)列挙型
- [OID\_DOT11\_現在\_チャネル](https://msdn.microsoft.com/library/windows/hardware/ff569127)
- [OID\_DOT11\_サポートされている\_PHY\_型](https://msdn.microsoft.com/library/windows/hardware/ff569426)
- [OID\_DOT11\_サポートされている\_OFDM\_頻度\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff569425)

## <a name="sample-and-documentation-updates"></a>サンプルとドキュメントの更新

[HYPER-V 拡張可能スイッチの拡張機能のサンプルを転送](https://go.microsoft.com/fwlink/p/?LinkId=617913)ハイブリッド転送を実装するために更新されました。

次のドキュメントのセクションでは、追加または大幅に拡張されました。

-   [NDIS 6.30 する NDIS 6.x ドライバーの移植](porting-ndis-6-x-drivers-to-ndis-6-30.md)
-   [ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)設計ガイド
-   [Generic Routing Encapsulation (NVGRE) タスク オフロードを使用してネットワーク仮想化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)
-   [Receive Segment Coalescing (RSC)](receive-segment-coalescing--rsc-.md)設計ガイド
-   [記述について HYPER-V 拡張可能スイッチの拡張機能](getting-started-writing-a-hyper-v-extensible-switch-extension.md)
-   [NVGRE タスク オフロードのリファレンス](https://msdn.microsoft.com/library/windows/hardware/dn197221)

NetDMA インターフェイスは、Windows 8 および Windows Server 2012 でサポートされている以降ではありません。 これを反映するようにドキュメントが更新されているようになりました。

ここでは、次のトピックについて説明します。

- [実装 6.40、NDIS ドライバー](implementing-an-ndis-6-40-driver.md)
- [NDIS 6.40 データ構造を使用](using-ndis-6-40-data-structures.md)
- [コンパイル 6.40、NDIS ドライバー](compiling-an-ndis-6-40-driver.md)

 

 





