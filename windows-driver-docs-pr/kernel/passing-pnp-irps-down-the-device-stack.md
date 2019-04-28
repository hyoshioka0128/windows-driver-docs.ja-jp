---
title: 下のデバイス スタックへの PnP IRP の受け渡し
description: 下のデバイス スタックへの PnP IRP の受け渡し
ms.assetid: 339ef4b4-1b4f-42ac-ab57-c53b83120f0d
keywords:
- WDK カーネルの PnP デバイス スタックを Irp を渡して、
- デバイス スタックを Irp を渡して、プラグ アンド プレイの WDK のカーネル
- WDK PnP Irp
- I/O 要求パケット PnP WDK
- デバイス スタック WDK ダウン Irp を渡す
- IoCompletion ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 647ac119a67c79f484195cff160f9c9c12f1c8d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369289"
---
# <a name="passing-pnp-irps-down-the-device-stack"></a>下のデバイス スタックへの PnP IRP の受け渡し





PnP マネージャーは、開始、停止、およびデバイスを削除するドライバーを直接を自分のデバイスのドライバーをクエリする Irp を使用します。 コードが主な機能であるすべての PnP Irp [ **IRP\_MJ\_PNP**](https://msdn.microsoft.com/library/windows/hardware/ff550772)、およびすべての PnP ドライバーが提供する必要があります、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンをこの関数のコードにサービスを提供します。 PnP マネージャーを初期化します**Irp の&gt;IoStatus.Status**ステータス\_されません\_IRP を送信するときにサポートされています。 詳細については、次を参照してください。 [DispatchPnP ルーチン](dispatchpnp-routines.md)します。

PnP マイナー Irp の一覧は、次を参照してください。[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

デバイスのすべてのドライバーには、スタック内のドライバーが IRP が失敗した場合を除き、PnP IRP に応答する機会が必要です。 (詳しくは、次の図を参照してください)。

![デバイス スタックのプラグ アンド プレイ irp を渡すことを示す図](images/passpnp.png)

PnP IRP が応答する唯一のドライバーであるデバイスの 1 つのドライバーは一切ことができます。 、たとえば、応答する関数のドライバーを検討してください、 [ **IRP\_MN\_クエリ\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff551664)要求し、に渡すことがなく、IRP が完了すると、次の下位のドライバーです。 None、下位のドライバーでサポートされている機能の一意のインスタンス ID や power など、親のバス ドライバーによってサポートされる管理機能が報告されます。

親のバス ドライバーを呼び出すと、バックアップ デバイス スタックを PnP IRP が送信されます[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343) I/O マネージャーは、いずれかと[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチンが、関数のドライバーまたはフィルター ドライバーで登録します。

PnP IRP を受信すると、関数またはフィルター ドライバーは、次を実行する必要があります。

-   場合は、ドライバーは IRP への応答アクションを実行します。
    1.  適切なアクションを実行します。
    2.  設定**Irp -&gt;IoStatus.Status**状態など、適切な状態に\_成功します。 設定**Irp -&gt;IoStatus.Information**IRP の該当する場合、します。
    3.  [次へ] スタックの場所を設定[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)または[ **IoCopyCurrentIrpStackLocationToNext**](https://msdn.microsoft.com/library/windows/hardware/ff548387)します。 設定した場合は、後者のルーチンを呼び出し、 *IoCompletion*ルーチン。
    4.  設定、 *IoCompletion*ルーチンで必要な場合。
    5.  IRP を実行しないでください。 (呼び出さない**IoCompleteRequest**)。親のバス ドライバーは IRP を完了します。
-   ドライバーでは、この IRP のアクションを実行していない場合、[次へ] のドライバーに IRP を渡す単純に準備します。
    1.  呼び出す**IoSkipCurrentIrpStackLocation** IRP からそのスタックの場所を削除します。
    2.  任意のフィールドを設定しないでください**Irp -&gt;IoStatus**します。
    3.  設定しないでください、 *IoCompletion*ルーチン。
    4.  IRP を実行しないでください。 (呼び出さない**IoCompleteRequest**)。親のバス ドライバーは IRP を完了します。

使用してドライバーを次の下位に IRP を渡す関数またはフィルター ドライバーは IRP を失敗しなかった場合[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)します。 ドライバーは、次の下位ドライバーへのポインター返されたポインター、 [ **IoAttachDeviceToDeviceStack** ](https://msdn.microsoft.com/library/windows/hardware/ff548300)以上のドライバーで呼び出す[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。

親のバス ドライバーは IRP に応答するすべてのタスクを実行した後、IRP を完了します。 バス ドライバーの呼び出し後**IoCompleteRequest**、I/O マネージャーを呼び出し、 *IoCompletion*ルーチンは、デバイスの関数またはフィルター ドライバーによって登録します。

 

 




