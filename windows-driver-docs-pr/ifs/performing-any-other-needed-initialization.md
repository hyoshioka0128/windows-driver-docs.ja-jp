---
title: その他必要な初期化の実行
description: その他必要な初期化の実行
ms.assetid: 781f241f-fb12-460e-b093-ffa916aae495
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e93262dd653ad7fd17f260ff38f75a61135dd745
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352771"
---
# <a name="performing-any-other-needed-initialization"></a>その他必要な初期化の実行


## <span id="ddk_performing_any_other_needed_initialization_if"></span><span id="DDK_PERFORMING_ANY_OTHER_NEEDED_INITIALIZATION_IF"></span>


IRP と高速の I/O の登録後にディスパッチ ルーチンの場合、ファイル システム フィルター ドライバーの**DriverEntry**ルーチンは必要に応じて、グローバルの追加のドライバーの変数とデータの構造体を初期化できます。

 

 




