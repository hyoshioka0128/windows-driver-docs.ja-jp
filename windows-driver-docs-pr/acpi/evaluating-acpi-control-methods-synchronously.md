---
title: ACPI 制御メソッドを同期的に評価する
description: ACPI 制御メソッドを同期的に評価する
ms.assetid: 3fd8f7bd-bfae-4846-8051-3a0023d565e4
keywords:
- ACPI 制御メソッド WDK、同期的に評価します。
- ACPI 制御メソッド WDK、入力バッファーの構造体
- ACPI 制御メソッド WDK、SendDownStreamIrp コード サンプル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c5a09a840543b8d122a3cc5ba2fae0279e023a1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355835"
---
# <a name="evaluating-acpi-control-methods-synchronously"></a>ACPI 制御メソッドを同期的に評価する


デバイス ドライバーは、次のデバイス制御要求を使用して、デバイスを ACPI 名前空間で定義されている制御メソッドを同期的に評価できます。

-   [**IOCTL\_ACPI\_EVAL\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_eval_method)

    この要求は、要求を送信するデバイスの ACPI 名前空間で直接の子オブジェクトであるコントロールのメソッドを評価します。

-   [**IOCTL\_ACPI\_EVAL\_メソッド\_例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ni-acpiioct-ioctl_acpi_eval_method_ex)

    この要求が同期的に、デバイスまたはデバイスの子オブジェクトでサポートされているコントロールのメソッドを評価する、要求が送信されます。

[ACPI の Windows ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)、Acpi.sys、システムの説明テーブルに指定されているデバイスに代わって、これらの要求の処理、 [ACPI BIOS](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-bios)します。 これらの要求の要件に適合するカーネル モード デバイス ドライバーで使用できる[カーネル モード ドライバー フレームワーク (KMDF)](https://docs.microsoft.com/windows-hardware/drivers/wdf/design-guide)または[Windows Driver Model (WDM)](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)します。 Windows 8 以降で、ユーザー モード デバイス ドライバーの要件に適合する[ユーザー モード ドライバー フレームワーク (UMDF)](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)これらの要求を使用することができます。

たとえば、WDM ドライバーは、次の一連のこれらの Ioctl のいずれかを使用する操作を実行します。

1.  呼び出し[ **IoBuildDeviceIoControlRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)要求を構築します。

2.  呼び出し[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)デバイス スタックの要求を送信します。

3.  下位レベルのドライバーが要求を完了したことをドライバーに通知する I/O マネージャーを待機します。

4.  要求の状態を確認します。

5.  出力引数の有効性を確認します。

6.  ドライバーに返される出力引数を処理します。

7.  要求を完了します。

ドライバーを呼び出し、要求をビルドする**IoBuildDeviceIoControlRequest**し、次のパラメーターを提供します。

-   *IoControlCode*に設定されている**IOCTL\_ACPI\_EVAL\_メソッド**または**IOCTL\_ACPI\_EVAL\_メソッド\_EX**します。

-   *デバイス オブジェクト*デバイスの物理デバイス オブジェクト (PDO) へのポインターに設定されます。

-   *InputBuffer*コントロール メソッドに渡される入力引数の型に依存する入力バッファーの構造体へのポインターに設定されます。 ACPI ドライバーには、引数を受け取らない入力、1 つの整数を取るを ASCII 文字列を受け取るまたはカスタムの入力引数の配列を受け取るメソッドがサポートしています。 入力バッファーがサポートされている構造体の詳細については、次を参照してください。[制御メソッドの入力バッファーの構造](control-method-input-buffer-structures.md)します。

-   *InputBufferLength*によって提供される入力バッファーのバイト単位のサイズに設定されている*InputBuffer*します。

-   *OutputBufferLength*によって提供される出力バッファーのバイト単位のサイズを提供*OutputBuffer*します。

-   *InternalDeviceIoControl*に設定されている**FALSE**します。

-   *イベント*呼び出し元が割り当てたで初期化イベント オブジェクトへのポインターに設定されます。 ドライバーは、I/O マネージャーは、このイベントは、下位レベルのドライバーが要求を完了していることを示しますを通知するまで待機します。

-   *OutputBuffer*へのポインターを提供する[ **ACPI\_EVAL\_出力\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)からの出力引数を含む構造体、メソッドを制御します。 出力引数は、特定の制御メソッドに固有です。 任意の出力を返すドライバーの場合は、すべての出力引数を保持するために十分な大きさのバッファーを割り当てる必要があります。

-   *IoStatusBlock*に設定されている、 [ **IO\_状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)構造体。 下位レベルのドライバーによって設定された要求の状態が返されます。

入力引数を受け取らないコントロールのメソッドを評価する方法のコード例では、次を参照してください。[コントロール メソッドなし入力引数を評価する](evaluating-a-control-method-without-input-arguments.md)します。

入力引数を受け取るコントロール メソッドを評価する方法のコード例では、次を参照してください。[コントロール メソッドは、その入力引数を評価する](evaluating-a-control-method-that-takes-input-arguments.md)します。
