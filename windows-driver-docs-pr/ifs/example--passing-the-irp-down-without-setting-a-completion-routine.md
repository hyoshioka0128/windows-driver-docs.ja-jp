---
title: 完了ルーチンを設定せずに IRP を渡す例
description: 完了ルーチンを設定せずに IRP を渡す例
ms.assetid: d18d3ead-2cec-4ea6-ac4c-b809ba985f23
keywords:
- IRP ディスパッチルーチン WDK ファイルシステム、IRP を渡す
- Irp をデバイススタック WDK に渡す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1131329767e984830a50e2f7949a1e4465ce719
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841424"
---
# <a name="example-passing-the-irp-down-without-setting-a-completion-routine"></a>例: 完了ルーチンを設定せずに IRP を渡す


## <span id="ddk_example_passing_the_irp_down_without_setting_a_completion_routine_"></span><span id="DDK_EXAMPLE_PASSING_THE_IRP_DOWN_WITHOUT_SETTING_A_COMPLETION_ROUTINE_"></span>


完了ルーチンを設定せずに、IRP を下位レベルのドライバーに渡すには、ディスパッチルーチンで次の操作を行う必要があります。

-   現在の IRP スタックの場所を削除するには、 [**Ioskipcurrent entiを**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)呼び出します。これにより、i/o マネージャーは、irp での完了処理を実行するときに、完了ルーチンを検索しません。

-   [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出して、次の下位レベルのドライバーに IRP を渡します。

この手法を次のコード例に示します。

```cpp
IoSkipCurrentIrpStackLocation ( Irp ); 
return IoCallDriver ( NextLowerDriverDeviceObject, Irp ); 
```

または、同等です。

```cpp
IoSkipCurrentIrpStackLocation ( Irp ); 
status = IoCallDriver ( NextLowerDriverDeviceObject, Irp ); 
/* log or debugprint the status value here */
return status; 
```

これらの例では、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)の呼び出しの最初のパラメーターは、次の下位レベルのフィルタードライバーのデバイスオブジェクトへのポインターです。 2番目のパラメーターは、IRP へのポインターです。

### <a name="span-idadvantages_of_this_approachspanspan-idadvantages_of_this_approachspanspan-idadvantages_of_this_approachspanadvantages-of-this-approach"></a><span id="Advantages_of_This_Approach"></span><span id="advantages_of_this_approach"></span><span id="ADVANTAGES_OF_THIS_APPROACH"></span>このアプローチの利点

上記の手法 ( [**Ioskipを**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)呼び出すことができます) は単純で効率的であり、ドライバーが完了ルーチンを登録せずに IRP をドライバースタックに渡すすべての場合に使用する必要があります。

### <a name="span-iddisadvantages_of_this_approachspanspan-iddisadvantages_of_this_approachspanspan-iddisadvantages_of_this_approachspandisadvantages-of-this-approach"></a><span id="Disadvantages_of_This_Approach"></span><span id="disadvantages_of_this_approach"></span><span id="DISADVANTAGES_OF_THIS_APPROACH"></span>このアプローチの欠点

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出すと、 **IoCallDriver**に渡された IRP ポインターは無効になり、安全に逆参照できなくなります。 IRP が下位レベルのドライバーによって処理された後、さらに処理やクリーンアップを実行する必要がある場合は、IRP をドライバースタックに送信する前に、完了ルーチンを設定する必要があります。 入力と完了ルーチンの設定の詳細については、「[完了ルーチンの使用](using-irp-completion-routines.md)」を参照してください。

IRP に対して[**Ioskipに Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出す場合、その IRP の完了ルーチンを設定することはできません。

 

 




