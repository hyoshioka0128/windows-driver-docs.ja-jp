---
title: プラグアンドプレイイベントの NDIS 処理の概要
description: プラグアンドプレイイベントの NDIS 処理の概要
ms.assetid: 3e9ae945-4241-4c66-bdb1-b9e3466167be
keywords:
- プラグアンドプレイ WDK NDIS ミニポート、IRP 処理 (NIC)
- NIC WDK NDIS の IRP 処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78f9dae42137fb620c9f0d022c758ccacf780461
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565666"
---
# <a name="overview-of-ndis-processing-of-plug-and-play-events"></a>プラグアンドプレイイベントの NDIS 処理の概要





ネットワークインターフェイスカード (NIC) の[関数ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/function-drivers)は、NDIS およびミニポートドライバーのペアとして実装されます。 NIC がシステムに追加されると、NDIS によって NIC 用の機能デバイスオブジェクト (FDO) が作成されます。 その後、NDIS は、この FDO に渡されるプラグアンドプレイ (PnP) と電源管理の Irp を含むすべての Irp を処理します。 NIC のミニポートドライバーは、NIC の操作インターフェイスを提供します。\`

次のセクションでは、NDIS が NIC に代わって PnP Irp を処理する方法について説明します。

[NIC の追加](adding-a-nic.md)

[NIC を開始する](starting-a-nic.md)

[NIC の停止](stopping-a-nic.md)

[NIC の削除](removing-a-nic.md)

[NIC の突然の削除の処理](processing-the-surprise-removal-of-a-nic.md)

 

 





