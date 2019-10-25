---
title: バッテリ クラス ドライバー クエリへの応答
description: バッテリ クラス ドライバー クエリへの応答
ms.assetid: 00b24b37-d312-46ee-8218-2bd7a9453d13
keywords:
- バッテリ miniclass ドライバー WDK、ルーチン
- ルーチン WDK バッテリ
- バッテリ miniclass ドライバー WDK、ステータスレポート
- ステータス情報 WDK バッテリ
- WDK バッテリのクエリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d24b352eda33f8b83e2196459b0cb54d74e595c4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833988"
---
# <a name="responding-to-battery-class-driver-queries"></a>バッテリ クラス ドライバー クエリへの応答


## <span id="ddk_responding_to_battery_class_driver_queries_dg"></span><span id="DDK_RESPONDING_TO_BATTERY_CLASS_DRIVER_QUERIES_DG"></span>


Miniclass ドライバーは、次の3つの[BatteryMini*Xxx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_battery/)ルーチンを提供する必要があります。これは、バッテリの状態を報告します。

[*BatteryMiniQueryTag*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_tag_callback)

[*BatteryMiniQueryInformation*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_information_callback)

[*BatteryMiniQueryStatus*](https://docs.microsoft.com/windows/desktop/api/batclass/nc-batclass-bclass_query_status_callback)

クラスドライバーの[**BatteryClassIoctl**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassioctl)ルーチンは、バッテリに関する情報を要求する ioctl を受信するときに、これらの miniclass ドライバールーチンを呼び出します。

 

 




