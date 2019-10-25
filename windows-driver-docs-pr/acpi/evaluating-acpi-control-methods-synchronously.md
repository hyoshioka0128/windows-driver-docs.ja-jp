---
title: ACPI 制御メソッドを同期的に評価する
description: ACPI 制御メソッドを同期的に評価する
ms.assetid: 3fd8f7bd-bfae-4846-8051-3a0023d565e4
keywords:
- ACPI 制御メソッド WDK、同期的に評価
- ACPI 制御メソッド WDK、入力バッファー構造
- ACPI 制御方法 WDK、SendDownStreamIrp コードサンプル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9142329595b927cfeec2013a4bfed075804f9c7c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826304"
---
# <a name="evaluating-acpi-control-methods-synchronously"></a>ACPI 制御メソッドを同期的に評価する


デバイスドライバーは、次のデバイス制御要求を使用して、デバイスの ACPI 名前空間で定義されているコントロールメソッドを同期的に評価できます。

-   [**IOCTL\_ACPI\_EVAL\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)

    この要求は、要求が送信されるデバイスの ACPI 名前空間の直下の子オブジェクトである制御メソッドを評価します。

-   [**IOCTL\_ACPI\_EVAL\_メソッド\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)

    この要求は、デバイスによってサポートされているコントロールメソッドまたは要求が送信されたデバイスの子子オブジェクトを同期的に評価します。

Acpi [BIOS](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-bios)のシステムの説明テーブルに指定されているデバイスに代わって、 [Windows acpi ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)(acpi) によってこれらの要求が処理されます。 これらの要求は、[カーネルモードドライバーフレームワーク (KMDF)](https://docs.microsoft.com/windows-hardware/drivers/wdf/design-guide)または[Windows Driver Model (WDM)](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)の要件に準拠するカーネルモードデバイスドライバーによって使用されます。 Windows 8 以降では、[ユーザーモードドライバーフレームワーク (UMDF)](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)の要件に準拠するユーザーモードデバイスドライバーは、これらの要求を使用できます。

たとえば、WDM ドライバーは次の一連の操作を実行して、これらの Ioctl のいずれかを使用します。

1.  [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)を呼び出して要求をビルドします。

2.  [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、デバイススタックで要求を送信します。

3.  I/o マネージャーが、下位レベルのドライバーが要求を完了したことをドライバーに通知するまで待機します。

4.  要求の状態を確認します。

5.  出力引数が有効かどうかを確認します。

6.  ドライバーに返される出力引数を処理します。

7.  要求を完了します。

要求を作成するために、ドライバーは**IoBuildDeviceIoControlRequest**を呼び出し、次のパラメーターを提供します。

-   *Iocontrolcode*が**ioctl\_acpi\_eval\_Method**または**ioctl\_acpi\_eval\_method\_EX**に設定されています。

-   *DeviceObject*は、デバイスの物理デバイスオブジェクト (PDO) へのポインターに設定されます。

-   *InputBuffer*は、コントロールメソッドに渡される入力引数の型に依存する入力バッファー構造へのポインターに設定されます。 ACPI ドライバーでは、入力引数を受け取らないメソッド、1つの整数を受け取るメソッド、ASCII 文字列を受け取るメソッド、または入力引数のカスタム配列を受け取るメソッドがサポートされています。 サポートされている入力バッファー構造の詳細については、「 [Control メソッドの入力バッファー構造](control-method-input-buffer-structures.md)」を参照してください。

-   *Inputbufferlength*は、 *InputBuffer*によって指定された入力バッファーのサイズ (バイト単位) に設定されます。

-   *Outputbufferlength*は、 *outputbuffer*によって提供される出力バッファーのサイズ (バイト単位) を提供します。

-   *InternalDeviceIoControl*が**FALSE**に設定されています。

-   *イベント*は、呼び出し元が割り当てられ、初期化されたイベントオブジェクトへのポインターに設定されます。 ドライバーは、i/o マネージャーがこのイベントを通知するまで待機します。これは、下位レベルのドライバーが要求を完了したことを示します。

-   *Outputbuffer*は、コントロールメソッドからの出力引数を格納する、 [**ACPI\_EVAL\_出力\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)構造へのポインターを提供します。 出力引数は、特定のコントロールメソッドに固有です。 ドライバーが出力を返すには、すべての出力引数を保持するのに十分な大きさのバッファーを割り当てる必要があります。

-   *Iostatusblock*は、 [**IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造に設定されています。 これにより、下位レベルのドライバーによって設定された要求の状態が返されます。

入力引数を受け取らないコントロールメソッドを評価する方法のコード例については、「[入力引数を使用しないコントロールメソッドの評価](evaluating-a-control-method-without-input-arguments.md)」を参照してください。

入力引数を受け取るコントロールメソッドを評価する方法のコード例については、「[入力引数を受け取るコントロールメソッドの評価](evaluating-a-control-method-that-takes-input-arguments.md)」を参照してください。
