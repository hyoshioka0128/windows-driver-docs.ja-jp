---
title: バグ チェック 0 xdb DRIVER_CORRUPTED_SYSPTES
description: DRIVER_CORRUPTED_SYSPTES のバグ チェックでは、0x000000DB の値を持ちます。 これは、おそらくシステム Pte の破損により、無効な IRQL でメモリにアクセスしようとすることを示します。
ms.assetid: f21a7582-c665-4677-851b-702888d9fe13
keywords:
- バグ チェック 0 xdb DRIVER_CORRUPTED_SYSPTES
- DRIVER_CORRUPTED_SYSPTES
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_CORRUPTED_SYSPTES
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c8a989bc200a5bf41571028310928a3ca2baa911
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238637"
---
# <a name="bug-check-0xdb-drivercorruptedsysptes"></a>バグ チェック 0xDB:ドライバー\_破損した\_SYSPTES


ドライバー\_破損した\_SYSPTES バグ チェックが 0x000000DB の値を持ちます。 これは、おそらくシステム Pte の破損により、無効な IRQL でメモリにアクセスしようとすることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="drivercorruptedsysptes-parameters"></a>ドライバー\_破損した\_SYSPTES パラメーター


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
<td align="left"><p>参照されるメモリ</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>書き込み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>メモリを参照するコード内のアドレスします。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

ドライバーのページング可能な (または完全に無効な) のメモリにもアクセスしようとした IRQL を高くします。 このバグ チェックは、システム Pte が破損しているドライバーによってほぼ常に発生します。

<a name="resolution"></a>解決方法
----------

このバグ チェックが発生した場合は、レジストリを編集して、原因を検出できます。  **\\ \\HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\セッション マネージャー\\メモリ管理**のレジストリ キーを作成または編集、 **TrackPtes**値に設定して、DWORD 3 に等しく設定します。 再起動します。 システムは、スタック トレースを保存し、システム、ドライバーは、同じエラーをコミットする場合は、発行[**バグ チェック 0 xda** ](bug-check-0xda--system-pte-misuse.md) (システム\_PTE\_誤用)。 スタック トレースは、エラーの原因となったドライバーを識別します。

 

 




