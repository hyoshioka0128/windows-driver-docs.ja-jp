---
title: システム電源の状態の処理の要求
description: システム電源の状態の処理の要求
ms.assetid: c4547b72-107e-4335-a7bd-081376962da0
keywords:
- 電源の状態の WDK カーネル
- 電源管理の WDK カーネルの電源状態を要求します。
- システム電源の状態の WDK カーネル、電源状態の要求します。
- WDK の要求の電源管理
- Irp WDK の電源管理
- I/O 要求パケット WDK 電源管理
- 要求 WDK カーネルの電源
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85334d5348cfa4eac7a4ff357bbac2eb033bda9a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538513"
---
# <a name="handling-system-power-state-requests"></a>システム電源の状態の処理の要求





すべてのドライバーは、システムがスリープ、休止状態、および正常に起動する場合に、システム電源の状態要求に応答できる必要があります。 デバイスの変更用のドライバー、[デバイスの電源状態](device-power-states.md)のデバイスには、システム電源の状態要求に応答します。

すべてのドライバー サポート システムの電源管理しない場合は、個々 のデバイスがスリープし、復帰が電源マネージャーはスリープ状態に全体として、システムを配置することはできません。

次のトピックでは、システム電源の状態要求の処理の詳細を説明します。

[システム電源の状態](system-power-states.md)

[システム電源ポリシー](system-power-policy.md)

[システム電源の状態の変更の防止](preventing-system-power-state-changes.md)

[IRP の処理\_MN\_クエリ\_システム電源の状態の電源](handling-irp-mn-query-power-for-system-power-states.md)

[IRP の処理\_MN\_設定\_システム電源の状態の電源](handling-irp-mn-set-power-for-system-power-states.md)

 

 




