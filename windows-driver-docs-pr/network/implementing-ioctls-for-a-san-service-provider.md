---
title: SAN サービス プロバイダーの Ioctl を実装します。
description: SAN サービス プロバイダーの Ioctl を実装します。
ms.assetid: 7d4c7039-6b42-4620-aee5-9189b4acd030
keywords:
- プロキシ ドライバー WDK San、Ioctl
- SAN プロキシ ドライバー WDK、Ioctl
- WDK の Ioctl San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a831bf17ff3870e44bf7f43bdfb368c854f3260a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553929"
---
# <a name="implementing-ioctls-for-a-san-service-provider"></a>SAN サービス プロバイダーの Ioctl を実装します。





SAN サービス プロバイダーは、I/O コントロール (IOCTL) 要求をプロキシ ドライバーに送信する場合、ドライバーを実装する必要があります、 [ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)ディスパッチこれらの要求を処理するルーチンです。 IOCTL 要求には、ドライバーの Nic に割り当てられた IP アドレスの一覧を取得する要求または割り当てやメモリを解放する要求を指定できます。 **DriverEntry**ルーチンは、ディスパッチ ルーチンのエントリ ポイントを指定する必要があります。

プロキシのドライバーのデバイス管理の日常的な呼び出し、 [ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)関数をデバイス制御ルーチンのルーチンに渡された IRP にポインターを渡します。 デバイスの制御ルーチンは、どの IOCTL 要求を受信したかを決定し、それに応じて、要求を処理します。

現在の IOCTL 要求の完了後、デバイス制御ルーチンの呼び出し、 [ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)機能し、操作の状態を渡します。 SAN サービス プロバイダーには、この状態が返されます。

 

 





