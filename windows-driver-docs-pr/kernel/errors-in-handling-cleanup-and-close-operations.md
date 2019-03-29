---
title: クリーンアップ操作と閉じる操作の処理エラー
description: クリーンアップ操作と閉じる操作の処理エラー
ms.assetid: 9d449974-99b1-4d38-9bbb-54938d67c23a
keywords:
- 信頼性 WDK カーネルでは、エラー
- DispatchClose
- DispatchCleanup
- クリーンアップ エラー WDK カーネル
- エラー WDK カーネルを閉じる
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf9a4344aa5dd9a25948adb638dc145f4809417c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572290"
---
# <a name="errors-in-handling-cleanup-and-close-operations"></a>クリーンアップ操作と閉じる操作の処理エラー





一部のドライバーで必要なタスクを区別するために失敗する[ *DispatchCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)と[ *DispatchClose* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。 I/O マネージャーには、ドライバーの*DispatchCleanup*ルーチン ファイル オブジェクトへの最後のハンドルが閉じられたときにします。 *DispatchClose*ルーチンは、ファイル オブジェクトからの最後の参照が解放されるときに呼び出されます。 ドライバーでのリソースを解放しないでその*DispatchCleanup*ファイル オブジェクトに関連付けられている、またはその他によって使用されているルーチン*ディスパッチ*Xxx ルーチン。

ディスパッチ ルーチンを呼び出すときに、I/O マネージャーは、通常の I/O 呼び出しのファイル オブジェクトへの参照を保持します。 ドライバーが後のファイル オブジェクトの I/O 要求を受信するため、その*DispatchCleanup*ルーチンが前に呼び出されてその*DispatchClose*ルーチンが呼び出されます。 たとえば、ユーザー モードの呼び出し元は、進行中の別のスレッドが I/O マネージャー要求、ファイル ハンドルを閉じることがあります。 ドライバーが削除または I/O マネージャー呼び出される前に必要なリソースを解放する場合、 *DispatchClose*ルーチン、無効なポインターの参照、およびその他の問題が発生する可能性があります。

 

 




