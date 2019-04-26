---
title: 電源 IRP の処理
description: 電源 IRP の処理
ms.assetid: 0fe4f27a-101d-41af-8f00-fb36da5dc793
keywords:
- 電源管理の WDK カーネル、Irp
- Irp WDK の電源管理
- 電源 Irp WDK カーネルでは、電源 Irp について
- IRP_MJ_POWER
- IRP_MN_QUERY_POWER
- IRP_MN_SET_POWER
- IRP_MN_WAIT_WAKE
- IRP_MN_POWER_SEQUENCE
- 電源の状態の WDK カーネル
- WDK の電源管理を状態します。
- 電源の状態の WDK カーネルを変更します。
- WDK カーネルの電源を節約します。
- スリープの電源管理の WDK カーネル
- 電源状態のクエリを実行します。
- WDK のスリープ状態のデバイスの電源管理
- I/O 要求パケット WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e0525d2ac28ad6e37efde2b9fdbe5a12b1beb46
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350020"
---
# <a name="handling-power-irps"></a>電源 IRP の処理





ドライバーで電源 Irp の処理、 [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。 主要な IRP コードがあるすべての電源管理の要求[ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)し、次の小さなコードのいずれか。

[**IRP\_MN\_クエリ\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551699) : 電源の状態の変更が可能かどうかを判断するクエリ

[**IRP\_MN\_設定\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744) — 1 つの電源の状態から別の変更を要求

[**IRP\_MN\_待機\_WAKE**](https://msdn.microsoft.com/library/windows/hardware/ff551766) — 要求自体またはシステムをスリープ解除するデバイスを有効にします。

[**IRP\_MN\_POWER\_シーケンス**](https://msdn.microsoft.com/library/windows/hardware/ff551644) -特定のデバイスへの復元の電源を最適化するために情報を要求します。

サポート**IRP\_MN\_設定\_POWER**と**IRP\_MN\_クエリ\_POWER**が必要です。 これらの Irp を処理するためにすべてのドライバーを準備する必要があります。

サポート**IRP\_MN\_待機\_WAKE**の外部からの信号への応答がスリープ解除できる任意のデバイスのデバイス スタックのすべてのドライバーが必要です。 ドライバーは、ウェイク アップについては、デバイスを有効にするには、この IRP を送信します。

サポート**IRP\_MN\_POWER\_シーケンス**は省略可能です。 この IRP では、電源を復旧する長い時間がかかるデバイスの最適化を提供します。

電源の IRP には、システムの電源操作またはデバイスの電源操作を指定できます。 [Irp のシステム電源](power-irps-for-the-system.md)と[Irp の個々 のデバイスの電源を](power-irps-for-individual-devices.md)次のセクションで説明したようにデバイス スタックを若干異なるパスを取得します。

 

 




