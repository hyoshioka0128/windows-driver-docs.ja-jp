---
title: NIC の LSOV2 TCP パケット セグメンテーション機能のレポート
description: NIC の LSOV2 TCP パケット セグメンテーション機能のレポート
ms.assetid: 2894c1a8-503f-4b53-8eb3-5c5eaea150db
keywords:
- LSOV2 WDK ネットワーク
- 大きな TCP パケットのセグメント化 WDK ネットワーク
- 大きな TCP パケットの WDK ネットワー キングのセグメント化
- タスクのオフロード LSOV1 と LSOV2 の WDK TCP/IP トランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3d4106176ec1f63560cc5a919c16562df2e2a57
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581859"
---
# <a name="reporting-a-nics-lsov2-tcp-packet-segmentation-capabilities"></a>NIC の LSOV2 TCP パケット セグメンテーション機能のレポート





NDIS ミニポート ドライバーが現在大量送信オフロード バージョン 2 (LSOV2) を指定では、NIC の構成を TCP パケットのセグメンテーションを[ **NDIS\_TCP\_LARGE\_送信\_オフロード\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff567884)構造体。ミニポート ドライバーでは、現在の LSOV2 構成を含める必要があります、 [ **NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565930)構造体。 ミニポート ドライバーの呼び出し、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数を[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数を渡す、NDIS 情報\_ミニポート\_アダプター\_オフロード\_属性。

ミニポート ドライバーが存在する場合に LSOV2 構成では、変更を報告する必要がありますで、 [ **NDIS\_状態\_タスク\_オフロード\_現在\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff567424)状態を示す値。

クエリに対する応答で[OID\_TCP\_オフロード\_現在\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805)、NDIS には、NDIS が含まれています\_TCP\_LARGE\_送信\_オフロード\_V2 構造、 [ **NDIS\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566599) NDIS を表す構造体、 **InformationBuffer**のメンバー[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体。 NDIS は、ミニポート ドライバーが提供される情報を使用します。

LSOV2 ハードウェアをサポートしているミニポート ドライバーが LSOV1 をサポートする必要がありますもことをお勧めします。 このサポートは、NDIS 5 の場合は、LSOV1 を使用する TCP/IP トランスポートを有効になります。*x*ミニポート アダプタ上で中間ドライバーがインストールされています。 LSOV1 機能に関する詳細については、次を参照してください。[レポート NIC の LSOV1 TCP パケットのセグメンテーション機能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)します。

LSOV2 には、IPv4 と IPv6 パケットがサポートされています。 ミニポート ドライバーは、IPv4 と IPv6 の両方に対して、次の情報を指定する必要があります、 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff567884)構造体。

-   カプセル化の設定で、**カプセル化**メンバー。 このメンバーの詳細については、「解説」セクションを参照してください。 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_V2**](https://msdn.microsoft.com/library/windows/hardware/ff567884)します。

-   TCP/IP トランスポートは大きな TCP パケットの場合に、ミニポート ドライバーで渡すことができるユーザー データの最大バイト数、 **MaxOffLoadSize**メンバー。

-   TCP/IP トランスポート オフロードできますが、セグメント化の NIC にで前に、大きな TCP パケットがで割り切れるする必要があるセグメントの最小数、 **MinSegmentCount**メンバー。

## <a name="related-topics"></a>関連トピック


[タスクのオフロード機能を判断します。](determining-task-offload-capabilities.md)

 

 






