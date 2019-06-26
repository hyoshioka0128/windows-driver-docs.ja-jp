---
title: PendingReturned フラグの確認
description: PendingReturned フラグの確認
ms.assetid: cdcdffb0-4210-4bf0-984e-b0c3234df129
keywords:
- IRP の完了ルーチン WDK ファイル システム、PendingReturned フラグ
- PendingReturned フラグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be4e5e06114cfaaa1a87edc50c19b80bc65e948b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379008"
---
# <a name="checking-the-pendingreturned-flag"></a>PendingReturned フラグの確認


## <span id="ddk_checking_the_pendingreturned_flag_if"></span><span id="DDK_CHECKING_THE_PENDINGRETURNED_FLAG_IF"></span>


これを確認する必要があります完了ルーチンが、イベントが通知されない場合、 **Irp‑&gt;PendingReturned**フラグ。 このフラグを設定すると、完了ルーチンは呼び出すことによって IRP の保留をマークする必要があります[ **IoMarkIrpPending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)します。

 

 




