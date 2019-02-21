---
title: システム電源の状態の IRP_MN_SET_POWER の処理
description: システム電源の状態の IRP_MN_SET_POWER の処理
ms.assetid: 21e8e8a7-ca77-445b-a49e-28a53f431a26
keywords:
- IRP_MN_SET_POWER
- システム電源の状態の WDK カーネル、IRP_MN_SET_POWER
- セット power Irp WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36e2048aac516b4420188cbbd383317396f67956
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527975"
---
# <a name="handling-irpmnsetpower-for-system-power-states"></a>IRP の処理\_MN\_設定\_システム電源の状態の電源





電源マネージャー送信電源コードの軽微なを指定する IRP [ **IRP\_MN\_設定\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)と次の理由の 1 つのシステム電源の状態。

-   システム電源の状態を変更します。

-   失敗した後、現在の電源状態のことを再確認する[ **IRP\_MN\_クエリ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)要求。

I/O マネージャーを通じて電源マネージャーは IRP を PnP デバイスの各ノードでデバイス スタックの最上位のドライバーに送信します。 IRP では、適切なシステム電源の状態の履歴内のすべてのドライバーに通知します。

所定のスタートアップを確実には、電源マネージャー シーケンス システムの電源を Irp その子の実行前に、親デバイスで power する機会が与えようにします。 電源マネージャーで、システムに送信する前に、照会されません IRP の電源投入します。

同様に、コンピューターがスリープ モードや、シャット ダウンを正しい方法で確実に、電源マネージャー送信システムで定義された一連の場合は、スリープ、休止状態またはシャット ダウンを指定する Irp ルートからのデバイスのルートに近いデバイスの前に電源を切るようにします。 可能であれば、このような IRP を送信する前に、電源マネージャーに照会します。 詳細については、次を参照してください。 [IRP の処理\_MN\_クエリ\_システム電源の状態のための電力](handling-irp-mn-query-power-for-system-power-states.md)します。

システム電源 IRP が電源状態の変更を直接要求ではありません — 通知します。 ドライバーへの直接応答として、デバイスの電源状態を変更する必要があります、*システム*IRP; の電源をドライバーへの応答でのみ、そのデバイスの電源状態の変更、*デバイス*IRP の電源をします。 (デバイスの電源ポリシー所有者には、デバイスの電源 IRP は送信しますを参照してください[電源ポリシー所有者のデバイスでシステム セット Power IRP の処理](handling-a-system-set-power-irp-in-a-device-power-policy-owner.md)。)。

各ドライバーがシステムを渡す必要がありますそれにもかかわらず、デバイスは、要求されたシステムの電源状態の有効なデバイスの電源状態で既にが、場合でも、次の下位ドライバー、バス ドライバーに到達するまでにセット power IRP します。 この IRP の完了、バス ドライバーのみが許可されます。

ドライバーでのこの IRP の処理方法は、次のセクションで説明されている、デバイス スタックにおけるその役割にによって異なります。

[デバイスの電源ポリシー所有者にシステム セット Power IRP の処理](handling-a-system-set-power-irp-in-a-device-power-policy-owner.md)

[バス ドライバーではシステム セット Power IRP の処理](handling-a-system-set-power-irp-in-a-bus-driver.md)

[フィルター ドライバーではシステム セット Power IRP の処理](handling-a-system-set-power-irp-in-a-filter-driver.md)

ドライバーが失敗することはできません、 **IRP\_MN\_設定\_POWER**システム電源の状態を設定する要求。 電源マネージャーは、この IRP の返されたすべてのエラー状態を無視します。

 

 




