---
title: プラグ アンド プレイ マネージャー
description: プラグ アンド プレイ マネージャー
ms.assetid: b1890b3c-fc7b-4a2e-b48a-8266f237c9b6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94c08fb3952610b2363e22f4c5ef65497339fd90
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360834"
---
# <a name="plug-and-play-manager"></a>プラグ アンド プレイ マネージャー


プラグ アンド プレイ (PnP) マネージャーでは、Windows での PnP の機能をサポートし、PnP に関連する次のタスクを担当します。

-   デバイスの検出と、システムの起動中に列挙型

-   追加またはシステムの実行中にデバイスを削除します。

カーネル モードの PnP マネージャーでは、新しいデバイスは、システムに存在し、インストールする必要があります、ユーザー モードの PnP マネージャーに通知します。

カーネル モードの PnP マネージャーも呼び出して、 [ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)と[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)デバイスのルーチンのドライバーと、を送信します。[**IRP_MN_START_DEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)デバイスを開始する要求。

PnP マネージャーの維持、[デバイス ツリー](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)は、デバイスをシステム内の追跡。 デバイスのツリーには、システム上に存在するデバイスに関する情報が含まれています。 コンピューターの起動時、PnP マネージャーはドライバーやその他のコンポーネントからの情報を使用して、このツリーを構築し、デバイスの追加または削除は、ツリーを更新します。

 

 





