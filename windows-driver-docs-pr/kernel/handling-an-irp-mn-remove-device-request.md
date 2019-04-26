---
title: IRP_MN_REMOVE_DEVICE 要求の処理
description: IRP_MN_REMOVE_DEVICE 要求の処理
ms.assetid: 1e0c8b41-5375-41dd-80eb-e48c0f513e01
keywords:
- IRP_MN_REMOVE_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14ce4f40df7c67f63add6af8b88b7ef11b15c02f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359813"
---
# <a name="handling-an-irpmnremovedevice-request"></a>IRP の処理\_MN\_削除\_デバイス要求





PnP マネージャーでは、この IRP を使用して、デバイスのソフトウェアの表現 (デバイス オブジェクト、およびなど) を削除するドライバーに指示します。 驚いたことに (ユーザーは、以前の警告なしには、そのスロットから、デバイスを取得) でデバイスが (たとえば、取り外しますプログラム内のユーザーによって開始された)、通常の方法で削除されたときに、または dri を更新するユーザーが要求したときに、PnP マネージャーがこの IRP を送信しますバージョン。

Windows 2000 およびそれ以降のシステムでは、PnP マネージャーは、デバイス マネージャーは、デバイスを無効にされた場合に、この IRP を送信します。 Windows 98 で PnP マネージャーとは、送信/Irp を代わりに停止します。 参照してください[デバイスを停止する](stopping-a-device.md)詳細についてはします。

PnP マネージャーは、デバイスのドライバーをこの IRP を送信する前に、次を行います。

-   送信**IRP\_MN\_削除\_デバイス**存在する場合、デバイスの子を要求します。

-   任意のユーザー モード コンポーネントと、デバイスが削除されることを通知に登録するカーネル モード ドライバーに通知します。 PnP マネージャーは、デバイスを識別するハンドルでターゲット デバイスの通知に登録されているすべてのユーザー モード コンポーネントを呼び出すし、カーネル モード ドライバー用に登録を呼び出す**EventCategoryTargetDeviceChange**します。

-   (Windows 2000 以降のシステムで)デバイスのファイル システムをマウントすると、PnP マネージャーはファイル システムとファイル システム フィルターを削除要求を送信します。 応答して、ファイル システムでは、ボリュームが通常マウント解除します。

デバイス スタックの最上位のドライバーは IRP の削除 を処理し、次へ の下位のドライバーに渡します。 デバイスの親のバス ドライバーは、そのデバイスの削除操作を実行する最後のドライバーです。 ドライバーのハンドルの Irp の削除、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

ドライバーの成功を返す前に、 **IRP\_MN\_削除\_デバイス**要求、デバイスのすべてのリソースがリリースされたことを確認する必要があります。 ドライバーが読み込まれる前に、この IRP では最後に呼び出した可能性があります。

1 つのデバイスを削除すると、一連の他のデバイスを削除する必要を作成できます。 PnP マネージャーでは、デバイスのルート レベルに至るまでの最上位レベルから追加のデバイス オブジェクトの削除を調整します。

このセクションについて説明します。

[関数ドライバーでは、デバイスを削除します。](removing-a-device-in-a-function-driver.md)

[フィルター ドライバーでは、デバイスを削除します。](removing-a-device-in-a-filter-driver.md)

[バス ドライバーでは、デバイスを削除します。](removing-a-device-in-a-bus-driver.md)

 

 




