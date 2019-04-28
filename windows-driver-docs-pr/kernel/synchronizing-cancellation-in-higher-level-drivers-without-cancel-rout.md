---
title: 上位レベル ドライバーでのキャンセル ルーチンを使用しないキャンセルの同期
description: 上位レベル ドライバーでのキャンセル ルーチンを使用しないキャンセルの同期
ms.assetid: 741d504e-7e61-4f60-a8cf-e4ea92f0654e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5d71b962278ea66de32d11639848f8bd78d5b3e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377892"
---
# <a name="synchronizing-cancellation-in-higher-level-drivers-without-cancel-routines"></a>上位レベル ドライバーでのキャンセル ルーチンを使用しないキャンセルの同期





高度なドライバーを推測できませんについてかどうか、または既存の下位レベルのドライバー キャンセル可能な Irp の処理方法。 高度なドライバーを呼び出すと、すぐ[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) IRP の所有していないこと IRP または確認も下位レベルのドライバーが IRP の処理を制御します。

ただしより高度なドライバーを設定できます、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)呼び出して IRP の日常的な[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)前に呼び出し**保留**します。 高度なドライバーが下位のドライバーで呼び出すことによって、保留中の IRP が取り消されたかどうかを判断することができます**IoSetCompletionRoutine**で、 *InvokeOnCancel*パラメーターに設定**TRUE** IRP がドライバーの下に渡す前にします。 こうことをドライバーの*IoCompletion* IRP が取り消されたり、完了したかどうかのルーチンが呼び出されます。

高度なドライバーを呼び出すことができます[ **IoCancelIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548338) IRP がドライバーが割り当てられている保留中のとします。 ただし、この呼び出しを行うとは限りません IRP がドライバーに割り当てられたが、I/O 状態ブロックの状態に設定を完了すること\_が取り消されました。 別のスレッドが IRP を完了する既に可能性があります。 IRP がキャンセルされたかどうかを確認するより高度なドライバーを呼び出す必要があります**IoSetCompletionRoutine**で、 *InvokeOnCancel*パラメーターに設定**TRUE**渡す前に、[次へ] の下位のドライバーに IRP します。 参照してください[Irp の完了](completing-irps.md)完了ルーチンの詳細についてはします。

高度なドライバーを呼び出してはならない**IoCancelIrp**割り当てませんでした IRP にします。

 

 




