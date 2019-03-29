---
title: 操作前と操作後のコールバック ルーチンの記述
description: 操作前と操作後のコールバック ルーチンの記述
ms.assetid: ad706d01-7a14-4730-8189-c465637987dc
keywords:
- ファイル システム ミニフィルター ドライバー WDK、preoperation コールバック ルーチン
- ミニフィルター ドライバー WDK、preoperation コールバック ルーチン
- preoperation コールバック ルーチン WDK ファイル システム ミニフィルター、preoperation コールバック ルーチンについて
- postoperation コールバック ルーチン WDK ファイル システム ミニフィルター、postoperation コールバック ルーチンについて
- ファイル システム ミニフィルター ドライバー WDK、postoperation コールバック ルーチン
- ミニフィルター ドライバー WDK、postoperation コールバック ルーチン
- preoperation コールバック ルーチン WDK ファイル システム ミニフィルター
- postoperation コールバック ルーチン WDK ファイル システム ミニフィルター
- ファイル システムの I/O の WDK
- コールバック ルーチン WDK ファイル システム
- I/O 操作の WDK ファイル システム ミニフィルターをフィルター処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7bd355067810fbcee2feeb6c07aac0da43e48d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572000"
---
# <a name="writing-preoperation-and-postoperation-callback-routines"></a>操作前と操作後のコールバック ルーチンの記述


## <span id="ddk_writing_preoperation_and_postoperation_callback_routines_if"></span><span id="DDK_WRITING_PREOPERATION_AND_POSTOPERATION_CALLBACK_ROUTINES_IF"></span>


その**DriverEntry** 、日常的なミニフィルター ドライバーを登録できますを 1 つまで[ **preoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551109)と 1 つの[ **postoperation コールバック ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff551107)をフィルター処理する必要がある I/O 操作の種類ごとにします。

ミニフィルター ドライバーは、従来のファイル システム フィルター ドライバーとは異なり、フィルター処理する I/O 操作の種類を選択できます。 ミニフィルター ドライバーは、postoperation コールバックの登録を行わずに特定の種類の I/O 操作の preoperation コールバック ルーチンを登録でき、その逆です。 ミニフィルター ドライバーでは、preoperation または postoperation コールバック ルーチンを登録することが I/O 操作のみを受信します。

A *preoperation コールバック ルーチン*はレガシ フィルター ドライバー モデル内のディスパッチ ルーチンに似ています。 フィルター マネージャーは、I/O 操作を処理するときは、この種類の I/O 操作のいずれかが登録したミニフィルター ドライバー インスタンス スタックで各ミニフィルター ドライバーの preoperation コールバック ルーチンを呼び出します。 最上位のミニフィルター ドライバー スタック--では、1 つのインスタンスが上限の高度 - 最初に受け取ります操作。 ミニフィルター ドライバーでは、操作の処理が完了したら、次に高いミニフィルター ドライバーに、操作を通過するフィルター マネージャーに、操作を返します。 ミニフィルター ドライバーには、I/O 操作が完了していなければ、ミニフィルター ドライバーのインスタンスのスタック内のすべてのミニフィルター ドライバーの I/O 操作 - が処理するときに、レガシ フィルターを操作し、ファイル システム フィルター マネージャーが送信します。

A *postoperation コールバック ルーチン*はレガシ フィルター ドライバー モデル内の終了ルーチンに似ています。 完了、I/O 操作の処理は、I/O マネージャー操作の完了のルーチンが登録されているファイル システムとレガシ フィルターに渡すと、操作を開始します。 これらのルーチンの完了が完了した後、フィルター マネージャーは、完了操作の処理を実行します。 フィルター マネージャーは、この種類の I/O 操作のいずれかが登録したミニフィルター ドライバー インスタンス スタックで、各ミニフィルター ドライバーの postoperation コールバック ルーチンを呼び出します。 下部にあるミニフィルター ドライバー - スタックでは、1 つのインスタンスが最も低い高度で - 最初に受け取ります操作。 ミニフィルター ドライバーでは、操作の処理が完了したら、[次へ] 最小ミニフィルター ドライバーに、操作を通過するフィルター マネージャーを返します。

このセクションの内容:

[Preoperation と Postoperation を登録するコールバック ルーチン](registering-preoperation-and-postoperation-callback-routines.md)

[ミニフィルター ドライバーでの I/O 操作をフィルター処理](filtering-i-o-operations-in-a-minifilter-driver.md)

[Preoperation コールバック ルーチンを記述](writing-preoperation-callback-routines.md)

[Postoperation コールバック ルーチンを記述](writing-postoperation-callback-routines.md)

[I/O 操作のパラメーターを変更します。](modifying-the-parameters-for-an-i-o-operation.md)

[I/O 操作のバッファリング方法の決定](determining-the-buffering-method-for-an-i-o-operation.md)

[I/O 操作のユーザー バッファーへのアクセス](accessing-the-user-buffers-for-an-i-o-operation.md)

 

 




