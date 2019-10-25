---
title: デバイス キューのセットアップと使用
description: デバイス キューのセットアップと使用
ms.assetid: 5221ffc0-0cb4-498b-9be2-4d240b5f2744
keywords:
- デバイスが WDK Irp をキューに入れ、セットアップ
- デバイスキュー WDK Irp、オブジェクト
- キューへの Irp の挿入
- デバイスキューオブジェクトの格納
- 補足の IRP キュー WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b8aa7149e95107ad6308c3ee434774580416540
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838428"
---
# <a name="setting-up-and-using-device-queues"></a>デバイス キューのセットアップと使用





ドライバーは、ドライバーまたはデバイスの初期化で[**Keinitializedevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedevicequeue)を呼び出すことによって、デバイスキューオブジェクトを設定します。 デバイスを起動した後、ドライバーは[**Keinsertdevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertdevicequeue)または[**Keinsertbykeydevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertbykeydevicequeue)を呼び出して、irp をこのキューに挿入します。 次の図は、これらの呼び出しを示しています。

![デバイスキューの設定と使用](images/3devqobj.png)

この図に示すように、ドライバーはデバイスキューオブジェクトの記憶域を提供する必要があります。このオブジェクトは常駐している必要があります。 通常、デバイスキューオブジェクトを設定するドライバーは、ドライバーによって作成されたデバイスオブジェクトの[デバイス拡張機能](device-extensions.md)に必要な記憶域を提供しますが、ドライバーが[コントローラーオブジェクト](using-controller-objects.md)または非ページプールで使用する場合は、記憶域をコントローラー拡張機能に含めることができます。ドライバーによって割り当てられます。

ドライバーがデバイス拡張機能のデバイスキューオブジェクトの記憶域を提供する場合、デバイスオブジェクトを作成した後、デバイスを起動する前に**Keinitializedevicequeue**を呼び出します。 つまり、ドライバーは、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンからキューを初期化するか、PnP IRP\_処理するときに、 [ **\_デバイス要求を開始\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)ことができます。 **Keinitializedevicequeue**への呼び出しでは、ドライバーはデバイスキューオブジェクト用に提供するストレージへのポインターを渡します。

デバイスを起動した後、ドライバーは**Keinsertdevicequeue**を呼び出して irp をデバイスキューに挿入できます。これにより、irp がキューの末尾に配置されるか、 **Keinsertbykeydevicequeue**によって irp がキューに格納されます。前の図に示すように、ドライバーによって決定された*SortKey*の値。

これらの各サポートルーチンは、IRP がキューに挿入されたかどうかを示すブール値を返します。 また、キューが現在空 (ビジー状態ではない) の場合は、これらの呼び出しによってデバイスキューオブジェクトの状態が Busy に設定されます。 ただし、キューが空 (ビジー状態ではない) の場合、 **Keinsert*Xxx*devicequeue**ルーチンでは、IRP がキューに挿入されません。 代わりに、デバイスキューオブジェクトの状態を Busy に設定し、 **FALSE**を返します。 IRP がキューに登録されていないため、ドライバーは、後続の処理のために別のドライバールーチンに渡す必要があります。

**補足デバイスキューを設定するときは、次の実装ガイドラインに従ってください。**

**Keinsert*Xxx*devicequeue**への呼び出しで**FALSE**が返された場合、呼び出し元は、キューに入れようとした IRP を別のドライバールーチンに渡す必要があります。
ただし、 **Keinsert*Xxx*devicequeue**を呼び出すと、デバイスキューオブジェクトの状態が "ビジー" に変更されます。そのため、ドライバーが最初に**keremove*xxx*devicequeue**を呼び出さない限り、次の IRP がキューに挿入されます。

デバイスキューオブジェクトの状態が "ビジー" に設定されている場合、ドライバーは、次のいずれかのサポートルーチンを呼び出すことによって、後続の処理のために IRP をデキューしたり、状態を "非ビジー" にリセットしたりすることができます。

-   キューの先頭にある IRP を削除するための[**Keremovedevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovedevicequeue)

-   ドライバーによって決定された*SortKey*値に従って選択された IRP を削除するための[**Keremovebykeydevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovebykeydevicequeue)

-   キュー内の特定の IRP を削除したり、特定の IRP がキューにあるかどうかを判断したりするための[**Keremoveentrydevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremoveentrydevicequeue)

    **Keremoveentrydevicequeue**は、IRP がデバイスキューにあったかどうかを示すブール値を返します。

これらのルーチンのいずれかを呼び出して、空であるがビジーなデバイスキューからエントリを削除すると、キューの状態が "ビジー" に変更されます。

各デバイスキューオブジェクトは、組み込みの executive スピンロックによって保護されています ([デバイスキューオブジェクトを使用し](#setting-up-and-using-device-queues)た図には示されていません)。 その結果、ドライバーは Irp をキューに挿入し、IRQL = ディスパッチ\_レベル以下で実行されている任意のドライバールーチンから、マルチプロセッサセーフな方法で Irp を削除できます。 この IRQL の制限により、ドライバーは、DIRQL で実行される ISR または[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンから**Ke*Xxx*devicequeue**ルーチンを呼び出すことができません。

詳細については、「[ハードウェアの優先順位の管理](managing-hardware-priorities.md)」および「[スピンロック](spin-locks.md)」を参照してください。 特定のサポートルーチンの IRQL 要件については、ルーチンのリファレンスページを参照してください。

 

 




