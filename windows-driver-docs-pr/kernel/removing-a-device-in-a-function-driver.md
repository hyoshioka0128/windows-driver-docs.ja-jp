---
title: 関数ドライバーでは、デバイスを削除します。
description: 関数ドライバーでは、デバイスを削除します。
ms.assetid: 46a75647-e72a-4194-be9d-070e3ac95650
keywords:
- 機能ドライバー WDK PnP
- DispatchPnP ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e2d98736378c5535bf57e968b9cc3285e8c1943
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560702"
---
# <a name="removing-a-device-in-a-function-driver"></a>関数ドライバーでは、デバイスを削除します。





関数のドライバーがすべての操作を取り消す必要があります、デバイスを削除するときにその解析が実行を追加して、デバイスを起動します。 ここには、周辺機器の関数のドライバーとバス デバイスの機能のドライバーが含まれます。

関数のドライバーなどでは、次の手順を使用してデバイスを削除します。 その[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

1. バスのデバイスの機能のドライバーですか。

   そうである場合は、バス上のデバイスのすべての未処理の子 Pdo を削除可能性があります。

   前に、バス ドライバーが処理される場合は[ **IRP\_MN\_突然\_削除**](https://msdn.microsoft.com/library/windows/hardware/ff551760)子デバイスがドライバーの要求がまだ受信していません、それ以降[ **IRP\_MN\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738)要求、バス ドライバーは、子の PDO をそのまま残ります。 子デバイスに対してすべてのハンドルを閉じるときに、後で、PnP マネージャーは、子デバイスの削除 IRP を送信し、バス ドライバーは、その時点で子 PDO を削除します。

   前に、バス ドライバーが処理される場合は**IRP\_MN\_削除\_デバイス**、デバイスの要求し、後続いいえが**IRP\_MN\_突然\_削除**バス ドライバーは、PDO の子を削除し、要求。 この場合、PnP マネージャーにより、すべての関数とフィルター ドライバーを子デバイスから削除されていること (DOs FDO とフィルターされて削除) 削除 IRP を親のバスのデバイスに送信する前にします。 子 PDO バス デバイスを削除する前に、バス ドライバーは子 PDO を削除する必要がありますので可能性が存在する場合は、あります。

2. ドライバーが既に処理前**IRP\_MN\_突然\_削除**この FDO の要求ですか?

   場合は、残りのクリーンアップを実行し、手順 8. に進みます[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)します。

   通常、ドライバーは、ドライバーが処理されるかどうかを示すデバイス拡張機能のフラグ、 **IRP\_MN\_突然\_削除**デバイスの要求。

3. ドライバーは以前、ウェイク アップについては、デバイスが有効になっている、キャンセル、 [ **IRP\_MN\_待機\_WAKE** ](https://msdn.microsoft.com/library/windows/hardware/ff551766)要求。

4. デバイスがアクティブであることを確認します。

   かどうか、デバイスは既に以前への応答で非アクティブな**IRP\_MN\_クエリ\_削除\_デバイス**ドライバーは新しい要求を受け入れないようにデバイスをマークする必要があり、完了する必要がありますこのドライバーですべての要求がキューに登録します。 ドライバーには、デバイスへのアクセスを必要とする未処理の要求が失敗する必要があります。

   ドライバーを使用できる、 **Io*Xxx*RemoveLock * Xxx*** 未処理の I/O をカウントし、その削除処理を示すイベントを設定するルーチンを続行できます。

5. 電源オフ操作を実行します。

   各デバイス ドライバーの受信したときに存在する場合、電源オフ操作を実行します、 **IRP\_MN\_削除\_デバイス**要求。 関数ドライバー、通常、デバイスの電源ポリシーの所有者が、個別に送信しません[ **IRP\_MN\_設定\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)デバイスの電源を設定する要求D3 状態です。 親のバス ドライバーは、通常、スロットを補強しで電源マネージャーに通知[ **PoSetPowerState** ](https://msdn.microsoft.com/library/windows/hardware/ff559765)バス ドライバーが IRP の削除を取得します。 詳細については、[電源管理](implementing-power-management.md)を参照してください。

6. 呼び出すことによって、デバイス インターフェイスを無効にする[ **IoSetDeviceInterfaceState**](https://msdn.microsoft.com/library/windows/hardware/ff549700)します。

7. ドライバーによって使用中のデバイスのハードウェア リソースを解放します。

   正確な操作は、デバイスとドライバーによって異なりますが、切断割り込みを含めることができます[ **IoDisconnectInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff549089)、物理アドレス範囲を解放[ **MmUnmapIoSpace**](https://msdn.microsoft.com/library/windows/hardware/ff556387)、I/O ポートを解放します。

8. 渡す、 **IRP\_MN\_削除\_デバイス**次のドライバーに要求します。

   IRP スタックの場所で [次へ] の下位のドライバーのセットアップ[ **IoSkipCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff550355)で次のドライバーに IRP を渡すと[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336).

   ドライバーは、基になるドライバーの削除活動を続行する前に、削除操作を完了するまで待機する必要はありません。

9. デバイス オブジェクトを使用してデバイス スタックから削除[ **IoDetachDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549087)します。

   [次へ] の低いデバイス オブジェクトとしてへのポインターを指定、*台*パラメーター。 ドライバーでは、このようなポインターを受け取るへの呼び出しから[ **IoAttachDeviceToDeviceStack** ](https://msdn.microsoft.com/library/windows/hardware/ff548300)ドライバーの[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。

10. 任意のデバイスに固有の割り当て、メモリ、イベント、およびなどをクリーンアップします。

11. 無料で FDO [ **IoDeleteDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549083)します。

12. 戻り値、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)から戻り値の状態を伝達するルーチン**保留**します。

関数のドライバーが指定されていない、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) IRP、完了ルーチンの IRP では、削除もできません。 Irp の削除は、親のバス ドライバーを実施します。

 

 




