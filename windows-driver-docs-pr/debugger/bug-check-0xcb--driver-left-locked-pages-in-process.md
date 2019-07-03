---
title: バグ チェック 0xCB DRIVER_LEFT_LOCKED_PAGES_IN_PROCESS
description: DRIVER_LEFT_LOCKED_PAGES_IN_PROCESS のバグ チェックでは、0x000000CB の値を持ちます。 これは、I/O 操作の後にロックされたページを解放するドライバー、または I/O マネージャーが失敗したことを示します。
ms.assetid: e97d114e-c6f1-44f1-a2ad-bfa8d03dc3c7
keywords:
- バグ チェック 0xCB DRIVER_LEFT_LOCKED_PAGES_IN_PROCESS
- DRIVER_LEFT_LOCKED_PAGES_IN_PROCESS
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_LEFT_LOCKED_PAGES_IN_PROCESS
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5885aa1b0269e87304ca7c534958e30ecf4dba00
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518907"
---
# <a name="bug-check-0xcb-driverleftlockedpagesinprocess"></a>バグ チェック 0xCB:ドライバー\_左\_ロック\_ページ\_IN\_プロセス


ドライバー\_左\_ロック\_ページ\_IN\_プロセスのバグ チェックが 0x000000CB の値を持ちます。 これは、I/O 操作の後にロックされたページを解放するドライバー、または I/O マネージャーが失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="driverleftlockedpagesinprocess-parameters"></a>ドライバー\_左\_ロック\_ページ\_IN\_プロセス パラメーター


メッセージに表示する 4 つのパラメーターは、2 つの可能性のある意味でことができます。

ドライバーにこれらのページがロックされている場合、パラメーターは次の意味を持ちます。

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
<td align="left"><p>ページをロックするドライバーのアドレスを呼び出す</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>呼び出し元のページをロックしたドライバーの呼び出し元のアドレス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>ロックされたページを含む MDL のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>ロックされたページ数</p></td>
</tr>
</tbody>
</table>

 

その名前がブルー スクリーンに印刷され、場所のメモリに格納されているドライバーのエラーの原因が識別できる場合 (PUNICODE\_文字列) **KiBugCheckDriver**します。

I/O マネージャーにこれらのページがロックされている場合、パラメーターは次の意味を持ちます。

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
<td align="left"><p>IRP の送付先となるスタックの最上位のドライバーのディスパッチ ルーチンのアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>IRP の送付先となるスタックの最上位のドライバーのデバイス オブジェクトのアドレス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>ロックされたページを含む MDL のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>ロックされたページ数</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

場合にのみ、このバグ チェックが発行されたレジストリ値 **\\ \\HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\セッション マネージャー\\メモリ管理\\TrackLockedPages** DWORD 1 にします。 この値が設定されていない場合に、システムはあまり有益な発行[**バグ チェック 0x76** ](bug-check-0x76--process-has-locked-pages.md) (プロセス\_HAS\_ロック\_ページ)。

以降 Windows Vista では、このバグ チェックもを発行できる Driver Verifier プールの追跡オプションを有効にします。

 

 




