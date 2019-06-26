---
title: 上位レベル ドライバーでのキャンセル ルーチンを使用しないキャンセルの同期
description: 上位レベル ドライバーでのキャンセル ルーチンを使用しないキャンセルの同期
ms.assetid: 741d504e-7e61-4f60-a8cf-e4ea92f0654e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 171f9f60ca4b03b8741553b9dd589a051be611df
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355473"
---
# <a name="synchronizing-cancellation-in-higher-level-drivers-without-cancel-routines"></a>上位レベル ドライバーでのキャンセル ルーチンを使用しないキャンセルの同期





高度なドライバーを推測できませんについてかどうか、または既存の下位レベルのドライバー キャンセル可能な Irp の処理方法。 高度なドライバーを呼び出すと、すぐ[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) IRP の所有していないこと IRP または確認も下位レベルのドライバーが IRP の処理を制御します。

ただしより高度なドライバーを設定できます、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)呼び出して IRP の日常的な[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)前に呼び出し**保留**します。 高度なドライバーが下位のドライバーで呼び出すことによって、保留中の IRP が取り消されたかどうかを判断することができます**IoSetCompletionRoutine**で、 *InvokeOnCancel*パラメーターに設定**TRUE** IRP がドライバーの下に渡す前にします。 こうことをドライバーの*IoCompletion* IRP が取り消されたり、完了したかどうかのルーチンが呼び出されます。

高度なドライバーを呼び出すことができます[ **IoCancelIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocancelirp) IRP がドライバーが割り当てられている保留中のとします。 ただし、この呼び出しを行うとは限りません IRP がドライバーに割り当てられたが、I/O 状態ブロックの状態に設定を完了すること\_が取り消されました。 別のスレッドが IRP を完了する既に可能性があります。 IRP がキャンセルされたかどうかを確認するより高度なドライバーを呼び出す必要があります**IoSetCompletionRoutine**で、 *InvokeOnCancel*パラメーターに設定**TRUE**渡す前に、[次へ] の下位のドライバーに IRP します。 参照してください[Irp の完了](completing-irps.md)完了ルーチンの詳細についてはします。

高度なドライバーを呼び出してはならない**IoCancelIrp**割り当てませんでした IRP にします。

 

 




