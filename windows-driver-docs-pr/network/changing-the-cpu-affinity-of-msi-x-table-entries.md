---
title: MSI X テーブル エントリの CPU アフィニティの変更
description: MSI X テーブル エントリの CPU アフィニティの変更
ms.assetid: 46ce91ad-76eb-4d05-af9d-a295c665640a
keywords:
- ネットワーク、MSI X テーブル エントリ CPU 関係 MSI X WDK
- メッセージ シグナル割り込み WDK ネットワー キング、MSI X テーブル エントリ CPU 関係
- Msi WDK ネットワー キング、MSI X テーブル エントリ CPU 関係
- WDK MSI X テーブル エントリ CPU 関係をネットワークの中断します。
- CPU af
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fbf3b077c67658fecba9e8d8b36eed8b952aa16
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382775"
---
# <a name="changing-the-cpu-affinity-of-msi-x-table-entries"></a>MSI X テーブル エントリの CPU アフィニティの変更





NDIS 6.1 と MSI X をサポートする以降のミニポート ドライバーを呼び出すことができます、 [ **NdisMConfigMSIXTableEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismconfigmsixtableentry)マスク、マスク解除、または MSI X テーブル エントリをデバイスに割り当てられた MSI X メッセージにマップする関数。 RSS の使用をサポートするミニポート ドライバー **NdisMConfigMSIXTableEntry**実行時に MSI X テーブル エントリの CPU 関係を変更します。

**NdisMConfigMSIXTableEntry**のラッパーです、 [GUID\_MSIX\_テーブル\_CONFIG\_インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff546563)クエリ。 ミニポート ドライバーを呼び出すことができます**NdisMConfigMSIXTableEntry** NDIS 呼び出した後、 [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数、および、からドライバーを返す前に[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)関数。

RSS キューごとに、MSI X テーブルのエントリを割り当てるし、RSS プロセッサの数がで MSI X メッセージ リソースを追加できるよりも少ないキューがミニポート ドライバー、 [ *MiniportFilterResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pnp_irp)関数。 デバイスに割り当てられたリソースを変更する方法の詳細については、次を参照してください。 [MSI X リソース フィルター](msi-x-resource-filtering.md)します。

ミニポート ドライバーは、デバイスがある RSS プロセッサごとに少なくとも 1 つの MSI X メッセージを持つように MSI X 割り込みリソースの CPU 関係を設定できます。 PCI バス ドライバーを最初にマップするメモ、 *n* MSI X テーブル エントリ (場所*n*は NIC ハードウェアは、バスを報告した MSI X テーブル エントリの数です)、最初に*n*変更されたリソースに MSI X メッセージ。 NDIS 後*MiniportInitializeEx*ミニポート ドライバーには、特定の MSI X テーブル エントリ、ドライバーの呼び出しのターゲットのプロセッサが変更されたとき、 **NdisMConfigMSIXTableEntry**そのテーブルのエントリをマップするには既に MSI X メッセージに、アフィニティは、必要なプロセッサを設定します。

 

 





