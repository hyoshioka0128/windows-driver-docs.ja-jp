---
title: PendingReturned フラグの確認
description: PendingReturned フラグの確認
ms.assetid: cdcdffb0-4210-4bf0-984e-b0c3234df129
keywords:
- IRP 完了ルーチン WDK ファイルシステム、PendingReturned フラグ
- PendingReturned フラグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ae8538bd1951ab94d81a7079c1a134f51deba97
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841476"
---
# <a name="checking-the-pendingreturned-flag"></a>PendingReturned フラグの確認


## <span id="ddk_checking_the_pendingreturned_flag_if"></span><span id="DDK_CHECKING_THE_PENDINGRETURNED_FLAG_IF"></span>


完了ルーチンがイベントを通知しない場合は、 **Irp&gt;PendingReturned た**フラグを確認する必要があります。 このフラグが設定されている場合、完了ルーチンは[**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出して、保留中の IRP をマークする必要があります。

 

 




