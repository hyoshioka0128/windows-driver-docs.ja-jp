---
title: 正しいデバイス電源状態の判断
description: 正しいデバイス電源状態の判断
ms.assetid: 4acefe93-1d7a-4c12-8701-03c2a8929591
keywords:
- DEVICE_CAPABILITIES 構造体
- 適切なデバイスの電源状態が WDK 電源管理
- デバイスの電源状態が WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d52a4beea6eb55f1e75bdc37fa76a8f127d804c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371271"
---
# <a name="determining-the-correct-device-power-state"></a>正しいデバイス電源状態の判断





電源ポリシーの所有者のチェック、 [ **DeviceState** ](devicestate.md)配列、 [**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)を決定します。各システムの電源状態のデバイスの電源状態の有効な範囲です。 配列には、各システムの電源状態の基になるデバイスをサポートできる最も高いデバイスの電源状態が一覧表示します。

この範囲から特定の状態を選択するときに、次の操作を考慮してください。

-   ほとんどのデバイスは、システム S0 状態になったときに、D0 状態を入力します。

-   ほとんどのデバイスは、システムがスリープ状態に入ったときに、D3 の状態を入力します。 ただし、このような状態をサポートしている場合、ウェイク アップを有効になっているデバイスは D1 または D2 を代わりに、入力する必要あります。 詳細については、次を参照してください。[デバイスの電源機能の報告](reporting-device-power-capabilities.md)します。

-   休止状態ファイルを保持するデバイスの特別な規則が適用されます。 システム IRP を要求した場合**PowerSystemHibernate**、休止状態ファイルを保持するデバイスの電源を切らないでする必要があります。 このようなデバイスの電源ポリシー所有者必要があります D3 デバイスの電源状態を要求し、コンテキストを保存が、デバイスのドライバーのデバイスの電源を電源する必要があります。

システム IRP を要求する場合**PowerSystemShutdown**、ドライバーは、電源を確認する必要があります\_のアクション値**Irp -&gt;Parameters.Power.ShutdownType**原因を特定するには状態の変更。 詳細については、次を参照してください。[システム電源操作](system-power-actions.md)します。

デバイスの電源ポリシー所有者は、デバイスを送信する必要がありますの各システム セット power IRP セット power IRP、デバイスは既に正しいデバイスの電源状態の場合でも。 以前に、ドライバーは、デバイスの操作を中断クエリ power IRP への応答で、セット power IRP によって Irp のキューを停止して、現在の電源状態の通常の操作に戻ることが通知されます。 唯一の例外は、デバイスが、D3 状態ときに発生します。この場合、ドライバー必要がある送信しない追加[ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) D3 を要求します。

 

 




