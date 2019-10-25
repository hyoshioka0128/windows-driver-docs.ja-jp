---
title: MSI X テーブル エントリの CPU アフィニティの変更
description: MSI X テーブル エントリの CPU アフィニティの変更
ms.assetid: 46ce91ad-76eb-4d05-af9d-a295c665640a
keywords:
- MSI-X WDK ネットワーク, MSI-X テーブルエントリ CPU アフィニティ
- メッセージシグナル割り込み (WDK ネットワーク)、MSI-X テーブルエントリ CPU アフィニティ
- Msi WDK ネットワーク, MSI-X テーブルエントリ CPU アフィニティ
- WDK ネットワークの割り込み、MSI-X テーブルエントリの CPU アフィニティ
- CPU af
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2962e7f51759affa24110960eabda5141809df99
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835203"
---
# <a name="changing-the-cpu-affinity-of-msi-x-table-entries"></a>MSI X テーブル エントリの CPU アフィニティの変更





MSI をサポートする NDIS 6.1 およびそれ以降のミニポートドライバーでは、 [**NdisMConfigMSIXTableEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismconfigmsixtableentry)関数を呼び出して、デバイスによって割り当てられた Msi-x メッセージに対して、msi x のテーブルエントリをマスク、マスク解除、またはマップすることができます。 RSS をサポートするミニポートドライバーは、 **NdisMConfigMSIXTableEntry**を使用して、実行時に MSI X のテーブルエントリの CPU 関係を変更します。

**NdisMConfigMSIXTableEntry**は、 [GUID\_MSIX\_TABLE\_CONFIG\_インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff546563)クエリのラッパーです。 ミニポートドライバーは、NDIS が[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出した後、ドライバーが[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数から戻る前に、 **NdisMConfigMSIXTableEntry**を呼び出すことができます。

各 RSS キューに MSI-X テーブルエントリを割り当て、RSS プロセッサ数よりも多くのキューを使用するミニポートドライバーでは、 [*MiniportFilterResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)関数に Msi-x メッセージリソースを追加できます。 デバイスに割り当てられたリソースを変更する方法の詳細については、「 [MSI-X リソースのフィルター処理](msi-x-resource-filtering.md)」を参照してください。

ミニポートドライバーは、デバイスが各 RSS プロセッサに対して少なくとも1つの MSI-X メッセージを保持するように、MSI-X 割り込みリソースの CPU 関係を設定できます。 PCI バスドライバーは、最初に*n 個*の Msi-x テーブルエントリをマップします (ここで、 *n*は NIC ハードウェアによってバスに報告された msi x テーブルエントリの数)。これは、変更されたリソースの最初の*n 個*の msi-x メッセージに対応しています。 NDIS 呼び出し*MiniportInitializeEx*の後、ミニポートドライバーが特定の MSI-x テーブルエントリのターゲットプロセッサを変更すると、ドライバーは**NdisMConfigMSIXTableEntry**を呼び出して、そのテーブルエントリを既に存在する msi-x メッセージにマップします。目的のプロセッサに設定された関係。

 

 





