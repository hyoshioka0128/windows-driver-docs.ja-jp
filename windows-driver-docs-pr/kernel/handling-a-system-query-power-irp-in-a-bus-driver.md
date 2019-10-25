---
title: バス ドライバーでのシステム電源クエリ IRP の処理
description: バス ドライバーでのシステム電源クエリ IRP の処理
ms.assetid: d42c268e-d57d-41a6-8e61-67c651082106
keywords:
- クエリ-電源 Irp の WDK 電源管理
- バスドライバーの WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0f03933e8352496b638d8cf612bf4b11f0be7f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836632"
---
# <a name="handling-a-system-query-power-irp-in-a-bus-driver"></a>バス ドライバーでのシステム電源クエリ IRP の処理





システムクエリ-電源要求がバスドライバー (デバイスの電源ポリシー所有者ではない) に到達すると、ドライバーは、照会されたシステムの電源状態に対応するデバイスの電源状態をサポートできるようにします。ウェイクアップが有効になっている場合は、クエリを実行したシステム電源状態が原因で、デバイスがシステムをスリープ解除できなくなることはありません。

Windows 7 と Windows Vista では、バスドライバーが**Irp&gt;iostatus. status**\_を、指定された電源状態に変更できる場合は [成功] を、ドライバーができない場合はエラー状態を設定するように設定します。

Windows Server 2003、Windows XP、および Windows 2000 では、バスドライバーはまず[**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出し、 **Irp&gt;iostatus**を設定します。これは、ドライバーが指定の電源状態に変更されるか、またはエラーが発生した場合に、状態\_成功に設定されます。ドライバーができない場合の状態。

バスドライバーが IRP を完了すると、電源マネージャーは、IRP がスタックに渡されたときに他のドライバーによって設定された[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを呼び出します。

 

 




