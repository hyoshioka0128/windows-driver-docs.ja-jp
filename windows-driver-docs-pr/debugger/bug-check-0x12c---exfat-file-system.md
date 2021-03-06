---
title: バグ チェック 0x12C EXFAT_FILE_SYSTEM
description: EXFAT_FILE_SYSTEM のバグ チェックでは 0x0000012C の値を持ちます。 このバグ チェックでは、拡張ファイル アロケーション テーブル (exFAT) のファイル システムで問題が発生したことを示します。
ms.assetid: f55bbe88-d96f-494f-b84b-eda7c4e6bdfc
keywords:
- バグ チェック 0x12C EXFAT_FILE_SYSTEM
- EXFAT_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- EXFAT_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9125cfe867d2898903fde5928764f158148d1ad6
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520646"
---
# <a name="bug-check-0x12c-exfatfilesystem"></a>バグ チェック 0x12C:EXFAT\_ファイル\_システム


EXFAT\_ファイル\_システムのバグ チェックでは 0x0000012C の値を持ちます。 このバグ チェックでは、拡張ファイル アロケーション テーブル (exFAT) のファイル システムで問題が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="exfatfilesystem-parameters"></a>EXFAT\_ファイル\_システム パラメーター


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
<td align="left"><p>ソース ファイルと行番号情報を指定します。 上位 16 ビット ("0 x"の後に最初の 4 つの 16 進数字) は、その識別子番号によってソース ファイルを決定します。 下位 16 ビットは、バグ チェックが発生したファイル内のソース行を決定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>場合<strong>FppExceptionFilter</strong>はスタックで、このパラメーターは例外レコードのアドレスを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>場合<strong>FppExceptionFilter</strong>はスタックで、このパラメーターはコンテキスト レコードのアドレスを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このバグ チェックは、その内部の計算がサポートできない状態と、続行するには、データ損失の大規模なリスクをもたらす最後の手段として、ファイル システムで発生します。 ファイル システムではこのバグ チェックことはありませんが、ディスク構造体が破損している、ディスク セクターは劣化し、またはメモリの割り当てが失敗した場合。 不良セクターによりバグ チェックでは、たとえば、カーネル コードでページ フォールトが発生したか、データと、メモリ マネージャーは、ページを読み取ることができません。 ただし、このバグ チェックでは、ファイル システム原因ではありません。

<a name="resolution"></a>解決方法
----------

**この問題をデバッグします。** 使用して、 [ **.cxr (コンテキスト レコードの表示)** ](-cxr--display-context-record-.md)と共にパラメーター 3 では、コマンドを使用して[ **kb (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)します。

 

 




