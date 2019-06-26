---
title: デバイスの電源機能のレポート
description: デバイスの電源機能のレポート
ms.assetid: 67a504d0-2c41-4c74-a912-4f0771885f7d
keywords:
- デバイスの電源機能をレポート
- デバイスの電源機能 WDK カーネル
- DEVICE_CAPABILITIES 構造体
- クエリ機能 Irp WDK の電源管理
- Irp WDK の電源管理
- I/O 要求パケット WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ca69ef60db256d4e4fc479b81d842a685057106
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373407"
---
# <a name="reporting-device-power-capabilities"></a>デバイスの電源機能のレポート





ドライバーは、列挙中に、PnP への応答でデバイスに固有の情報を報告[ **IRP\_MN\_クエリ\_機能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)要求。 ドライバーがデバイスの電源管理機能を報告するこのような他の情報と共に、 [**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)構造体。 通常、バス ドライバーは、この構造体に格納します。

高度なドライバーを設定する必要があります、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)クエリ機能の日常的な IRP のため、構造体のローカル コピーを作成していることを確認できますが含まれている適切な値には。 一般的な規則としてより高度なドライバーはこれらの値を変更しないでください。 ただし、変更が必要な場合は、ドライバーがデバイスの機能をさらに制限できますに追加することはできません。 つまり、ドライバーより制限の厳しいルールを作成できますが、それらを緩めることはできません。

IRP が完了し、すべてのドライバーの完了のルーチンが実行されている後、は、構造体がキャッシュされ、ドライバーは、その内容を変更できません。

次のメンバー、**デバイス\_機能**構造体は、電源管理に関連します。

[DeviceD1 と DeviceD2](deviced1-and-deviced2.md)

[WakeFromD0、WakeFromD1、WakeFromD2、および WakeFromD3](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)

[deviceState](devicestate.md)

[SystemWake](systemwake.md)

[DeviceWake](devicewake.md)

[D1Latency、D2Latency、および D3Latency](d1latency--d2latency--and-d3latency.md)

 

 




