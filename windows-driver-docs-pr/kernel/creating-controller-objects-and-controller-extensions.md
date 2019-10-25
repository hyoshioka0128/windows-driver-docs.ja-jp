---
title: コントローラー オブジェクトとコントローラー拡張の作成
description: コントローラー オブジェクトとコントローラー拡張の作成
ms.assetid: 1f5bfcbc-1d8e-4ace-9539-a25e226444a6
keywords:
- コントローラーオブジェクト WDK カーネル、作成
- IoCreateController
- コントローラー拡張機能の WDK i/o
- 拡張機能の WDK コントローラーオブジェクト
- コントローラーオブジェクト WDK カーネル、拡張機能
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72588b1b51265bacb337d850812678aa078f0e7c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837013"
---
# <a name="creating-controller-objects-and-controller-extensions"></a>コントローラー オブジェクトとコントローラー拡張の作成





ドライバーがコントローラーオブジェクトを使用している場合は、デバイスオブジェクトを作成した後、 [**IoCreateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatecontroller)を呼び出す必要があります。これは通常、PnP\_IRP を受信した後に、\_デバイスの要求を[**開始\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)には、通常は i/o の準備ができています。 次の図は、の呼び出しを示しています。

![コントローラーオブジェクトを示す図](images/3ctlrobj.png)

すべてのコントローラーオブジェクトには、コントローラー拡張機能が関連付けられています。 前の図に示すように、 **IoCreateController**の呼び出し元はコントローラー拡張機能の*サイズ*を決定します。 その構造と内容はドライバーで定義されています。

前の図は、ドライバーが物理コントローラー (またはチャネルを使用したデバイス) について管理するデバイス固有の状態情報に加えて、コントローラー拡張機能のドライバー定義データの代表的なセットを示しています。

**IoCreateController**によって返される*PtrToControllerObject*ポインターは、ドライバーの[**IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)および[**IoFreeController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller)への呼び出しで渡す必要があります。詳細については、「 [i/o のコントローラーオブジェクトの割り当て」を参照してください。操作](allocating-controller-objects-for-i-o-operations.md)。 ドライバーは、返されたコントローラーオブジェクトポインターを、ドライバーによって作成されたデバイスオブジェクトのデバイス拡張機能、またはドライバーによってアクセス可能な別の常駐ストレージ領域 (ドライバーによって割り当てられた非ページプール) に格納する必要があります。 ドライバーがアンロードされた場合は、コントローラーオブジェクトポインターを[**IoDeleteController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iodeletecontroller)に渡す必要もあります。

コントローラーオブジェクトを設定するほとんどのドライバーは、コントローラー拡張機能の現在のターゲットデバイスオブジェクトまたはデバイス拡張機能へのポインターを格納するのに便利です。 通常、このようなドライバーでは、コントローラーオブジェクトのポインターをすべてのデバイス拡張機能の1つに格納します。これにより、コントローラーは、コントローラーによって維持される、i/o に関するコントローラー固有の状態にアクセスするために、コントローラーオブジェクトを *&gt;* 使用できるようになります。すべてのターゲットデバイスオブジェクトに対する操作。

コントローラーオブジェクトによって表される物理コントローラーが割り込みを生成する場合、ドライバーは[**Ioconnectinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)によって返される*PtrToInterruptObject*ポインターのストレージとしてコントローラー拡張機能を使用することもできます。 詳細については、「 [Interrupt Service ルーチン](interrupt-service-routines.md)」を参照してください。

**IoCreateController**は、コントローラーオブジェクトと拡張機能の常駐ストレージを割り当てます。これは0で初期化されます。 メモリを割り当てられない場合、 **IoCreateController**は**NULL**ポインターを返します。 この問題が発生した場合、ドライバーはデバイスの起動に失敗し、リソース\_不足している\_ステータスを返す必要があります。

 

 




