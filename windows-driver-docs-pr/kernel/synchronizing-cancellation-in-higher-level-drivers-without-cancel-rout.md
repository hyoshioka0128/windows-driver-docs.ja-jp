---
title: 上位レベル ドライバーでのキャンセル ルーチンを使用しないキャンセルの同期
description: 上位レベル ドライバーでのキャンセル ルーチンを使用しないキャンセルの同期
ms.assetid: 741d504e-7e61-4f60-a8cf-e4ea92f0654e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c2ce793697e94ac3e15a449dcc8ccb8f29864b97
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838395"
---
# <a name="synchronizing-cancellation-in-higher-level-drivers-without-cancel-routines"></a>上位レベル ドライバーでのキャンセル ルーチンを使用しないキャンセルの同期





上位レベルのドライバーでは、既存の下位レベルのドライバーがキャンセル可能な Irp を処理するかどうか、またはその方法を想定していない場合があります。 上位レベルのドライバーは、IRP の[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出すとすぐに、その irp を所有しなくなります。また、下位レベルのドライバーによる irp の処理を確認したり制御したりすることはできません。

ただし、上位レベルのドライバーでは、 **IoCallDriver**を呼び出す前に[**iosetcompletion ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)を呼び出すことによって、IRP の[*iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定できます。 上位レベルのドライバーでは、IRP を下位のドライバーに渡す前に、 *InvokeOnCancel*パラメーターを**TRUE**に設定して**ioset ルーチン**を呼び出すことにより、保留中の irp が下位のドライバーで取り消されたかどうかを判断できます。 これにより、IRP が取り消されたか完了したかにかかわらず、ドライバーの*Iocompletion*ルーチンが呼び出されるようになります。

上位レベルのドライバーは、ドライバーによって割り当てられた保留中の IRP で[**Iocancelirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)を呼び出すことができます。 ただし、この呼び出しを行っても、ドライバーによって割り当てられる IRP は、i/o 状態ブロックが状態\_キャンセルされた状態で完了します。別のスレッドが既に IRP を完了している可能性があります。 IRP が取り消されたかどうかを確認するには、より高いレベルのドライバーで**IosetInvokeOnCancel ルーチン**を呼び出す必要があります。これは、irp を次の下位のドライバーに渡す前に**TRUE**に設定します。 完了ルーチンの詳細については、「 [irp の完了](completing-irps.md)」を参照してください。

上位レベルのドライバーは、割り当てられていない IRP で**Iocancelirp**を呼び出すことはできません。

 

 




