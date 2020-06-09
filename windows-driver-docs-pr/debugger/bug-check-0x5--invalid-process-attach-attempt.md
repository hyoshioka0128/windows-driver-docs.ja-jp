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
ms.openlocfilehash: b74da3425eb501fc2ad485eac3b417f633239ff1
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534623"
---
# <a name="bug-check-0x5-invalid_process_attach_attempt"></a>バグチェック 0x5: \_ プロセス \_ アタッチ \_ 試行が無効です


無効な \_ プロセス \_ アタッチ \_ 試行のバグチェックには、0x00000005 の値が含まれています。 これは、通常、許可されていない状況でスレッドがプロセスにアタッチされたことを示します。 たとえば、スレッドが既にプロセスにアタッチされているときに**Keattachprocess**が呼び出された (無効な) 場合、または特定の関数から返されたスレッドがアタッチされた状態 (無効) である場合に、このバグチェックが発生する可能性があります。

このバグチェックは非常に頻繁に行われません。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="invalid_process_attach_attempt-parameters"></a>\_プロセスの \_ アタッチ \_ 試行パラメーターが無効です


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
<td align="left"><p>ターゲットプロセスのディスパッチャーオブジェクトへのポインター。スレッドが既にアタッチされている場合は、元のプロセスのオブジェクトへのポインター。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>現在のスレッドが現在アタッチされているプロセスのディスパッチャーオブジェクトへのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>スレッドの APC 状態インデックスの値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0以外の値は、DPC が現在のプロセッサで実行されていることを示します。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
このバグチェックは、ドライバーが**Keattachprocess**関数を呼び出し、スレッドが既に別のプロセスにアタッチされている場合に発生する可能性があります。 **Kestackattachprocess**関数を使用することをお勧めします。 現在のスレッドが既に別のプロセスにアタッチされている場合、 **Kestackattachprocess**関数は、現在のスレッドを新しいプロセスにアタッチする前に、現在の APC の状態を保存します。

 

 




