---
title: NIC の LSOV1 TCP パケット セグメンテーション機能のレポート
description: NIC の LSOV1 TCP パケット セグメンテーション機能のレポート
ms.assetid: 976f5943-a50e-413b-8520-e280b04122f9
keywords:
- LSOV1 WDK ネットワーク
- 大きな TCP パケットのセグメント化 WDK ネットワーク
- 大きな TCP パケットの WDK ネットワー キングのセグメント化
- タスクのオフロード LSOV1 と LSOV2 の WDK TCP/IP トランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5af5c69dbc43f8718d44bbc68743ceb19f4a756f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380881"
---
# <a name="reporting-a-nics-lsov1-tcp-packet-segmentation-capabilities"></a>NIC の LSOV1 TCP パケット セグメンテーション機能のレポート





NDIS ミニポート ドライバーが現在の大量送信オフロード バージョン 1 (LSOV1) を指定します - TCP パケットのセグメント化の構成では、NIC の[ **NDIS\_TCP\_LARGE\_送信\_オフロード\_V1** ](https://msdn.microsoft.com/library/windows/hardware/ff567883)構造体。ミニポート ドライバーで現在 LSOV1 オフロードの構成を含める必要があります、 [ **NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565930)構造体。 ミニポート ドライバーの呼び出し、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数を[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数を渡す、NDIS 情報\_ミニポート\_アダプター\_オフロード\_属性。

ミニポート ドライバーが存在する場合に LSOV1 構成では、変更を報告する必要がありますで、 [ **NDIS\_状態\_タスク\_オフロード\_現在\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff567424)状態を示す値。

クエリに対する応答で[OID\_TCP\_オフロード\_現在\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805)、NDIS には、NDIS が含まれています\_TCP\_LARGE\_送信\_オフロード\_V1 構造、 [ **NDIS\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566599) NDIS を表す構造体、 **InformationBuffer**のメンバー[ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体。 NDIS は、ミニポート ドライバーが提供される情報を使用します。

NDIS サポートする多数の送信は、LSO の拡張のバージョンは、バージョン 2 (LSOV2) をオフロードします。 LSOV2 機能に関する詳細については、次を参照してください。[レポート NIC の LSOV2 TCP パケットのセグメンテーション機能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)します。

ミニポート ドライバーは、NDIS で、次の情報を指定する必要があります\_TCP\_LARGE\_送信\_オフロード\_V1 構造体。

-   カプセル化の設定で、**カプセル化**メンバー。 このメンバーの詳細については、「解説」セクションを参照してください。 [ **NDIS\_TCP\_LARGE\_送信\_オフロード\_V1**](https://msdn.microsoft.com/library/windows/hardware/ff567883)します。

-   TCP/IP トランスポートは大きな TCP パケットの場合に、ミニポート ドライバーで渡すことができるユーザー データの最大バイト数、 **MaxOffLoadSize**メンバー。 最大サイズは 64 K バイトを超えることはできません。

-   TCP/IP トランスポート オフロードできますが、セグメント化の NIC にで前に、大きな TCP パケットがで割り切れるする必要があるセグメントの最小数、 **MinSegmentCount**メンバー。

-   かどうか、NIC は、TCP オプションを含む大きな TCP パケットを分割することができます。

-   かどうか、NIC は、IPv4 のオプションを含む大きな TCP パケットを分割することができます。

## <a name="related-topics"></a>関連トピック


[タスクのオフロード機能を判断します。](determining-task-offload-capabilities.md)

 

 






