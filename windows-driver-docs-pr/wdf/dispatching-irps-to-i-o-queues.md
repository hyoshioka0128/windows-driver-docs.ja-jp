---
title: Irp の I/O キューへのディスパッチ
description: Irp の I/O キューへのディスパッチ
ms.assetid: 71872114-2A38-47FE-9D18-EF8923273811
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3cbd7dfb6cfb9238d6f1bc37c04dbe5f3f2b783
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532626"
---
# <a name="dispatching-irps-to-io-queues"></a>Irp の I/O キューへのディスパッチ


\[KMDF および UMDF に適用されます。\]

フレームワーク ベースのドライバーでは、着信 IRP のターゲット キューを動的に指定することができます。 特定のキューに IRP をディスパッチするドライバーを呼び出す必要があります、 [ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/hh451105)メソッド。

通常、ドライバーを呼び出す[ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/hh451105)いずれかからその[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)または[*EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)コールバック関数。 最適なパフォーマンスをほとんどのドライバーには、両方のコールバック関数が提供されません。

**注**  A UMDF ドライバーを指定できます、 [ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)コールバック関数が唯一の KMDF ドライバーが提供できる[ *EvtDeviceWdmIrpPreprocess*](https://msdn.microsoft.com/library/windows/hardware/ff540925)します。

 

場合は、ドライバーが既に用意されています[ *EvtDeviceWdmIrpPreprocess*](https://msdn.microsoft.com/library/windows/hardware/ff540925)、それを使用して、キューを動的に選択することができます。 そうでない場合は、提供[ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)を呼び出すと[ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/hh451105)からそのコールバック内関数。

さらに、次の注意する必要があります。

-   I/O のキューに IRP のディスパッチ用の別の方法として[既定のキューを作成する](creating-i-o-queues.md)しから、キューのハンドラー内で呼び出す[ **WdfRequestForwardToIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549958)します。 この手法は以降 KMDF 1.0 で使用できますが、適切では機能しません[進行中のキューに転送](guaranteeing-forward-progress-of-i-o-operations.md)は一般に遅くなります。 使用を検討して[ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/hh451105)代わりにします。

-   呼び出すときに[ **WdfDeviceConfigureWdmIrpDispatchCallback** ](https://msdn.microsoft.com/library/windows/hardware/hh451093)を登録する、 [ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)コールバック関数ドライバーを設定する必要があります、 *MajorFunction*次のいずれかのパラメーター。IRP\_MJ\_DEVICE\_CONTROL, IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL, IRP\_MJ\_READ, IRP\_MJ\_WRITE. この要件には適用されません[ *EvtDeviceWdmIrpPreprocess*](https://msdn.microsoft.com/library/windows/hardware/ff540925)のみ、これらの型の Irp は指定されたキューを動的にディスパッチします。

-   移動 Irp [ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)追加のスタックの場所があります。 移動 Irp [ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404) (の直前の呼び出しなし*EvtDeviceWdmIrpPreprocess*) はありません。

-   [*EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)促進はしないドライバーによって定義されたコンテキストの情報を送信する一方[ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)は。

## <a name="dispatching-non-preprocessed-irps"></a>前処理された非 Irp のディスパッチ


ドライバーから Irp をディスパッチする[ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)コールバック関数を次の手順を使用します。

1.  その[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数では、ドライバー呼び出し[ **WdfDeviceConfigureWdmIrpDispatchCallback** ](https://msdn.microsoft.com/library/windows/hardware/hh451093)に登録、 [ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)コールバック関数。

    KMDF ドライバーを呼び出す必要があります、ターゲットが、親デバイスの I/O キューの場合は、 [ **WdfPdoInitAllowForwardingRequestToParent** ](https://msdn.microsoft.com/library/windows/hardware/ff548789)を呼び出す前に[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926). KMDF ドライバーにも指定されている場合、 [ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)コールバック関数、フレームワーク関数を呼び出すそのまず IRP が到着するとします。 コールバック関数は、要求を前処理し、後に呼び出して[ **WdfDeviceWdmDispatchPreprocessedIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff546927) IRP をフレームワークに戻ります。

2.  フレームワークは、ドライバーの[ *EvtDeviceWdmIrpDispatch* ](https://msdn.microsoft.com/library/windows/hardware/hh406404)コールバック関数。
3.  内から[ *EvtDeviceWdmIrpDispatch*](https://msdn.microsoft.com/library/windows/hardware/hh406404)、呼び出すことができます、ドライバー [ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/hh451105)または[ **WdfDeviceWdmDispatchIrp**](https://msdn.microsoft.com/library/windows/hardware/hh451100)、両方ではないです。 KMDF ドライバーでは、どちらも、これらのメソッドを呼び出すことと代わりに、IRP の完了または保留中のマークの追加のオプションがあります。
4.  KMDF ドライバーが、WDF を設定した場合\_フォワード\_IRP\_TO\_IO\_キュー\_INVOKE\_INCALLERCTX\_コールバック フラグが有効になっていないことが保証処理を進行し、フレームワーク ターゲット I/O キューの呼び出し、ドライバーの[ *EvtIoInCallerContext*](https://msdn.microsoft.com/library/windows/hardware/ff541764)指定されている場合、します。 要求を前処理した後、コールバック関数する必要がありますか、再生待ちに呼び出して[ **WdfDeviceEnqueueRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff545945)呼び出して完了または[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945).

## <a name="dispatching-preprocessed-irps"></a>前処理済みの Irp のディスパッチ


ドライバーから Irp をディスパッチする[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)コールバック関数を特定の I/O キューは、次の手順を使用します。

1.  ドライバーのレジスタを[ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)コールバック関数を呼び出して[ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546043).
2.  ドライバー呼び出し[ **WdfPdoInitAllowForwardingRequestToParent** ](https://msdn.microsoft.com/library/windows/hardware/ff548789)ターゲットが、親デバイスの I/O キューの場合。
3.  [ *EvtDeviceWdmIrpPreprocess*](https://msdn.microsoft.com/library/windows/hardware/ff540925)、呼び出す[ **WdfDeviceWdmDispatchIrpToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/hh451105)で*フラグ*WDF に設定\_フォワード\_IRP\_TO\_IO\_キュー\_前処理された\_IRP します。
4.  ドライバーは WDF を設定した場合\_フォワード\_IRP\_TO\_IO\_キュー\_INVOKE\_INCALLERCTX\_コールバック フラグが有効になっていないと転送保証ターゲット I/O キューの場合、フレームワークの進行状況の呼び出し、ドライバーの[ *EvtIoInCallerContext*](https://msdn.microsoft.com/library/windows/hardware/ff541764)指定されている場合、します。 コールバック関数は、要求の前処理が完了したら後に、する必要がありますか、再生待ちに呼び出して[ **WdfDeviceEnqueueRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff545945)呼び出して完了または[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)します。

 

 





