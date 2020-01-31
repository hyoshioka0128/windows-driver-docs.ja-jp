---
title: バグチェック 0x5 INVALID_PROCESS_ATTACH_ATTEMPT
description: INVALID_PROCESS_ATTACH_ATTEMPT バグチェックの値は0x00000005 です。
ms.assetid: 72efb88f-1bf7-4552-b44e-4ecb04754b7d
keywords:
- バグチェック 0x5 INVALID_PROCESS_ATTACH_ATTEMPT
- INVALID_PROCESS_ATTACH_ATTEMPT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_PROCESS_ATTACH_ATTEMPT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 663aabde692a1c0e27347914f589c328aa9113c5
ms.sourcegitcommit: 70c8e83900015eaea013fb742e5e137cfd08ca98
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2020
ms.locfileid: "76885357"
---
# <a name="bug-check-0x5-invalid_process_attach_attempt"></a>バグチェック 0x5: 無効な\_プロセス\_アタッチ\_試行


無効な\_プロセス\_アタッチ\_試行のバグチェックの値が0x00000005 になっています。 これは、通常、許可されていない状況でスレッドがプロセスにアタッチされたことを示します。 たとえば、スレッドが既にプロセスにアタッチされているときに**Keattachprocess**が呼び出された (無効な) 場合、または特定の関数から返されたスレッドがアタッチされた状態 (無効) である場合に、このバグチェックが発生する可能性があります。

このバグチェックは非常に頻繁に行われません。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="invalid_process_attach_attempt-parameters"></a>無効な\_プロセス\_\_試行パラメーターをアタッチしています


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
<td align="left"><p>1 で保護されたプロセスとして起動されました</p></td>
<td align="left"><p>ターゲットプロセスのディスパッチャーオブジェクトへのポインター。スレッドが既にアタッチされている場合は、元のプロセスのオブジェクトへのポインター。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2 で保護されたプロセスとして起動されました</p></td>
<td align="left"><p>現在のスレッドが現在アタッチされているプロセスのディスパッチャーオブジェクトへのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3 で保護されたプロセスとして起動されました</p></td>
<td align="left"><p>スレッドの APC 状態インデックスの値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
<td align="left"><p>0以外の値は、DPC が現在のプロセッサで実行されていることを示します。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
このバグチェックは、ドライバーが**Keattachprocess**関数を呼び出し、スレッドが既に別のプロセスにアタッチされている場合に発生する可能性があります。 **Kestackattachprocess**関数を使用することをお勧めします。 現在のスレッドが既に別のプロセスにアタッチされている場合、 **Kestackattachprocess**関数は、現在のスレッドを新しいプロセスにアタッチする前に、現在の APC の状態を保存します。

 

 




