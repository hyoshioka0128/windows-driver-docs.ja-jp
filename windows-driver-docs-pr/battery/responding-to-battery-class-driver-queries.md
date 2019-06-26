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
ms.openlocfilehash: 6b8f9cb79f9edf97952b1dc3947a0f4bbcac281a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364744"
---
# <a name="responding-to-battery-class-driver-queries"></a>バッテリ クラス ドライバー クエリへの応答


## <span id="ddk_responding_to_battery_class_driver_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_CLASS_DRIVER_QUERIES_DG"></span>


Miniclass ドライバーは、次の 3 つを指定する必要があります[BatteryMini*Xxx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_battery/)ルーチンで、バッテリの状態を報告します。

[*BatteryMiniQueryTag*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_tag_callback)

[*BatteryMiniQueryInformation*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_information_callback)

[*BatteryMiniQueryStatus*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_status_callback)

[ **BatteryClassIoctl** ](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassioctl) Ioctl バッテリに関する情報を要求を受信すると、クラス ドライバーのルーチンが miniclass ドライバーのこれらのルーチンを呼び出します。

 

 




