---
title: BRB の構築と送信
description: BRB の構築と送信
ms.assetid: 53a692e7-9c71-4dca-9331-32ac97b94179
keywords:
- Bluetooth の WDK、Bluetooth のブロックを要求します。
- BRBs WDK
- Bluetooth の WDK、要求のブロック
- BRBs を送信します。
- WDK の Bluetooth の値を返す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03c883b19f878fd37a636282eb1d512eb98c3972
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350183"
---
# <a name="building-and-sending-a-brb"></a>BRB の構築と送信


次の手順では、ビルドし、Bluetooth 要求ブロック (BRB) を送信するプロファイルのドライバーが次の一般的なプロセスについて説明します。 BRB は、実行する Bluetooth 操作を記述したデータのブロックです。

### <a name="span-idtobuildandsendabrbspanspan-idtobuildandsendabrbspanto-build-and-send-a-brb"></a><span id="to_build_and_send_a_brb"></span><span id="TO_BUILD_AND_SEND_A_BRB"></span>構築し、BRB の送信

1.  IRP を割り当てます。 Irp を使用する方法の詳細については、次を参照してください。 [Irp の処理](https://msdn.microsoft.com/library/windows/hardware/ff546847)します。

2.  BRB を割り当てます。 BRBs を割り当てるには、呼び出し、 [ **BthAllocateBrb** ](https://msdn.microsoft.com/library/windows/hardware/ff536634)プロファイル ドライバーで使用するため、Bluetooth ドライバー スタックをエクスポートする関数。 ポインターを取得する、 *BthAllocateBrb*関数を参照してください[Bluetooth インターフェイスの照会](querying-for-bluetooth-interfaces.md)します。

3.  BRB のパラメーターを初期化します。 各 BRB では、対応する構造体を使用します。 使用目的に従って構造体のメンバーを設定します。 BRBs と、対応する構造の一覧については、次を参照してください。 [Bluetooth ドライバー スタックを使用して](using-the-bluetooth-driver-stack.md)します。

4.  IRP のパラメーターを初期化します。 設定、 **MajorFunction** IRP に IRP のメンバー\_MJ\_内部\_デバイス\_コントロール。 設定、 **Parameters.DeviceIoControl.IoControlCode** IOCTL メンバー\_内部\_両方\_送信\_BRB します。 設定、 **Parameters.Others.Argument1** BRB をポイントするメンバー。

5.  IRP がドライバー スタック ダウンを渡します。 呼び出す[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) IRP を次の下位ドライバーに送信します。

次の擬似コードの例では、Bluetooth ドライバー スタックの処理に L2CAP Ping BRB を設定する方法を示します。

**注**  読みやすくするために、次の擬似コードの例では示しませんエラー処理します。

 

```cpp
#include <bthddi.h>

// Code for obtaining the BthInterface pointer

// Define a custom pool tag to identify your profile driver's dynamic memory allocations.
// You should change this tag to easily identify your driver's allocations from other drivers.
#define PROFILE_DRIVER_POOL_TAG '_htB'

PIRP Irp;
Irp = IoAllocateIrp( DeviceExtension->ParentDeviceObject->StackSize, FALSE );

PBRB_L2CA_PING BrbPing; // Define storage for a L2CAP Ping BRB

// Allocate the Ping BRB
BrbPing = BthInterface->BthAllocateBrb( BRB_L2CA_PING, PROFILE_DRIVER_POOL_TAG );

// Set up the next IRP stack location
PIO_STACK_LOCATION NextIrpStack;
NextIrpStack = IoGetNextIrpStackLocation( Irp );
NextIrpStack->MajorFunction = IRP_MJ_INTERNAL_DEVICE_CONTROL;
NextIrpStack->Parameters.DeviceIoControl.IoControlCode = IOCTL_INTERNAL_BTH_SUBMIT_BRB;
NextIrpStack->Parameters.Others.Argument1 = BrbPing;

// Pass the IRP down the driver stack
NTSTATUS Status;
Status = IoCallDriver( DeviceExtension->NextLowerDriver, Irp );
```

 

 





