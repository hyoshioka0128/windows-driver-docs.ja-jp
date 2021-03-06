---
title: ディスパッチ ルーチン内で IRP を完了するタイミング
description: ディスパッチ ルーチン内で IRP を完了するタイミング
ms.assetid: 24159535-927f-490c-9472-05ea565b7ae5
keywords:
- ルーチンをディスパッチ Irp WDK カーネルを完了すると、
- ディスパッチ ルーチンの WDK カーネル、Irp の完了
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c2f2bf62852eba46c340ea0789abbf56294ea1e
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716852"
---
# <a name="when-to-complete-an-irp-in-a-dispatch-routine"></a>ディスパッチ ルーチン内で IRP を完了するタイミング





通常、ドライバーを実行しないで Irp がディスパッチ ルーチン内で指定された要求のパラメーターが有効でない場合を除き、または、デバイスのドライバー、しない限り、特に**IRP\_MJ\_<em>XXX</em>** デバイス I/O 操作は必要ありません。

複数層のドライバーのチェーン内のすべてのドライバーは IRP がドライバーのディスパッチ ルーチンが受信した各の独自 I/O スタックの場所のパラメーターの有効性を確認できます。 最高の可能なドライバーのディスパッチ ルーチンで無効なパラメーターを持つ Irp の完了には、ドライバーのすべてのチェーンをシステムの全体的な I/O スループットが向上します。

ドライバーではより高度なディスパッチ ルーチンは、する必要があります、IRP の完了またはいずれか処理で渡す低いドライバーは、次のガイドラインに従って。

-   ディスパッチ ルーチンが、自身の I/O スタックの場所ですべてのパラメーターが無効であると判断した場合、前に、状態など、該当するエラー状態をすぐにその IRP を完了する必要があります\_無効な\_パラメーター。

-   IRP に関数コードが含まれている場合[ **IRP\_MJ\_クリーンアップ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)、 [ *DispatchCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンすべての IRP を完了する必要があります、ドライバーの I/O で指定されたファイル オブジェクトのスタックの場所とクリーンアップ IRP の完了はターゲット デバイス オブジェクトに現在キューに登録します。

    クリーンアップ要求は、アプリケーションが終了していますか、ドライバーのデバイス オブジェクトを表すファイル オブジェクトのファイル ハンドルが閉じられてことを示します。 ときに、 *DispatchCleanup*ルーチン返します、通常は、ドライバーの[ *DispatchClose* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは次に呼び出されます。

-   それ以外の場合より高度なドライバーは、次の下位ドライバーに渡すことによってのみ要求を満たすことができます。

最下位レベルのドライバーにディスパッチ ルーチンは、次のガイドラインに従って IRP を完了する必要があります。

-   ディスパッチ ルーチンは、I/O スタックの場所は、独自のパラメーターが有効でないことを決定します。 または、ドライバーは IRP をサポートしていない場合には、適切なエラー状態をすぐにその IRP を完了します。 このような場合、ドライバー完了する必要がない状態のステータス値を持つ IRP\_成功します。

    通常より高度なドライバーが既に要求された操作のパラメーターをチェックしますが、最下位レベルのデバイス ドライバーは、独自のパラメーター チェックもを実行する必要があります。

-   IRP に関数コードが含まれている場合**IRP\_MJ\_クリーンアップ**、 *DispatchCleanup*ルーチンは、すべての IRP を完了する必要がありますの対象のデバイス オブジェクトを現在キューに登録します指定したドライバーの i/o オブジェクトをファイルの場所をスタックし、IRP のクリーンアップを完了します。

    クリーンアップ要求は、アプリケーションが終了していますか、ドライバーのデバイス オブジェクトを表すファイル オブジェクトのファイル ハンドルが閉じられてことを示します。 ときに、 *DispatchCleanup*ルーチン返します、通常は、ドライバーの*DispatchClose*ルーチンは次に呼び出されます。

-   要求には、デバイスの I/O 操作は不要、ディスパッチ ルーチンでは、要求を満たすためし、IRP を完了する必要があります。

    たとえば、ドライバー保存、デバイスの現在のモード、デバイスの拡張機能で初期化後にデバイスのモードが変更頻度の低い場合に特にします。 その[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは、この格納された情報を返すことによって、現在のデバイス モードのクエリを実行する要求を満たす、でした。

ディスパッチ ルーチンを呼び出す必要がありますそれ以外の場合、 [ **IoMarkIrpPending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)、後続の処理のためには、その他のドライバー ルーチンに IRP のキューおよび状態を返す\_保留します。

 

 




