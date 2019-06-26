---
title: 電源管理のマイナー IRP
description: 電源管理のマイナー IRP
ms.date: 08/12/2017
ms.assetid: 8af0609f-168b-4455-aae8-1a3c9e40ed47
ms.localizationpriority: medium
ms.openlocfilehash: 557e39d900ee834c036b2b6180ff28647d5553dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374199"
---
# <a name="power-management-minor-irps"></a>電源管理のマイナー IRP





Irp のすべてのパワーが大規模なコードがある[ **IRP\_MJ\_POWER** ](irp-mj-power.md)と特定の電源管理の要求を示す、次の小さなコードのいずれか。

[**IRP\_MN\_POWER\_シーケンス**](irp-mn-power-sequence.md)

[**IRP\_MN\_クエリ\_電源**](irp-mn-query-power.md)

[**IRP\_MN\_SET\_POWER**](irp-mn-set-power.md)

[**IRP\_MN\_待機\_WAKE**](irp-mn-wait-wake.md)

このセクションでは、アルファベット順で個々 の Irp の参照情報を提供します。 タイミングの詳細については、Irp が送信され、ドライバーは、それらを処理する必要がある方法を参照してください。[電源管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-power-management)します。 電源管理 セクションには、電源管理と用語の概要も含まれています。

 

 




