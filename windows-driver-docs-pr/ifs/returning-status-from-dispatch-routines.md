---
title: ディスパッチ ルーチンから返される状態
description: ディスパッチ ルーチンから返される状態
ms.assetid: 76bd651a-344f-4e22-a435-b62fdf2d7ddc
keywords:
- IRP ディスパッチルーチン WDK ファイルシステム、ステータスを返す
- 状態値 WDK ファイルシステム
- 成功の状態の値 WDK ファイルシステム
- ステータス WDK ファイルシステムを返す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09b464f79b79c54821ef491ec004670dc68bc075
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840986"
---
# <a name="returning-status-from-dispatch-routines"></a>ディスパッチ ルーチンから返される状態


## <span id="ddk_returning_status_from_dispatch_routines_if"></span><span id="DDK_RETURNING_STATUS_FROM_DISPATCH_ROUTINES_IF"></span>


IRP を完了する場合を除き、完了ルーチンを設定しないディスパッチルーチンは、常に[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)から返された NTSTATUS 値を返す必要があります。 この値が [\_保留中] の場合を除き、irp を完了したドライバーによって設定された**irp&gt;IoStatus. status**の値と一致する必要があります。

IRP をワークキューにポストする可能性のある完了ルーチンを設定するディスパッチルーチンでは、次のいずれかを実行する必要があります。

-   **IoCallDriver**によって返された NTSTATUS 値を返します。

-   完了ルーチンによってイベントが通知され、 **Irp&gt;IoStatus. Status**の値が返されるまで待機します。

-   IRP を保留中としてマークし、作業キューにポストして、状態\_保留中に戻します。

-   完了ルーチンが IRP をワークキューにポストする可能性がある場合、ディスパッチルーチンは、IRP pending および return STATUS\_PENDING とマークする必要があります。

これらの動作のうち、どれが適切であるか、または可能であるかは、特定の操作によって異なります。 ディレクトリ変更通知など、一部の操作は同期できません。また、一部 (oplock など) を非同期にすることはできません。

ディスパッチルーチンから状態を返す方法の詳細については、「[ディスパッチルーチンの制約](constraints-on-dispatch-routines.md)」を参照してください。

 

 




