---
title: プラグ アンド プレイ マネージャー
description: プラグ アンド プレイ マネージャー
ms.assetid: b1890b3c-fc7b-4a2e-b48a-8266f237c9b6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 764aaec910426cfcd64be2d82838bc3b8e10f155
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391447"
---
# <a name="plug-and-play-manager"></a>プラグ アンド プレイ マネージャー


プラグ アンド プレイ (PnP) マネージャーでは、Windows での PnP の機能をサポートし、PnP に関連する次のタスクを担当します。

-   デバイスの検出と、システムの起動中に列挙型

-   追加またはシステムの実行中にデバイスを削除します。

カーネル モードの PnP マネージャーでは、新しいデバイスは、システムに存在し、インストールする必要があります、ユーザー モードの PnP マネージャーに通知します。

カーネル モードの PnP マネージャーも呼び出して、 [ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)と[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)デバイスのルーチンのドライバーと、を送信します。[**IRP_MN_START_DEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff551749)デバイスを開始する要求。

PnP マネージャーの維持、[デバイス ツリー](https://msdn.microsoft.com/library/windows/hardware/ff543194)は、デバイスをシステム内の追跡。 デバイスのツリーには、システム上に存在するデバイスに関する情報が含まれています。 コンピューターの起動時、PnP マネージャーはドライバーやその他のコンポーネントからの情報を使用して、このツリーを構築し、デバイスの追加または削除は、ツリーを更新します。

 

 





