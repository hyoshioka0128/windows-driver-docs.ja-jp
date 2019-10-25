---
title: IRP_MJ_CLEANUP
description: プロセス固有のコンテキスト情報を保持するドライバーは、DispatchCleanup ルーチンでクリーンアップ要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 097f5f1d-3e88-4db0-bb79-db2267bdaf38
keywords:
- IRP_MJ_CLEANUP カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 2305708032d2ad491766481b78194de4af836efd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828136"
---
# <a name="irp_mj_cleanup"></a>IRP\_MJ\_CLEANUP


プロセス固有のコンテキスト情報を保持するドライバーは、 [*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンでクリーンアップ要求を処理する必要があります。

<a name="when-sent"></a>送信時
---------

この要求の受信は、ターゲットデバイスオブジェクトに関連付けられているファイルオブジェクトの最後のハンドルが閉じられていることを示します (ただし、未処理の i/o 要求によって、解放されていない可能性があります)。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

<a name="operation"></a>操作
---------

この IRP は、ファイルオブジェクトハンドルを閉じたプロセスのコンテキストで送信されます。 そのため、ドライバーは、以前にロックまたはマップされたユーザーメモリなどのプロセス固有のリソースを解放する必要があります。

ドライバーのデバイスオブジェクトが排他的として設定されていて、1つのスレッドのみが一度にデバイスを使用できるようにする場合、ドライバーは、ターゲットデバイスオブジェクトに現在キューに置かれているすべての IRP を完了し、各 IRP の i/o 状態ブロックで状態\_キャンセルする必要があります。

それ以外の場合、ドライバーは、解放されているファイルオブジェクトハンドルに関連付けられている現在のキューにある Irp だけをキャンセルして完了する必要があります。 (ファイルオブジェクトへのポインターは、ドライバーの[**IO\_スタック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)の**FILEOBJECT**メンバー\_IRP の場所にあります)。これらのキューに登録された Irp を取り消した後、ドライバーはクリーンアップ IRP を完了し、i/o 状態ブロックの状態\_成功に設定します。

この要求の処理の詳細については、「 [DispatchCleanup ルーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchcleanup-routines)」を参照してください。

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
<td>Wdm (Wdm .h、Ntddk、または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IRP\_MJ\_閉じる**](irp-mj-close.md)

 

 




