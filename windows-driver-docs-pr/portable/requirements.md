---
Description: 必要条件
title: 要件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65cfd58a71c6da5af4bfed01d51d8a48bc9b1835
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376222"
---
# <a name="requirements"></a>要件


Windows ポータブル デバイス (WPD) ドライバーを作成するには、最新いる必要があります[Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p/?linkid=178709)コンピューターにインストールします。 必要なヘッダーとライブラリ ファイルは、次のリストに表示され、WDK に含まれます。

-   *PortableDeviceGuids.lib*
-   *PortableDeviceClassExtension.h*
-   *PortableDeviceTypes.h*
-   *PortableDevice.h*
-   その他の任意の必要なライブラリまたはユーザー モード ドライバー フレームワーク (UMDF) によって必要なヘッダー ファイル。

ドライバーは、新しいデバイスのサービス モデルをサポートする場合、次のヘッダー ファイルの 1 つ以上も含まれます。

-   *AnchorSyncDeviceService.h*
-   *BridgeDeviceService.h*
-   *CalendarDeviceService.h*
-   *ContactDeviceService.h*
-   *DeviceServices.h*
-   *FullEnumSyncDeviceService.h*
-   *HintsDeviceService.h*
-   *MessageDeviceService.h*
-   *MetadataDeviceService.h*
-   *NotesDeviceService.h*
-   *RingtoneDeviceService.h*
-   *StatusDeviceService.h*
-   *SyncDeviceService.h*
-   *TaskDeviceService.h*

これらのファイルの*BridgeDeviceService.h*と*DeviceService.h*がすべてのサービス アプリケーションに必要です。 他のアプリケーションには、特定のデバイスをサポートするその他のこれらのファイルの 1 つ以上を含める必要があります。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**WPD ドライバー**](wpd-drivers.md)

 

 





