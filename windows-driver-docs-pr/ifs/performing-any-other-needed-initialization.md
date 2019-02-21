---
title: 他の必要な初期化を実行します。
description: 他の必要な初期化を実行します。
ms.assetid: 781f241f-fb12-460e-b093-ffa916aae495
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e93262dd653ad7fd17f260ff38f75a61135dd745
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530553"
---
# <a name="performing-any-other-needed-initialization"></a>他の必要な初期化を実行します。


## <span id="ddk_performing_any_other_needed_initialization_if"></span><span id="DDK_PERFORMING_ANY_OTHER_NEEDED_INITIALIZATION_IF"></span>


IRP と高速の I/O の登録後にディスパッチ ルーチンの場合、ファイル システム フィルター ドライバーの**DriverEntry**ルーチンは必要に応じて、グローバルの追加のドライバーの変数とデータの構造体を初期化できます。

 

 




