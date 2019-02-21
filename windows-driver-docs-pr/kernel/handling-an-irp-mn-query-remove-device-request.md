---
title: IRP_MN_QUERY_REMOVE_DEVICE 要求の処理
description: IRP_MN_QUERY_REMOVE_DEVICE 要求の処理
ms.assetid: 30177e51-5312-4a24-972e-0c1c2d183d18
keywords:
- IRP_MN_QUERY_REMOVE_DEVICE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a34dcd72d4c683f819630b16bf211f4d947915d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550342"
---
# <a name="handling-an-irpmnqueryremovedevice-request"></a>IRP の処理\_MN\_クエリ\_削除\_デバイス要求





PnP マネージャーでは、デバイスは、コンピューターから削除されると、マシンを停止することがなく、デバイスを削除できるかどうかを確認することをドライバーに通知するためには、この IRP を送信します。 ユーザーがデバイスのドライバーの更新を要求すると、この IRP も送信します。

PnP マネージャーでは、この IRP を送信 IRQL パッシブで\_システム スレッドのコンテキスト内のレベル。

デバイスのドライバーをこの IRP を送信する前に、次が行われます。

-   デバイス (または関連するデバイス) で通知に登録されているすべてのユーザー モード アプリケーションに通知します。

    これには、デバイスの子孫 (子デバイス、子、およびその他の子) のいずれかで、デバイスまたはデバイスの取り外し関係の 1 つの通知に登録するアプリケーションが含まれます。 アプリケーションを呼び出すことによってこのような通知の登録**RegisterDeviceNotification**します。

    この通知への応答、アプリケーションはデバイスの削除 (デバイスに閉じますハンドル) を準備するか、またはクエリが失敗しました。

-   デバイス (または関連するデバイス) で通知に登録されているすべてのカーネル モード ドライバーに通知します。

    これには、デバイスの子孫のいずれかで、デバイスまたはデバイスの取り外し関係の 1 つの通知に登録されているドライバーが含まれます。 ドライバーでは、呼び出すことによってこの通知を登録します。 [ **IoRegisterPlugPlayNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff549526)のイベント カテゴリに**EventCategoryTargetDeviceChange**します。

    この通知への応答、ドライバーはデバイスの削除 (デバイスに閉じますハンドル) を準備するか、またはクエリが失敗しました。

-   送信[ **IRP\_MN\_クエリ\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551705) Irp をデバイスの子孫のドライバーにします。

-   (Windows 2000 およびそれ以降のシステム)デバイスのファイル システムをマウントすると、PnP マネージャーはファイル システムとファイル システム フィルターにクエリの削除要求を送信します。 デバイスに開いているハンドルがある場合は、ファイル システムでは通常、クエリの削除要求が失敗します。 通常、ファイル システムをロックそうでない場合の次の位置から未来を防ぐためにボリュームを作成します。 マウントされたファイル システムがクエリの削除要求をサポートしていない場合、PnP マネージャー デバイスのクエリの削除要求は失敗します。

PnP マネージャーが送信すべて上記の手順の成功した場合、 **IRP\_MN\_クエリ\_削除\_デバイス**デバイスのドライバーにします。

**IRP\_MN\_クエリ\_削除\_デバイス**デバイス スタックの最上位のドライバーによって、各 [次へ] の下のドライバーでし、要求が最初に処理します。 ドライバーのハンドルの Irp の削除、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

応答、 **IRP\_MN\_クエリ\_削除\_デバイス**ドライバーは、次を実行する必要があります。

1.  操作を中断せず、マシンからデバイスを削除できるかどうかを決定します。

    次のいずれかに該当する場合、ドライバーはクエリ削除 IRP に失敗する必要があります。

    -   場合は、デバイスを削除するデータを失うことになる可能性があります。

    -   場合は、コンポーネントには、デバイスへの開いているハンドルがあります。 (これは、Windows 98 上の問題/ユーザーのみです。 開いているハンドルを追跡し、後に開いているハンドルがある場合、クエリは失敗し、Windows 2000 以降のバージョンの Windows、 **IRP\_MN\_クエリ\_削除\_デバイス**が完了するとします)。

    -   ドライバーの通知を受け取る場合 (を通じて、 [ **IRP\_MN\_デバイス\_使用状況\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff550841) IRP) デバイスが、ページングのパスにあります。クラッシュ ダンプ、または休止状態ファイル。

    -   場合は、ドライバーでは、デバイスに対する未処理インターフェイス参照があります。 ドライバーは、インターフェイスへの応答で提供されている場合、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff551687)要求とインターフェイスがない逆参照されています。

2.  デバイスを削除できない場合は、IRP がクエリの削除に失敗します。

    設定**Irp -&gt;IoStatus.Status**は適切なエラー状態を (通常の状態\_失敗)、呼び出す[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)でIO\_いいえ\_ドライバーからの戻り値のインクリメントと*DispatchPnP*ルーチン。 [次へ] の下のドライバーに IRP を渡さないでください。

3.  ドライバーが以前に送信された場合、 [ **IRP\_MN\_待機\_WAKE** ](https://msdn.microsoft.com/library/windows/hardware/ff551766)待機ウェイク IRP をキャンセルするウェイク アップについては、デバイスを有効にする要求。

4.  デバイスの以前の PnP 状態を記録します。

    ドライバーはドライバーが受信したときに、デバイスが含まれる PnP の状態を記録する必要があります、 [ **IRP\_MN\_クエリ\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551705)要求ドライバーは、クエリが取り消された場合に、その状態のデバイスを返す必要がありますので ([**IRP\_MN\_キャンセル\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff550823)). 以前の状態が通常は「開始」、ドライバーが正常に完了したときに、デバイスが入力した状態である、 [ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)要求。

    ただし、他の以前の状態は、考えられるです。 たとえば、ユーザー デバイス マネージャーを介してデバイスを無効が可能性があります。 またはへの応答、 **IRP\_MN\_クエリ\_機能**要求と、親のバス ドライバー (またはフィルター ドライバー、バス ドライバーに) 可能性がありますが報告されるデバイスのハードウェアが無効になっています。 いずれの場合も、無効になっているデバイスのドライバーが表示されることができます、 **IRP\_MN\_クエリ\_削除\_デバイス**要求を受信する前に、 **IRP\_MN\_開始\_デバイス**要求。

5.  IRP を終了します。

    関数またはフィルター ドライバーでは。

    -   設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。

    -   [次へ] スタックの場所を設定[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)で [次へ] の下位のドライバーに IRP を渡すと[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336).

    -   状態を反映**保留**から戻り値の状態として、 *DispatchPnP*ルーチン。

    -   IRP を実行しないでください。

    バス ドライバー。

    -   設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。

    -   IRP の完了 ([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)) IO と\_いいえ\_インクリメントします。

    -   戻り値、 *DispatchPnP*ルーチン。

デバイス スタック内の任意のドライバーが失敗した場合、 **IRP\_MN\_クエリ\_削除\_デバイス**、PnP マネージャーに送信する**IRP\_MN\_キャンセル\_削除\_デバイス**デバイス スタックにします。 これにより、ドライバーを必要とする、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)下位のドライバーが IRP を失敗するかどうかを検出するためにクエリの削除 IRP のルーチンです。

ドライバーが完了すると、 **IRP\_MN\_クエリ\_削除\_デバイス**削除保留中状態にあるデバイスと見なされる場合、ドライバーが、それ以降の作成に失敗する必要がありますデバイスの要求数。 ドライバーが処理の他のすべての Irp 通常どおり、ドライバーが受信されるまで、 **IRP\_MN\_キャンセル\_削除\_デバイス**または**IRP\_MN\_削除\_デバイス**します。

 

 




