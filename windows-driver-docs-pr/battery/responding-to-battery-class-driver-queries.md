---
title: バッテリ クラス ドライバー クエリへの応答
description: バッテリ クラス ドライバー クエリへの応答
ms.assetid: 00b24b37-d312-46ee-8218-2bd7a9453d13
keywords:
- バッテリ miniclass ドライバー WDK、ルーチン
- ルーチンの WDK バッテリ
- バッテリ miniclass ドライバー WDK、状態レポート
- WDK のバッテリの状態情報
- クエリの WDK バッテリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffd97504e09fbed7ac9b259ad55cb2f8f810777a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574938"
---
# <a name="responding-to-battery-class-driver-queries"></a>バッテリ クラス ドライバー クエリへの応答


## <span id="ddk_responding_to_battery_class_driver_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_CLASS_DRIVER_QUERIES_DG"></span>


Miniclass ドライバーは、次の 3 つを指定する必要があります[BatteryMini*Xxx* ](https://msdn.microsoft.com/library/windows/hardware/ff536286)ルーチンで、バッテリの状態を報告します。

[*BatteryMiniQueryTag*](https://msdn.microsoft.com/library/windows/hardware/ff536275)

[*BatteryMiniQueryInformation*](https://msdn.microsoft.com/library/windows/hardware/ff536273)

[*BatteryMiniQueryStatus*](https://msdn.microsoft.com/library/windows/hardware/ff536274)

[ **BatteryClassIoctl** ](https://msdn.microsoft.com/library/windows/hardware/ff536267) Ioctl バッテリに関する情報を要求を受信すると、クラス ドライバーのルーチンが miniclass ドライバーのこれらのルーチンを呼び出します。

 

 




