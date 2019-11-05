---
title: デバイスの電源機能のレポート
description: デバイスの電源機能のレポート
ms.assetid: 67a504d0-2c41-4c74-a912-4f0771885f7d
keywords:
- レポートデバイスの電源機能
- デバイスの電源機能 WDK カーネル
- DEVICE_CAPABILITIES 構造体
- クエリ機能の Irp WDK 電源管理
- Irp WDK 電源管理
- I/o 要求パケットの WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a17e9f0d089d6c7c87e9b76cfc39a2164686c885
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838452"
---
# <a name="reporting-device-power-capabilities"></a>デバイスの電源機能のレポート





列挙中に、ドライバーは PnP IRP\_に応答してデバイス固有の情報を報告し、 [ **\_機能要求\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)を実行します。 その他の情報と共に、ドライバーはデバイス[ **\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造にデバイスの電源管理機能を報告します。 通常、バスドライバーはこの構造体にデータを格納します。

上位レベルのドライバーでは、構造のローカルコピーを作成し、適切な値が含まれていることを確認できるように、クエリ機能の IRP の[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定する必要があります。 一般的な規則として、上位レベルのドライバーでは、これらの値を変更しないでください。 ただし、変更が必要な場合、ドライバーはデバイスの機能をさらに制限することができますが、追加することはできません。 つまり、ドライバーは、規則の制限を厳しくすることができますが、それらを緩めることはできません。

IRP が完了し、すべてのドライバーの完了ルーチンが実行されると、構造はキャッシュされ、ドライバーはその内容を変更できません。

**デバイス\_機能**の構造体の次のメンバーは、電源管理に関連しています。

[DeviceD1 と DeviceD2](deviced1-and-deviced2.md)

[WakeFromD0、WakeFromD1、WakeFromD2、および WakeFromD3](wakefromd0--wakefromd1--wakefromd2--and-wakefromd3.md)

[DeviceState](devicestate.md)

[SystemWake](systemwake.md)

[DeviceWake](devicewake.md)

[D1Latency、D2Latency、D3Latency](d1latency--d2latency--and-d3latency.md)

 

 




