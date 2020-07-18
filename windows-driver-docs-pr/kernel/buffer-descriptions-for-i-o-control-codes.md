---
title: I/O 制御コードのバッファー記述
description: I/O 制御コードのバッファー記述
ms.assetid: a458f3fb-a6c7-42ae-870e-1617a96b496f
keywords:
- I/o 制御コード WDK カーネル、バッファーの説明
- コントロールコード WDK Ioctl、バッファーの説明
- Ioctl WDK カーネル、バッファーの説明
- バッファーの説明 WDK Ioctl
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c100506b5a41c43fda17747aa8b7e3993e30435d
ms.sourcegitcommit: 701e4a41860877cc1134e139bc0bd4a9f7270443
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2020
ms.locfileid: "86453985"
---
# <a name="buffer-descriptions-for-io-control-codes"></a>I/O 制御コードのバッファー記述





I/o 制御コードは、 [**irp \_ MJ \_ デバイス \_ コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)および[**irp \_ MJ \_ 内部 \_ デバイス \_ 制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求に含まれています。 I/o マネージャーは、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) (Microsoft Windows SDK のドキュメントで説明されています) と[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)を呼び出した結果として、これらの要求を作成します。

[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)と**IoBuildDeviceIoControlRequest**は、引数として入力バッファーと出力バッファーの両方を受け入れるため、すべての**Irp \_ MJ \_ device \_ control**および**irp \_ MJ \_ 内部 \_ デバイス \_ 制御**要求は、入力バッファーと出力バッファーの両方を提供します。 システムがこれらのバッファーを記述する方法は、データ転送の種類によって異なります。 転送の種類は、IOCTL コード値を作成する[**CTL \_ コード**](defining-i-o-control-codes.md)マクロの*transfertype*値によって指定されます。

システムは、各*Transfertype*値のバッファーを次のように記述します。

<a href="" id="method-buffered"></a>メソッド \_ バッファー  
この転送の種類では、irp は、 **irp &gt;AssociatedIrp.Systembuffer**のバッファーへのポインターを提供します。 このバッファーは、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)および**IoBuildDeviceIoControlRequest**の呼び出しで指定された入力バッファーと出力バッファーの両方を表します。 ドライバーは、このバッファーの外にデータを転送します。

入力データの場合、バッファーサイズはドライバーの[**IO \_ スタックの \_ 場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)構造の**DeviceIoControl**によって指定されます。 出力データの場合、バッファーサイズはドライバーの**IO \_ スタックの \_ 場所**構造の DeviceIoControl によって指定されます **。**

システムが1つの入力/出力バッファーに割り当てる領域のサイズは、2つの長さの値のうち、大きい方になります。

<a href="" id="method-in-direct-or-method-out-direct"></a>\_ \_ Direct または method \_ OUT \_ direct のメソッド  
これらの転送の種類では、irp は、 **irp &gt;AssociatedIrp.Systembuffer**でバッファーへのポインターを提供します。 これは、 **DeviceIoControl**および**IoBuildDeviceIoControlRequest**の呼び出しで指定されるバッファーを表します。 バッファーサイズは、ドライバーの**IO \_ スタックの \_ 場所**構造の DeviceIoControl によって指定されます **。**

これらの転送の種類では、irp は、 **irp- &gt; mdladdress**の MDL へのポインターも提供します。 これは、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)および**IoBuildDeviceIoControlRequest**の呼び出しで指定されるバッファーを表します。 このバッファーは、次のように入力バッファーまたは出力バッファーとして使用できます。

-   \_DIRECT のメソッド \_ は、IRP を処理するドライバーが呼び出されたときにバッファー内のデータを受信する場合に指定されます。 MDL は入力バッファーを記述し、メソッドを \_ DIRECT に指定することで、 \_ 実行中のスレッドがバッファーに対する読み取りアクセス権を持つことを保証します。

-   Irp \_ を \_ 処理するドライバーが irp を完了する前にバッファーにデータを書き込む場合、メソッド OUT DIRECT が指定されます。 MDL は出力バッファーを記述し、メソッド OUT DIRECT を指定することで、 \_ \_ 実行中のスレッドがバッファーへの書き込みアクセス権を持つことを保証します。

これらの転送型の両方に対して、 **DeviceIoControl**は、MDL によって記述されるバッファーのサイズを指定します。

<a href="" id="method-neither"></a>メソッド ( \_ いずれも)  
I/o マネージャーでは、システムバッファーや MDLs は提供されません。 IRP は、 **DeviceIoControl**または**IoBuildDeviceIoControlRequest**に指定された入力バッファーと出力バッファーのユーザーモード仮想アドレスを、検証やマッピングを行わずに提供します。

入力バッファーのアドレスは、ドライバーの**IO \_ スタックの \_ 場所**構造で DeviceIoControl によって指定されます。出力バッファーのアドレスは、 **Type3InputBuffer**に**よって &gt; **指定されます。

バッファーサイズは、ドライバーの**IO \_ スタックの \_ 場所**の構造体で、 **DeviceIoControl**と**DeviceIoControl**の長さのパラメーターによって指定されます。

**CTL \_ コード**マクロと上記の転送の種類の詳細については、「 [I/o 制御コードの定義](defining-i-o-control-codes.md)」を参照してください。

 

 




