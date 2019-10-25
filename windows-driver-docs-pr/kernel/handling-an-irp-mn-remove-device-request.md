---
title: IRP_MN_REMOVE_DEVICE 要求の処理
description: IRP_MN_REMOVE_DEVICE 要求の処理
ms.assetid: 1e0c8b41-5375-41dd-80eb-e48c0f513e01
keywords:
- IRP_MN_REMOVE_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff04f4fec994c2c96e8911051c6a1da8748a1a16
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838661"
---
# <a name="handling-an-irp_mn_remove_device-request"></a>IRP\_処理して\_デバイスの要求\_削除する





PnP マネージャーは、この IRP を使用して、デバイスのソフトウェア表現 (デバイスオブジェクトなど) を削除するドライバーに指示します。 PnP マネージャは、デバイスが適切な方法で削除されたとき (たとえば、取り外しまたは取り出しハードウェアプログラムのユーザーによって開始された)、驚き (ユーザーが前の警告なしでデバイスをスロットからプルした場合)、またはユーザーが dri を更新するように要求したときに、この IRP を送信します。vers.

Windows 2000 以降のシステムでは、デバイスをデバイスマネージャー無効にした場合に、PnP マネージャーによってこの IRP が送信されます。 Windows 98/Me では、PnP マネージャーが代わりに停止 Irp を送信します。 詳細について[は、「デバイスの停止](stopping-a-device.md)」を参照してください。

PnP マネージャーは、この IRP をデバイスのドライバーに送信する前に、次のことを実行します。

-   デバイスの子 (存在する場合) に\_デバイスの要求を**削除\_、IRP\_** を送信します。

-   デバイスが削除されていることを通知するために登録されているユーザーモードコンポーネントとカーネルモードドライバーに通知します。 PnP マネージャーは、デバイスへのハンドルでターゲットデバイス通知に登録されているユーザーモードコンポーネントを呼び出し、 **Eventcomponents Targetdevicechange**に登録されているカーネルモードドライバーを呼び出します。

-   (Windows 2000 以降のシステム)ファイルシステムがデバイスにマウントされている場合、PnP マネージャーは、ファイルシステムおよびすべてのファイルシステムフィルターに削除要求を送信します。 応答として、通常、ファイルシステムはボリュームのマウントを解除します。

デバイススタック内の上位のドライバーは、remove IRP を処理し、それを次の下位のドライバーに渡します。 デバイスの親バスドライバーは、デバイスの削除操作を実行する最後のドライバーです。 ドライバーは、 [*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチン内の irp の削除を処理します。

ドライバーが正常に終了した\_場合は、デバイスのすべてのリソースが解放されていることを確認する必要があります。これにより、 **\_デバイスの要求\_削除**する必要があります。 この IRP は、ドライバーがアンロードされる前の最後の呼び出しである可能性があります。

デバイスを1つ削除すると、他の一連のデバイスを削除する必要が生じます。 PnP マネージャーは、追加のデバイスオブジェクトの最上位レベルからルートデバイスレベルへの削除を調整します。

このセクションの説明:

[関数ドライバーでのデバイスの削除](removing-a-device-in-a-function-driver.md)

[フィルタードライバーでのデバイスの削除](removing-a-device-in-a-filter-driver.md)

[バスドライバーでのデバイスの削除](removing-a-device-in-a-bus-driver.md)

 

 




