---
title: BRB の構築と送信
description: BRB の構築と送信
ms.assetid: 53a692e7-9c71-4dca-9331-32ac97b94179
keywords:
- Bluetooth WDK、Bluetooth 要求ブロック
- BRBs WDK
- Bluetooth WDK、要求ブロック
- 送信 (BRBs を)
- 戻り値 WDK Bluetooth
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8adcba3e4028c18947d84eb7f586906493164da6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833873"
---
# <a name="building-and-sending-a-brb"></a>BRB の構築と送信


次の手順は、プロファイルドライバーが Bluetooth 要求ブロック (BRB) をビルドして送信するための一般的なプロセスの概要を示しています。 BRB は、実行する Bluetooth 操作を記述するデータのブロックです。

### <a name="span-idto_build_and_send_a_brbspanspan-idto_build_and_send_a_brbspanto-build-and-send-a-brb"></a><span id="to_build_and_send_a_brb"></span><span id="TO_BUILD_AND_SEND_A_BRB"></span>BRB をビルドして送信するには

1.  IRP を割り当てます。 Irp の使用方法の詳細については、「 [irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)」を参照してください。

2.  BRB を割り当てます。 BRBs を割り当てるには、デバイスドライバーによって使用されるように、Bluetooth ドライバースタックによってエクスポートされる[**Bthallocatebrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/nc-bthddi-pfnbth_allocate_brb)関数を呼び出します。 *Bthallocatebrb*関数へのポインターを取得するには、「 [Bluetooth インターフェイスのクエリ](querying-for-bluetooth-interfaces.md)」を参照してください。

3.  BRB のパラメーターを初期化します。 各 BRB は、対応する構造体を使用します。 使用目的に応じて構造体のメンバーを設定します。 BRBs とそれに対応する構造体の一覧については[、「Bluetooth ドライバースタックの使用](using-the-bluetooth-driver-stack.md)」を参照してください。

4.  IRP のパラメーターを初期化します。 IRP の**MajorFunction**メンバーを IRP\_MJ\_内部\_デバイス\_コントロールに設定します。 \_内部\_BTH\_SUBMIT\_BRB に渡すように、 **DeviceIoControl のコード**メンバーを IOCTL に設定します。 BRB を指すように**引数 1**メンバーを設定します。

5.  IRP をドライバースタックに渡します。 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、IRP を次の下位のドライバーに送信します。

次の擬似コード例は、Bluetooth ドライバースタックが処理するように L2CAP Ping BRB を設定する方法を示しています。

**メモ**  読みやすくするために、次の擬似コード例ではエラー処理を示していません。

 

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

 

 





