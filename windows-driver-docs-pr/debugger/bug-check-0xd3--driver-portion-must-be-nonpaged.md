---
title: バグチェック 0xD3 DRIVER_PORTION_MUST_BE_NONPAGED
description: DRIVER_PORTION_MUST_BE_NONPAGED バグチェックの値は0x000000D3 です。 これは、システムが高すぎたプロセス IRQL でページング可能なメモリにアクセスしようとしたことを示します。
ms.assetid: 8b33dd20-9faa-4c02-96b7-89f55e69aeec
keywords:
- バグチェック 0xD3 DRIVER_PORTION_MUST_BE_NONPAGED
- DRIVER_PORTION_MUST_BE_NONPAGED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_PORTION_MUST_BE_NONPAGED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f6e2ee24a40f27a4e5142cce1cbdc754d29845b2
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534575"
---
# <a name="bug-check-0xd3-driver_portion_must_be_nonpaged"></a>バグチェック 0xD3: ドライバー \_ 部分 \_ \_ は、 \_ 非ページ化されている必要があります


ドライバー \_ の部分は、 \_ \_ 非ページ化さ \_ れたバグチェックの値が0x000000D3 である必要があります。 これは、システムが高すぎたプロセス IRQL でページング可能なメモリにアクセスしようとしたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="driver_portion_must_be_nonpaged-parameters"></a>ドライバー \_ 部分 \_ \_ は、 \_ 非ページパラメーターである必要があります


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
<td align="left"><p>参照時の IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>込ん</p>
<p><strong>1:</strong>企画</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>参照されたメモリのアドレス</p></td>
</tr>
</tbody>
</table>

 

エラーの原因となっているドライバーを識別できる場合は、その名前が青色の画面に出力され、メモリ内の場所 (PUNICODE \_ 文字列) **KiBugCheckDriver**に格納されます。

<a name="cause"></a>原因
-----

このバグチェックは通常、独自のコードまたはデータをページング可能としてマークしていないドライバーによって発生します。

<a name="resolution"></a>解像度
----------

デバッグを開始するには、カーネルデバッガーを使用してスタックトレースを取得します。この拡張機能で[**は、バグ**](-analyze.md)チェックに関する情報を表示し、根本原因を特定し、 [**Kb (スタックバックトレースの表示)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドを使用してスタックトレースを取得します。

 

 




