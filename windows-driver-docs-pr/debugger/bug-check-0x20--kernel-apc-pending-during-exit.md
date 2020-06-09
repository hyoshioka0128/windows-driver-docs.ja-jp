---
title: バグチェック 0x20 KERNEL_APC_PENDING_DURING_EXIT
description: KERNEL_APC_PENDING_DURING_EXIT バグチェックの値は0x00000020 です。 これは、スレッドが終了したときに、非同期プロシージャコール (APC) がまだ保留されていたことを示します。
ms.assetid: 0ef7c2b2-0864-4206-b786-bac9df9cedc7
keywords:
- バグチェック 0x20 KERNEL_APC_PENDING_DURING_EXIT
- KERNEL_APC_PENDING_DURING_EXIT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_APC_PENDING_DURING_EXIT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4b919df6dd569d53c1a0413a8608bc4dd1709851
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534827"
---
# <a name="bug-check-0x20-kernel_apc_pending_during_exit"></a>バグチェック 0x20: \_ \_ \_ 終了中にカーネル APC が保留中です \_


\_ \_ 終了バグチェック中に保留中のカーネル APC の \_ \_ 値は0x00000020 です。 これは、スレッドが終了したときに、非同期プロシージャコール (APC) がまだ保留されていたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="kernel_apc_pending_during_exit-parameters"></a>\_ \_ \_ 終了パラメーター中に保留中のカーネル APC \_


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
<td align="left"><p>終了中に保留された APC のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>スレッドの APC の無効化カウント</p></td>
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

キーデータ項目は、スレッドの APC disable count (パラメーター 2) です。 カウントが0以外の場合は、問題の原因を示します。

APC の disable count は、ドライバーが**KeEnterCriticalRegion**、 **fsrtlenterfilesystem**を呼び出すたび、またはミューテックスを取得するたびにデクリメントされます。

APC disable count は、ドライバーが**KeLeaveCriticalRegion**、 **KeReleaseMutex**、または**fsrtlexitfilesystem**を呼び出すたびに増分されます。

これらの呼び出しは常にペアになっている必要があるため、スレッドの終了時には、APC の disable count を0にする必要があります。 負の値は、ドライバーが再度有効にすることなく、APC の呼び出しを無効にしたことを示します。 正の値は、反転が true であることを示します。

このエラーが発生する場合は、コンピューターにインストールされているすべてのドライバー (特に異常なドライバーまたは非標準ドライバー) について非常に疑わしいことを確認してください。

この現在の IRQL (パラメーター 3) は0である必要があります。 そうでない場合は、ドライバーの取り消しルーチンによって、管理者特権での IRQL が返され、このバグチェックが発生する可能性があります。 この場合は、クラッシュ時に実行されていたもの (および終了したもの) を注意深くメモし、クラッシュ時にインストールされているすべてのドライバーをメモしておきます。 この場合の原因は、通常、ドライバーの重大なバグです。


## <a name="resolution"></a>解像度
! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
 

 




