---
title: SAN サービス プロバイダー向けの IOCTL の実装
description: SAN サービス プロバイダー向けの IOCTL の実装
ms.assetid: 7d4c7039-6b42-4620-aee5-9189b4acd030
keywords:
- プロキシ ドライバー WDK San、Ioctl
- SAN プロキシ ドライバー WDK、Ioctl
- WDK の Ioctl San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d31366b182ea32304b8841981aed78a651c7d851
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374862"
---
# <a name="implementing-ioctls-for-a-san-service-provider"></a>SAN サービス プロバイダー向けの IOCTL の実装





SAN サービス プロバイダーは、I/O コントロール (IOCTL) 要求をプロキシ ドライバーに送信する場合、ドライバーを実装する必要があります、 [ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)ディスパッチこれらの要求を処理するルーチンです。 IOCTL 要求には、ドライバーの Nic に割り当てられた IP アドレスの一覧を取得する要求または割り当てやメモリを解放する要求を指定できます。 **DriverEntry**ルーチンは、ディスパッチ ルーチンのエントリ ポイントを指定する必要があります。

プロキシのドライバーのデバイス管理の日常的な呼び出し、 [ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)関数をデバイス制御ルーチンのルーチンに渡された IRP にポインターを渡します。 デバイスの制御ルーチンは、どの IOCTL 要求を受信したかを決定し、それに応じて、要求を処理します。

現在の IOCTL 要求の完了後、デバイス制御ルーチンの呼び出し、 [ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)機能し、操作の状態を渡します。 SAN サービス プロバイダーには、この状態が返されます。

 

 





