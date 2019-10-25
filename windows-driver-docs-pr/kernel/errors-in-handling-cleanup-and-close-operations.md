---
title: クリーンアップ操作と閉じる操作の処理エラー
description: クリーンアップ操作と閉じる操作の処理エラー
ms.assetid: 9d449974-99b1-4d38-9bbb-54938d67c23a
keywords:
- 信頼性 WDK カーネル、エラー
- DispatchClose
- DispatchCleanup
- クリーンアップエラー WDK カーネル
- エラーを閉じる WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 958c9b739a9857d9d184537bc4623375b791219c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836757"
---
# <a name="errors-in-handling-cleanup-and-close-operations"></a>クリーンアップ操作と閉じる操作の処理エラー





一部のドライバーでは、 [*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンと[*DispatchClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンで必要とされるタスクを区別できません。 I/o マネージャーは、ファイルオブジェクトへの最後のハンドルが閉じられたときに、ドライバーの*DispatchCleanup*ルーチンを呼び出します。 *DispatchClose*ルーチンは、ファイルオブジェクトから最後の参照が解放されるときに呼び出されます。 ドライバーは、ファイルオブジェクトにアタッチされているか、他の*ディスパッチ*Xxx ルーチンによって使用される可能性がある、 *DispatchCleanup*ルーチン内のリソースを解放しようとしないでください。

ディスパッチルーチンを呼び出すとき、i/o マネージャーは、通常の i/o 呼び出しのファイルオブジェクトへの参照を保持します。 その結果、ドライバーは、 *DispatchCleanup*ルーチンが呼び出された後、 *DispatchClose*ルーチンが呼び出される前に、ファイルオブジェクトの i/o 要求を受け取ることができます。 たとえば、ユーザーモードの呼び出し元は、i/o マネージャーの要求が別のスレッドから実行されている間にファイルハンドルを閉じる場合があります。 I/o マネージャーが*DispatchClose*ルーチンを呼び出す前に、ドライバーによって必要なリソースが削除または解放された場合、無効なポインター参照やその他の問題が発生する可能性があります。

 

 




