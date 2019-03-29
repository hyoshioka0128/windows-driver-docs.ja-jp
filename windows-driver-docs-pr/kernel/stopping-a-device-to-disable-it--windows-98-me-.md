---
title: 無効にするためのデバイスの停止 (Windows 98/Me)
description: 無効にするためのデバイスの停止 (Windows 98/Me)
ms.assetid: 2fc42fe4-ad29-4a51-9560-74b568bcd129
keywords:
- PnP デバイスを無効にします。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 082ebff5e3412fa32311522501e1d0bcebec2c65
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571327"
---
# <a name="stopping-a-device-to-disable-it-windows-98me"></a>無効にするためのデバイスの停止 (Windows 98/Me)





Windows 98 で/stop、PnP マネージャー問題 Irp デバイス マネージャーは、デバイスを無効にされた場合。 (Windows 2000 および以降のバージョンの Windows 問題[Irp の削除](removing-a-device.md)このような場合)。

PnP マネージャーでは、次の順序で停止 Irp を送信します。

1.  PnP マネージャーの問題、 [ **IRP\_MN\_クエリ\_停止\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551725)デバイスのドライバーがデバイスを停止できるかどうかを確認します。

    デバイス スタック内のすべてのドライバーが状態を返すかどうか\_成功すると、ドライバーがデバイスに (停止待ち) の状態をデバイスすばやく停止できるからです。

    PnP マネージャーは、デバイスを無効にする必要に応じて、多くのデバイス スタックを照会します。

2.  場合、 **IRP\_MN\_クエリ\_停止\_デバイス**成功すると、PnP マネージャーの問題、 [ **IRP\_MN\_の停止\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551755)デバイスを停止します。

    PnP マネージャーは、デバイスの以前のクエリ停止 IRP が正常に完了した場合にのみ停止 IRP を送信します。 IRP の停止に応答してでは、ドライバーは、(その I/O ポート) など、デバイスのハードウェア リソースを解放し、デバイスへのアクセスを必要とする任意の Irp が失敗します。

3.  場合、 **IRP\_MN\_クエリ\_停止\_デバイス**PnP マネージャー送信が失敗した、 [ **IRP\_MN\_のキャンセル\_停止\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff550826)クエリをキャンセルします。

    応答、 **IRP\_MN\_キャンセル\_停止\_デバイス**デバイスのドライバーがデバイスを開始状態に戻すし、デバイスの I/O 要求の処理を再開します。

    PnP マネージャーは、スタック内の 1 つのドライバーには、要求が失敗した場合、デバイス スタックのクエリの停止をキャンセルします。 送信 PnP マネージャーでは、1 つのデバイス スタックでクエリ停止をキャンセルしたときに、 **IRP\_MN\_キャンセル\_停止\_デバイス**ドライバー上すべてのドライバーが接続されているため、要求クエリに失敗した保留中の停止の状態で、デバイスを所有します。 ときに、 **IRP\_MN\_キャンセル\_停止\_デバイス**成功すると、ドライバーには開始状態に、デバイスが返されます。

デバイスを無効にされているそのドライバーは、デバイスが再度有効にすると、保証がないため受信 Irp をキューことはできません。 その結果、データが失われる可能性があります。

 

 




