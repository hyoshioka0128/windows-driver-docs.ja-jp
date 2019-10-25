---
title: アンロード ルーチンの環境
description: アンロード ルーチンの環境
ms.assetid: 4acf66f1-7b97-494e-9f84-14292e971542
keywords:
- アンロードルーチン WDK カーネル、環境
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17d56760466fa4ab827ff326029f14094544d246
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836094"
---
# <a name="unload-routine-environment"></a>アンロード ルーチンの環境





ドライバーが交換されるとき、またはドライバーサービスによって削除されたすべてのデバイスが削除されたときに、オペレーティングシステムによってドライバーがアンロードされます。 PnP マネージャーは、PnP ドライバーの[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンを呼び出します。これにより、ドライバーが IRP\_処理した後にデバイスオブジェクトがなくなり、 [ **\_デバイスの要求\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)されます。

アンロードシーケンスの開始時に、i/o マネージャーまたは PnP マネージャーは、ドライバーオブジェクトとそのデバイスオブジェクトを "アンロード待ち" としてマークします。 ドライバーが "アンロード待ち" としてマークされている場合、そのドライバーに追加のドライバーをアタッチしたり、ドライバーのデバイスオブジェクトに追加の参照を加えたりすることはできません。 ドライバーは未処理の Irp を完了できますが、システムはドライバーに新しい Irp を送信しません。

I/o マネージャーは、次のすべてに該当する場合にドライバーの*アンロード*ルーチンを呼び出します。

-   ドライバーによって作成されたデバイスオブジェクトには、参照が残っていません。 つまり、基になるデバイスに関連付けられているファイルを開くことはできません。また、どの Irp もドライバーのデバイスオブジェクトに対して未処理になることはありません。

-   このドライバーには他のドライバーがアタッチされていません。

-   ドライバーは、以前に登録されたすべての PnP 通知の登録を解除するために[**IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)を呼び出しました。

ドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンがエラー状態を返す場合、 *Unload*ルーチンは呼び出されないことに注意してください。 この場合、i/o マネージャーは、ドライバーによって使用されるメモリ領域を単純に解放します。

PnP マネージャーも i/o マネージャーも、システムのシャットダウン時に*アンロード*ルーチンを呼び出しません。 シャットダウン処理を実行する必要があるドライバーは、 [*DispatchShutdown*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンを登録する必要があります。

 

 




