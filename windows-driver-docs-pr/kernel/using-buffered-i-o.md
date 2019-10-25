---
title: バッファー付き I/O の使用
description: バッファー付き I/O の使用
ms.assetid: 69291156-babb-465a-9e80-1766f075768b
keywords:
- バッファーされる i/o WDK カーネル
- バッファー (WDK i/o、バッファー i/o)
- データバッファー WDK i/o、バッファー i/o
- 非ページシステムバッファー (WDK i/o)
- I/o 制御コード WDK カーネル、バッファーされる i/o
- I/o WDK カーネル、バッファー i/o
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55676be840c1f446056457cec777459a86c2104b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836031"
---
# <a name="using-buffered-io"></a>バッファー付き I/O の使用





対話型または低速のデバイス、または通常は比較的少量のデータを一度に転送するドライバーは、バッファーされた[i/o](methods-for-accessing-data-buffers.md)転送方法を使用する必要があります。 バッファー内 i/o を使用して小規模な対話型転送を使用すると、物理メモリ全体の使用量が向上します。これは、ダイレクト i/o を要求するドライバーの場合と同じように、メモリマネージャーは転送ごとに完全な物理ページをロックダウンする必要がないためです。 一般に、ビデオ、キーボード、マウス、シリアル、およびパラレルのドライバーは、バッファリングされた i/o を要求します。

I/o マネージャーは、i/o 操作で次のようにバッファーされた i/o を使用していると判断します。

-   [**Irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)および[**irp\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求の場合は、[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造の**Flags**メンバーにバッファー\_IO を設定します。 詳細については、「[デバイスオブジェクトの初期化](initializing-a-device-object.md)」を参照してください。

-   [**Irp\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)と[**irp\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求の場合、IOCTL コードの値には、 *TRANSFERTYPE*値としてバッファーに格納されているメソッドが含まれます。IOCTL 値。 詳細については、「 [I/o 制御コードの定義](defining-i-o-control-codes.md)」を参照してください。

次の図は、i/o マネージャーが、バッファー i/o を使用する転送操作の**IRP\_MJ\_読み取り**要求を設定する方法を示しています。

![ユーザーバッファーのバッファー i/o を示す図](images/3mdlbffr.png)

次の図は、ドライバーがデバイスオブジェクトの**フラグ**と DO\_バッファリング\_IO を使用して、読み取り要求のデータを転送するときに、IRP 内の**systembuffer**ポインターを使用する方法の概要を示しています。

1.  一部のユーザー領域の仮想アドレスは、現在のスレッドのバッファーを表し、バッファーの内容はページベースの物理アドレスの範囲内のどこかに格納されている可能性があります (前の図では濃い網掛け)。

2.  I/o マネージャーは、現在のスレッドの読み取り要求をサービスします。この要求は、スレッドがバッファーを表すユーザー空間の仮想アドレスの範囲を渡します。

3.  I/o マネージャーは、ユーザーが指定したバッファーにアクセシビリティがあるかどうかを確認し、 [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)を呼び出して、ユーザーが指定したバッファーのサイズを非ページシステムスペースバッファー (**systembuffer**) で作成します。

4.  I/o マネージャーは、ドライバーに送信される IRP で、新しく割り当てられた**Systembuffer**にアクセスできるようにします。

    図に書き込み要求が示されている場合、i/o マネージャーは、IRP をドライバーに送信する前に、ユーザーバッファーからシステムバッファーにデータをコピーします。

5.  前の図に示されている読み取り要求の場合、ドライバーはデバイスからシステム領域バッファーにデータを読み込みます。 このバッファーのメモリはページングされていません。ドライバーは、最初にロックせずにバッファーに安全にアクセスできます。 読み取り要求が満たされると、ドライバーは IRP を使用して[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出します。

6.  元のスレッドが再びアクティブになると、i/o マネージャーによって、読み込まれたデータがシステムバッファーからユーザーバッファーにコピーされます。 また、 [**Exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)を呼び出してシステムバッファーを解放します。

I/o マネージャーによってドライバー用のシステム領域バッファーが作成された後は、要求元のユーザーモードスレッドをスワップアウトして、その物理メモリを別のスレッドで再利用できます (場合によっては、別のプロセスに属するスレッドを使用します)。 ただし、IRP に指定されたシステムスペースの仮想アドレス範囲は、ドライバーが IRP で[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出すまで有効なままです。

一度に大量のデータを転送するドライバー (特に、複数ページにわたる転送を行うドライバー) は、バッファー i/o を使用しないようにする必要があります。 システムを実行すると、非ページプールが断片化されることがあります。これにより、i/o マネージャーは、このようなドライバーの Irp で送信するために、サイズの大きい連続したシステムスペースバッファーを割り当てることができなくなります。

通常、ドライバーでは、i/o を[直接](methods-for-accessing-data-buffers.md)使用する場合でも、 [**irp\_MJ\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求など、一部の種類の irp に対してバッファー i/o を使用します。 ダイレクト i/o を使用するドライバーは、通常、 [**irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)および[**irp\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求、および場合によってはドライバーで定義された[**irp\_MJ\_内部\_デバイス\_コントロールに対してのみ実行されます。** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)大きなデータ転送を必要とする要求。

すべての**irp\_MJ\_デバイス\_control**および**irp\_MJ\_内部\_デバイス\_コントロール**要求には、i/o 制御コードが含まれています。 I/o 制御コードが、バッファー i/o を使用して IRP がサポートされている必要があることを示している場合、i/o マネージャーは、1つのシステムバッファーを使用して、ユーザーアプリケーションの入力バッファーと出力バッファーを表します。 このような i/o 制御コードをサポートするドライバーは、バッファーから入力データ (存在する場合) を読み取り、入力データを上書きすることによって出力データ (存在する場合) を指定する必要があります。 詳細については、「 [I/o 制御コードの定義](defining-i-o-control-codes.md)」を参照してください。

 

 




