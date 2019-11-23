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
ms.openlocfilehash: 084a6c5a801b94112c6891f1948cb880ef9cf381
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837171"
---
# <a name="buffer-descriptions-for-io-control-codes"></a>I/O 制御コードのバッファー記述





I/o 制御コードは、 [**irp\_MJ\_デバイス\_control**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)および[**irp\_MJ\_内部\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求に含まれています。 I/o マネージャーは、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) (Microsoft Windows SDK のドキュメントで説明されています) と[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)を呼び出した結果として、これらの要求を作成します。

[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)と**IoBuildDeviceIoControlRequest**は入力バッファーと出力バッファーの両方を引数として受け取るため、すべての**irp\_MJ\_デバイス\_control**および**irp\_MJ\_内部\_デバイス\_制御**要求が入力バッファーと出力バッファーの両方を提供します。 システムがこれらのバッファーを記述する方法は、データ転送の種類によって異なります。 転送の種類は、IOCTL コード値を作成する[**CTL の\_コード**](defining-i-o-control-codes.md)マクロの*transfertype*値によって指定されます。

システムは、各*Transfertype*値のバッファーを次のように記述します。

<a href="" id="method-buffered"></a>メソッド\_バッファーされる  
この転送の種類では、irp は、 **irp-&gt;AssociatedIrp**にあるバッファーへのポインターを提供します。 このバッファーは、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)および**IoBuildDeviceIoControlRequest**の呼び出しで指定された入力バッファーと出力バッファーの両方を表します。 ドライバーは、このバッファーの外にデータを転送します。

入力データの場合、バッファーサイズは、ドライバーの[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)の構造の**DeviceIoControl**によって指定されます。 出力データの場合、バッファーサイズは、ドライバーの**IO\_スタック\_の場所**の構造体のパラメーターによって指定され**ます。**

システムが1つの入力/出力バッファーに割り当てる領域のサイズは、2つの長さの値のうち、大きい方になります。

<a href="" id="method-in-direct-or-method-out-direct"></a>\_直接またはメソッドでのメソッド\_\_OUT\_DIRECT  
これらの転送の種類では、irp は、 **irp-&gt;AssociatedIrp**にあるバッファーへのポインターを提供します。 これは、 **DeviceIoControl**および**IoBuildDeviceIoControlRequest**の呼び出しで指定された入力バッファーを表します。 バッファーサイズは、ドライバーの**IO\_スタック\_の場所**の構造で、パラメーターによって指定されます **。**

これらの転送の種類では、irp は、 **irp-&gt;MdlAddress**にある MDL へのポインターも提供します。 これは、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)および**IoBuildDeviceIoControlRequest**の呼び出しで指定される出力バッファーを表します。 ただし、このバッファーは、次のように、実際には入力バッファーまたは出力バッファーとして使用できます。

-   IRP を処理するドライバーが、バッファーが呼び出されたときにバッファー内のデータを受信する場合は、\_DIRECT のメソッド\_が指定されます。 MDL は入力バッファーを記述し、\_DIRECT でメソッド\_を指定することにより、実行中のスレッドがバッファーに対する読み取りアクセス権を持っていることを確認します。

-   Irp を処理するドライバーが IRP を完了する前にバッファーにデータを書き込む場合は、メソッド\_OUT\_DIRECT が指定されます。 MDL は出力バッファーを記述し、メソッド\_OUT\_DIRECT を指定することで、実行中のスレッドがバッファーへの書き込みアクセス権を持っていることを保証します。

これらの転送型の両方に対して、 **DeviceIoControl**は、MDL によって記述されるバッファーのサイズを指定します。

<a href="" id="method-neither"></a>メソッド\_ません。  
I/o マネージャーでは、システムバッファーや MDLs は提供されません。 IRP は、 **DeviceIoControl**または**IoBuildDeviceIoControlRequest**に指定された入力バッファーと出力バッファーのユーザーモード仮想アドレスを、検証やマッピングを行わずに提供します。

入力バッファーのアドレスは、ドライバーの**IO\_スタック\_の場所**の構造で、 **Type3InputBuffer**によって指定されます。出力バッファーのアドレスは、 **Irp-&gt;UserBuffer**によって指定されます。

バッファーサイズは、パラメーターによって指定されます **。 DeviceIoControl の長さ**と**DeviceIoControl の長さ**は、ドライバーの**IO\_スタック\_の場所**の構造体に含まれています。

**CTL\_コード**マクロ、および上記の転送の種類の詳細については、「 [i/o 制御コードの定義](defining-i-o-control-codes.md)」を参照してください。

 

 




