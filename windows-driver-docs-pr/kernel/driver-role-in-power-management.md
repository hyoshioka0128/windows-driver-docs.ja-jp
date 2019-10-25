---
title: 電源管理でのドライバーの役割
description: 電源管理でのドライバーの役割
ms.assetid: 24b55880-e767-4f18-977e-c4a93332b909
keywords:
- 電源管理 WDK カーネル、のドライバーロール
- システム電源の状態 WDK カーネル、ドライバーロール
- デバイスの電源状態 WDK カーネル
- ドライバーの電源サポートロールの WDk カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e565ef066cbb0476133bd1429aaaf3587a9be92
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836791"
---
# <a name="driver-role-in-power-management"></a>電源管理でのドライバーの役割





ドライバーは、次の2つの方法で電源管理をサポートします。

1.  ドライバーは、電源マネージャーによって発行されたシステム全体の電源要求に応答します。

2.  ドライバーは、個々のデバイスの電源とパフォーマンスの状態を管理します。

すべてのドライバーには、 [**IRP\_MJ\_の電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)要求を処理するための[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンが必要です。 *DispatchPower*ルーチンは、各電源 IRP を検査し、それを処理するか、次の下位のドライバーに渡す必要があります。

デバイスを電源管理に参加させるには、デバイスのデバイススタック内のすべてのドライバーが応答するか、電源 Irp を適切に渡す必要があります。 1つのドライバーを正しく動作させることができないと、システム全体で電源管理が無効になる可能性があります。

デバイスごとに1つのドライバーによって、デバイスの[電源ポリシーが管理](managing-device-power-policy.md)します。 そのドライバーは、独自のデバイススタックに電源 Irp を送信して、デバイス上での電源操作を実行できます。 電源ポリシーマネージャーは、システムの電源 Irp に対応するデバイスの電源 Irp を発行する役割を担います。

さらに、ドライバーは、電源 IRP を受信せずに、デバイスの起動時または電源切断など、特定の電源タスクを実行する場合があります。 これらは暗黙的な電源要求と見なされます。

詳細については、「[ドライバーの電源管理の役割](power-management-responsibilities-for-drivers.md)」を参照してください。

 

 




