---
title: IRP_MJ_CLEANUP
description: プロセス固有のコンテキスト情報を管理するドライバーには、DispatchCleanup ルーチンでクリーンアップ要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 097f5f1d-3e88-4db0-bb79-db2267bdaf38
keywords:
- IRP_MJ_CLEANUP Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: a6c8959931957965cf13143fc14747934727e816
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327296"
---
# <a name="irpmjcleanup"></a>IRP\_MJ\_CLEANUP


プロセス固有のコンテキスト情報を管理するドライバーのクリーンアップ要求を処理する必要があります[ *DispatchCleanup* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

<a name="when-sent"></a>送信時
---------

この要求の受信は、ターゲット デバイス オブジェクトに関連付けられているファイル オブジェクトの最後のハンドルが閉じられたことを示します (ただし、未処理の I/O のため、要求が解放されていない)。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

<a name="operation"></a>操作
---------

ファイル オブジェクトのハンドルを終了したプロセスのコンテキストでは、この IRP が送信されます。 そのため、ドライバーはドライバーが以前ロックされているか、マップされていることをユーザー メモリなどのプロセスに固有のリソースをリリースする必要があります。

ドライバーのデバイス オブジェクトが設定されている場合の排他として、一度に 1 つのスレッドのみがデバイスを使用できるようにドライバーする必要があります完了現在ターゲット デバイス オブジェクトをキューに登録し、状態を設定するすべての IRP\_各 IRP の I/O の状態が取り消されましたブロックです。

それ以外の場合、ドライバーはキャンセルし、リリースされる、ファイル オブジェクトのハンドルに関連付けられている現在キューに置かれた Irp の完了する必要があります。 (ファイル オブジェクトへのポインターにある、 **FileObject**のドライバーのメンバー [ **IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659) IRP の)。ドライバーが IRP のクリーンアップが完了して状態を設定後、これらをキャンセルするには、Irp をキューに置かれた、\_I/O の状態のブロックで成功します。

この要求の処理の詳細については、次を参照してください。 [DispatchCleanup ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff543242)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[**IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)

[**IRP\_MJ\_CLOSE**](irp-mj-close.md)

 

 




