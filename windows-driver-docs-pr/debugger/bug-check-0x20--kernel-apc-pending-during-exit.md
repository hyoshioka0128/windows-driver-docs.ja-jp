---
title: バグ チェック 0x20 KERNEL_APC_PENDING_DURING_EXIT
description: KERNEL_APC_PENDING_DURING_EXIT のバグ チェックでは、0x00000020 の値を持ちます。 これは、非同期プロシージャ コール (APC) がまだされたことを示します。 保留中のスレッドが終了しました。
ms.assetid: 0ef7c2b2-0864-4206-b786-bac9df9cedc7
keywords:
- バグ チェック 0x20 KERNEL_APC_PENDING_DURING_EXIT
- KERNEL_APC_PENDING_DURING_EXIT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_APC_PENDING_DURING_EXIT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ecbb2142c27d4787c2f25d1cc634439ffe745851
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238771"
---
# <a name="bug-check-0x20-kernelapcpendingduringexit"></a>バグ チェック 0x20:カーネル\_APC\_PENDING\_に\_終了


カーネル\_APC\_PENDING\_に\_終了のバグ チェックが 0x00000020 の値を持ちます。 これは、非同期プロシージャ コール (APC) がまだされたことを示します。 保留中のスレッドが終了しました。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="kernelapcpendingduringexit-parameters"></a>カーネル\_APC\_PENDING\_に\_終了パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>保留中の終了時に検出された APC のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>スレッドの APC の無効化の数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>現在の IRQL</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

キーのデータ項目では、APC がスレッドの数 (パラメーター 2) を無効にします。 カウントが 0 以外の場合は、問題の原因が示されます。

APC の無効化カウントがデクリメントされますドライバーを呼び出すたびに**KeEnterCriticalRegion**、 **FsRtlEnterFileSystem**、または、ミュー テックスを取得します。

APC の無効化の数には、ドライバーを呼び出すたびがインクリメントされます**KeLeaveCriticalRegion**、 **KeReleaseMutex**、または**FsRtlExitFileSystem**します。

これらの呼び出しは、ペアで常にする必要があります、APC の無効化の数は、スレッドの終了時に、その 0 にする必要があります。 負の値は、ドライバーにそれらを再度有効にすることがなく APC 呼び出しが無効になっていることを示します。 正の値は、逆が true であることを示します。

これまでこのエラーが発生した場合は、特に異常であるか非標準のドライバー、マシンにインストールされているすべてのドライバーの非常に疑わしいあります。

この現在の IRQL (パラメーター 3) は、0 にする必要があります。 ない場合、ドライバーのキャンセル ルーチンが管理者特権での IRQL で返すことによってこのバグ チェック原因がある可能性があります。 この場合は、慎重に、クラッシュの時点で実行されている (および、何を埋めることでした) は何でしたをメモし、クラッシュ時にインストールされているドライバーのすべてに注意してください。 原因、ドライバーの重大なバグをここでは、通常、します。


## <a name="resolution"></a>解決方法
[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。
 

 




