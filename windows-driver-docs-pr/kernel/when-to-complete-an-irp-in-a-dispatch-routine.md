---
title: ディスパッチ ルーチン内で IRP を完了するタイミング
description: ディスパッチ ルーチン内で IRP を完了するタイミング
ms.assetid: 24159535-927f-490c-9472-05ea565b7ae5
keywords:
- Irp WDK カーネル、ディスパッチルーチンを完了する
- ディスパッチルーチン WDK カーネル、Irp の完了
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 014d94c0ede2febda5559fe0a5d9739a768ee49a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838318"
---
# <a name="when-to-complete-an-irp-in-a-dispatch-routine"></a>ディスパッチ ルーチン内で IRP を完了するタイミング





通常、ドライバーは、指定された要求のパラメーターが無効であるか、またはデバイスドライバー内で、特定の**irp\_MJ\_<em>XXX</em>** がデバイス i/o 操作を必要としない限り、irp を完了しません。

階層化されたドライバーのチェーン内のすべてのドライバーは、ドライバーのディスパッチルーチンによって受信された各 IRP について、独自の i/o スタックの場所にあるパラメーターの有効性を確認できます。 最も可能性の高いドライバーのディスパッチルーチンで、無効なパラメーターを使用して Irp を完了すると、すべてのドライバーチェーンとシステム全体で i/o スループットが向上します。

上位レベルのドライバーのディスパッチルーチンは、次のガイドラインに従って、IRP を完了するか、またはそれを下位のドライバーで処理するために渡す必要があります。

-   ディスパッチルーチンによって、独自の i/o スタック位置にあるパラメーターが無効であると判断された場合は、状態\_無効\_パラメーターなど、適切なエラー状態を使用して IRP を直ちに完了する必要があります。

-   IRP に関数コード[**irp\_MJ\_CLEANUP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)が含まれている場合、 [*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、ターゲットデバイスオブジェクトに現在キューに置かれているすべての irp を、ドライバーの i/o スタックの場所で指定されたファイルオブジェクトに対して実行する必要があります。クリーンアップ IRP を完了します。

    クリーンアップ要求は、アプリケーションが終了されているか、ドライバーのデバイスオブジェクトを表すファイルオブジェクトのファイルハンドルを閉じたことを示します。 *DispatchCleanup*ルーチンからが返されると、通常、ドライバーの[*DispatchClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンが次に呼び出されます。

-   それ以外の場合、上位レベルのドライバーは、この要求を次の下位のドライバーに渡すことによってのみ、要求を満たすことができます。

最下位レベルのドライバーのディスパッチルーチンは、次のガイドラインに従って IRP を完了する必要があります。

-   ディスパッチルーチンで、独自の i/o スタック位置にあるパラメーターが無効であると判断された場合、またはドライバーが IRP をサポートしていない場合は、適切なエラー状態で IRP を直ちに完了する必要があります。 このような場合、ドライバーは状態の値が "SUCCESS\_" の IRP を完了できません。

    通常、上位レベルのドライバーは、要求された操作のパラメーターを既に確認していますが、最下位レベルのデバイスドライバーでも、独自のパラメーターチェックを実行する必要があります。

-   IRP に関数コード**irp\_MJ\_CLEANUP**が含まれている場合、 *DispatchCleanup*ルーチンは、ドライバーの i/o スタックの場所にある特定のファイルオブジェクトについて、ターゲットデバイスオブジェクトに現在キューに置かれているすべての IRP を完了する必要があります。クリーンアップ IRP を完了します。

    クリーンアップ要求は、アプリケーションが終了されているか、ドライバーのデバイスオブジェクトを表すファイルオブジェクトのファイルハンドルを閉じたことを示します。 *DispatchCleanup*ルーチンからが返されると、通常、ドライバーの*DispatchClose*ルーチンが次に呼び出されます。

-   要求にデバイス i/o 操作が必要ない場合は、ディスパッチルーチンが要求を満たし、IRP を完了する必要があります。

    たとえば、ドライバーによってデバイスの現在のモードがデバイス拡張に保存される場合があります (特に、初期化後にデバイスのモードが変更されない場合)。 その後、この格納されている情報を返すことによって、現在のデバイスモードを照会する要求を[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンが満たすことができます。

それ以外の場合は、ディスパッチルーチンが[**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出し、さらに処理するために IRP を他のドライバールーチンにキューに置いて、状態\_保留中に戻す必要があります。

 

 




