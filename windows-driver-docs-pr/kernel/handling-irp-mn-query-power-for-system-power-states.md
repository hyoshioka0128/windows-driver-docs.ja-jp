---
title: システム電源状態についての IRP_MN_QUERY_POWER の処理
description: システム電源状態についての IRP_MN_QUERY_POWER の処理
ms.assetid: 1904a1cb-a220-41cc-8894-5f90919e7383
keywords:
- IRP_MN_QUERY_POWER
- システム電源の状態の WDK カーネル、IRP_MN_QUERY_POWER
- クエリ power Irp WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12706c591573a995b3d796d4e22e8d43c35a7e7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385627"
---
# <a name="handling-irpmnquerypower-for-system-power-states"></a>IRP の処理\_MN\_クエリ\_システム電源の状態の電源





電源マネージャー送信 IRP のコードを少しで累乗 IRP [ **IRP\_MN\_クエリ\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)と**SystemPowerState**で**Parameters.Power.Type**を指定したシステム電源の状態 (S1 S5) に安全に変更できるかどうかを判断して、このような変更を準備するドライバーを許可します。

電源マネージャーが送信する前にクエリ可能であれば、 [ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)低 (小さい電源) 状態を要求します。 ただし、バッテリの故障の場合、または停電が迫っていないか、電源マネージャー セット power IRP せず送信まずクエリを実行します。 電源マネージャー システムを動作状態 (S0) に設定するのには IRP を送信する前にクエリを送信します。

デバイスの電源ポリシーの所有者がシステム クエリ性能の要求を処理する方法については、次を参照してください。[電源ポリシー所有者のデバイスでのシステム クエリ Power IRP の処理](handling-a-system-query-power-irp-in-a-device-power-policy-owner.md)します。

(デバイスの電源ポリシー所有者ではない) ドライバーがシステム クエリ性能の要求を処理する方法については、次を参照してください。

[フィルターまたは関数のドライバーでのシステム クエリ Power IRP の処理](handling-a-system-query-power-irp-in-a-filter-or-function-driver.md)

[フィルターまたは関数のドライバーでのシステム クエリ Power IRP の失敗](failing-a-system-query-power-irp-in-a-filter-or-function-driver.md)

[バス ドライバーでのシステム クエリ Power IRP の処理](handling-a-system-query-power-irp-in-a-bus-driver.md)

ドライバーがデバイスに送信する必要がありますしないに注意してください。 **IRP\_MN\_設定\_POWER**システム クエリに対する応答の要求はシステム セット電源要求を受信した後にのみ、このような IRP を要求します。

電源マネージャーは、システム上の各デバイス スタックに IRP のシステム クエリを送信するための 1 つのデバイス ドライバーは正常に完了の他のデバイス ドライバーは、クエリを失敗可能性があることができます。 Windows Vista 以降、スリープ状態にシステムの電源状態の変更は、重要な電源状態の変更です。 ドライバーが IRP のクエリ機能、Windows Vista の電源マネージャー可能性がありますが、システムが失敗した場合でも、スリープ状態にシステムの電源状態を変更します。 期限切れ、バッテリに可能性があります、クエリがアクティブな間、即座にシャット ダウンを必要とすることもできます。 その結果、クエリー IRP の後、ドライバーは次電源の Irp を受信する準備する必要があります。

-   **IRP\_MN\_設定\_POWER**クエリ対象の状態

-   **IRP\_MN\_設定\_POWER**別の電源の状態

-   **IRP\_MN\_設定\_POWER**を現在の電源の状態

-   **IRP\_MN\_クエリ\_POWER**任意の状態

ドライバーがシステム セット電源を受け取るただし、通常、IRP の次のシステムは IRP をクエリします。 関係なく、ドライバーがドライバーには、クエリ性能 IRP が失敗した場合でも、システムの電源状態を変更する準備があります。

 

 




