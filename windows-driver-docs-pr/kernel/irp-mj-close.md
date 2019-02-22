---
title: IRP_MJ_CLOSE
description: すべてのドライバーには、ドライバーがデバイスを無効またはシステムを停止せずに、マシンから削除できませんのような例外の DispatchClose ルーチンで閉じる要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 109819a8-3787-448d-a766-5d53dbcf55f4
keywords:
- IRP_MJ_CLOSE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 46dcf7742a7c57527dd6e3206890c263e493ccd5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528305"
---
# <a name="irpmjclose"></a>IRP\_MJ\_閉じる


すべてのドライバーで閉じる要求を処理する必要があります、 [ *DispatchClose* ](separate-dispatchcreate-and-dispatchclose-routines.md)ルーチン、可能性のある例外のドライバーがデバイスを無効またはシステムを停止せずに、マシンから削除できません. デバイスを保持するシステムのページング ファイル ディスク ドライバーは、このようなドライバーの例を示します。 このようなデバイスのドライバーもできないことアンロード動的に注意してください。

<a name="when-sent"></a>送信時
---------

この要求の受信は、ターゲット デバイス オブジェクトに関連付けられているファイル オブジェクトの最後のハンドルが閉じられたされ解放されていることを示します。 すべての未処理 I/O 要求を完了またはキャンセルされています。

## <a name="input-parameters"></a>入力パラメーター


なし

## <a name="output-parameters"></a>出力パラメーター


なし

<a name="operation"></a>操作
---------

ステータス設定だけで多くのデバイスとドライバーの中間\_I/O ステータスに成功 IRP のブロックし、閉じる要求を完了します。 ただし、特定のドライバーは終了要求の受信時に、ドライバーの設計によって異なります。 一般に、ドライバーがかかるの受信時に任意のアクションを取り消す必要があります、 [ **IRP\_MJ\_作成**](irp-mj-create.md)要求。 デバイス オブジェクトを持つは排他的で、シリアル ドライバーなどのデバイス ドライバーは、終了要求の受信時にハードウェアもリセットできます。

**IRP\_MJ\_閉じる**要求は、必ずしもファイル オブジェクトのハンドルを終了したプロセスのコンテキストでは送信されません。 場合は、ドライバーはドライバーが以前ロックされているか、マップされるユーザー メモリなどのプロセスに固有のリソースを解放する必要がありますが行う必要がありますへの応答、 [ **IRP\_MJ\_クリーンアップ**](irp-mj-cleanup.md)要求。

**IRP\_MJ\_閉じる**パッシブで常に要求が送信される\_レベル。

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

[*DispatchClose*](separate-dispatchcreate-and-dispatchclose-routines.md)

[**IRP\_MJ\_クリーンアップ**](irp-mj-cleanup.md)

[**IRP\_MJ\_CREATE**](irp-mj-create.md)

 

 




