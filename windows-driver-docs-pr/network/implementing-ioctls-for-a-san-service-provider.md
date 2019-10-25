---
title: SAN サービス プロバイダー向けの IOCTL の実装
description: SAN サービス プロバイダー向けの IOCTL の実装
ms.assetid: 7d4c7039-6b42-4620-aee5-9189b4acd030
keywords:
- プロキシドライバー WDK San、Ioctl
- SAN プロキシドライバー WDK、Ioctl
- Ioctl WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b249ccac9bca6bd758639cec82438e074281ea6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842329"
---
# <a name="implementing-ioctls-for-a-san-service-provider"></a>SAN サービス プロバイダー向けの IOCTL の実装





SAN サービスプロバイダーがプロキシドライバーに i/o 制御 (IOCTL) 要求を送信する場合、ドライバーは、これらの要求を処理するために\_ディスパッチルーチンを制御するように、 [**IRP\_MJ\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)を実装する必要があります。 IOCTL 要求は、ドライバーの Nic に割り当てられた IP アドレスの一覧を取得する要求、たとえば、メモリの割り当てや解放を要求することができます。 **Driverentry**ルーチンでは、ディスパッチルーチンのエントリポイントを指定する必要があります。

プロキシドライバーのデバイス制御ルーチンは、 [**Iogetcurrentirpstacklocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)関数を呼び出します。この関数は、ルーチンに渡された IRP へのポインターを渡します。 次に、デバイス制御ルーチンは、受信した IOCTL 要求を特定し、それに応じて要求を処理します。

現在の IOCTL 要求が完了すると、デバイス制御ルーチンは[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)関数を呼び出し、操作の状態を渡します。 この状態は、SAN サービスプロバイダーに返されます。

 

 





