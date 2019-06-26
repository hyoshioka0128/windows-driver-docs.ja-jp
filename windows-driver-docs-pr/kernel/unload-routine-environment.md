---
title: アンロード ルーチンの環境
description: アンロード ルーチンの環境
ms.assetid: 4acf66f1-7b97-494e-9f84-14292e971542
keywords:
- アンロード ルーチン WDK カーネル、環境
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb61fb9e1920cf753adef3a345bf26161e5c1f36
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382938"
---
# <a name="unload-routine-environment"></a>アンロード ルーチンの環境





オペレーティング システム、ドライバーが置き換えられるとき、またはドライバーがアンロードされるすべてのデバイス ドライバー サービスが削除されていること。 PnP マネージャーを呼び出す、PnP ドライバーの[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)ルーチンの場合は、ドライバーがあるない複数のデバイス オブジェクトを処理した後、 [ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)要求。

アンロードのシーケンスの先頭には、I/O マネージャーまたはマネージャーの PnP ドライバー オブジェクトとそのデバイス オブジェクトとしてマーク「アンロードは保留中」します。 ドライバーは、「アンロードは保留中」としてマークされたが後、は、ドライバーには、追加のドライバーが接続することはありませんもことができます、追加の参照は、ドライバーのデバイス オブジェクトを作成します。 ドライバーは未解決の Irp を入力できますが、システムは、ドライバーをすべて新しい Irp を送信しません。

I/O マネージャーには、ドライバーの*アンロード*ルーチンに次のすべてに該当する場合。

-   ドライバーが作成したデバイス オブジェクトのいずれかに参照が残っていません。 つまり、開放できる基になるデバイスに関連付けられているファイルはありません。 またことができます、Irp がドライバーのデバイス オブジェクトのいずれかの未処理。

-   その他のドライバーはこのドライバーに接続されている残っていません。

-   ドライバーが呼び出されて[ **IoUnregisterPlugPlayNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iounregisterplugplaynotification)を登録されているすべての PnP 通知の登録を解除します。

なお、*アンロード*ルーチンは、ドライバーの場合は呼び出されません[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンがエラー状態を返します。 この場合、I/O マネージャーでは、単に、ドライバーによって使用されるメモリ領域を解放します。

PnP マネージャーでも I/O マネージャーを呼び出す*アンロード*システム シャット ダウン時にルーチン。 シャット ダウン処理を実行する必要があるドライバーを登録する必要があります、 [ *DispatchShutdown* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

 

 




