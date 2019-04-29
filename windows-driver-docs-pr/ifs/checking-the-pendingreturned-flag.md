---
title: PendingReturned フラグの確認
description: PendingReturned フラグの確認
ms.assetid: cdcdffb0-4210-4bf0-984e-b0c3234df129
keywords:
- IRP の完了ルーチン WDK ファイル システム、PendingReturned フラグ
- PendingReturned フラグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 040aae998f8fe74a6abe88c35cec8563bcc7e10f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327906"
---
# <a name="checking-the-pendingreturned-flag"></a>PendingReturned フラグの確認


## <span id="ddk_checking_the_pendingreturned_flag_if"></span><span id="DDK_CHECKING_THE_PENDINGRETURNED_FLAG_IF"></span>


これを確認する必要があります完了ルーチンが、イベントが通知されない場合、 **Irp‑&gt;PendingReturned**フラグ。 このフラグを設定すると、完了ルーチンは呼び出すことによって IRP の保留をマークする必要があります[ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)します。

 

 




