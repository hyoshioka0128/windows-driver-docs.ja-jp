---
title: 完了、I/O 操作の処理を実行します。
description: 完了、I/O 操作の処理を実行します。
ms.assetid: 7e65c21c-d38f-4804-8c07-6cd89f6a6dd6
keywords:
- postoperation コールバック ルーチン WDK ファイル システム ミニフィルター、処理の完了
- WDK のファイル システムを要求する I/O の完了
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0950c3ad81ed4f5b7ddd4e3e65e291540c68dd85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551825"
---
# <a name="performing-completion-processing-for-an-io-operation"></a>完了、I/O 操作の処理を実行します。


## <span id="ddk_performing_completion_processing_for_an_io_operation_if"></span><span id="DDK_PERFORMING_COMPLETION_PROCESSING_FOR_AN_IO_OPERATION_IF"></span>


ミニフィルター ドライバーの[ **postoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551107)基になるファイル システム、レガシ フィルター、または他のミニフィルター ドライバーにある I/O 操作が完了したときに呼び出されますが、ミニフィルター ドライバーのインスタンスのスタックでの高度の低い。

さらに、ミニフィルター ドライバーのインスタンスが破棄されるときに、フィルター マネージャー「ドレイン」、インスタンスが受信するすべての I/O 操作を[ **preoperation コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff551109) を待機していますが、[**postoperation コールバック**](https://msdn.microsoft.com/library/windows/hardware/ff551107)します。 フィルター マネージャーが I/O 操作が完了していないと、FLTFL を設定する場合でも、ミニフィルター ドライバーの postoperation コールバック ルーチンを呼び出すこのような状況で\_POST\_操作\_ドレイン中、フラグ*フラグ*入力パラメーター。

ときに、FLTFL\_POST\_操作\_ドレイン中のフラグが設定されて、ミニフィルター ドライバーでは、正常に終了処理は実行する必要があります。 代わりに、ミニフィルター ドライバーに割り当てられたメモリの解放など、必要なだけのクリーンアップを使用する場合を実行する必要がありますが、 *CompletionContext*パラメーターでは、preoperation コールバック ルーチンと戻り値の FLT\_POSTOP\_完了\_処理します。

このセクションには、次のトピックが含まれます。

[安全な IRQL で完了処理が実行されることを確認](ensuring-that-completion-processing-is-performed-at-safe-irql.md)

 

 




