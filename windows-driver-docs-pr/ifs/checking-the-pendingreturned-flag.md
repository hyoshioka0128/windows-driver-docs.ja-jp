---
title: PendingReturned フラグのチェック
description: PendingReturned フラグのチェック
ms.assetid: cdcdffb0-4210-4bf0-984e-b0c3234df129
keywords:
- IRP の完了ルーチン WDK ファイル システム、PendingReturned フラグ
- PendingReturned フラグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 040aae998f8fe74a6abe88c35cec8563bcc7e10f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561054"
---
# <a name="checking-the-pendingreturned-flag"></a>PendingReturned フラグのチェック


## <span id="ddk_checking_the_pendingreturned_flag_if"></span><span id="DDK_CHECKING_THE_PENDINGRETURNED_FLAG_IF"></span>


これを確認する必要があります完了ルーチンが、イベントが通知されない場合、 **Irp‑&gt;PendingReturned**フラグ。 このフラグを設定すると、完了ルーチンは呼び出すことによって IRP の保留をマークする必要があります[ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)します。

 

 




