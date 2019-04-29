---
title: DispatchPower ルーチン
description: DispatchPower ルーチン
ms.assetid: e385064f-cbdb-432f-951a-743217891333
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchPower ルーチン
- DispatchPower ルーチン
- 電源管理の WDK カーネル、ディスパッチ ルーチン
- 対し、IRP_MJ_POWER I/O 関数のコード
- リムーバブル デバイスの電源ディスパッチ ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05fbae0b57a6fd6edf3bd86605306f78a956658f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387215"
---
# <a name="dispatchpower-routines"></a>DispatchPower ルーチン





ドライバーの[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)日常的なサポート[電源管理](implementing-power-management.md)の Irp を処理することによって、 [ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784) I/O 関数のコード。 関連付けられている、 **IRP\_MJ\_POWER**関数コードが電源管理の小さな I/O 関数コードをいくつか。 電源マネージャーを待機し、ウェイク アップのシステム イベントを自分のデバイスのドライバーをクエリするのに応答の電源状態を変更するのにドライバーに出力するため、これらのマイナー関数コードを使用します。

各ドライバーの*DispatchPower*ルーチンは、次のタスクを実行します。

-   可能であれば、IRP を処理します。

-   デバイスで [次へ] の下位のドライバーに IRP を渡すを使用して、スタック[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)します。

-   場合は、バス ドライバーをデバイスで要求された電源操作を実行し、IRP の完了します。

デバイスのすべてのドライバーには、いくつかの場合、関数またはフィルター ドライバーの IRP の失敗が許可される場所を除く、デバイスの電源 Irp を処理する必要があります。 ほとんどの関数とフィルター ドライバーがいくつかの処理を実行したり設定や、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)の IRP では、各電源ルーチンが完了する前に、[次へ] の下位のドライバーに IRP を渡します。 最終的に IRP では、バス ドライバーは、物理的に必要な場合は、デバイスの電源状態を変更し、IRP の完了に到達します。

I/O マネージャーが、いずれかで呼び出す IRP が完了したら、 *IoCompletion*ルーチン IRP を結ぶデバイス スタックと、ドライバーによって設定します。 ドライバーは、完了ルーチンを設定する必要があるかどうかは IRP とドライバーの個別の要件の種類によって異なります。

電源の Irp こと、デバイスの電源を入れます処理する必要が最初にデバイス スタック (基になるバス ドライバー) の最下位のドライバーをし、スタックに連続する各ドライバーでします。 電源 Irp が、デバイスの電源を処理する必要が最初にデバイス スタックの上部にあるドライバーをし、スタックを下方向に連続する各ドライバーでします。

### <a name="special-handling-for-removable-devices"></a>リムーバブル デバイス用の特別な処理

*DispatchPower*ルーチン、リムーバブル デバイスのドライバーは、デバイスがまだ存在するかどうかを確認する必要があります。 デバイスが削除された場合、ドライバーが IRP が [次へ] の下のドライバーを渡さないでください。 代わりに、ドライバーは、次の操作にする必要があります。

-   呼び出す[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)のべ IRP の処理を開始します。

-   設定**Irp -&gt;IoStatus.Status**ステータス\_削除\_保留します。

-   呼び出す[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)、IO を指定する\_いいえ\_IRP の完了をインクリメントします。

-   状態を返す\_削除\_保留します。

 

 




