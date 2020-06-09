---
title: バグチェック 0x51 REGISTRY_ERROR
description: REGISTRY_ERROR バグチェックの値は0x00000051 です。 これは、重大なレジストリエラーが発生したことを示します。
ms.assetid: 286e462f-e4d4-408f-91ad-3e20336e2025
keywords:
- バグチェック 0x51 REGISTRY_ERROR
- REGISTRY_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- REGISTRY_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4a20d14feff30fbf99cf61977d3c26fdd22fdfbd
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534621"
---
# <a name="bug-check-0x51-registry_error"></a>バグチェック 0x51: レジストリ \_ エラー


レジストリ \_ エラーのバグチェックには、0x00000051 の値が含まれています。 これは、重大なレジストリエラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="registry_error-parameters"></a>レジストリの \_ エラーパラメーター


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
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>Hive へのポインター (使用可能な場合)</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>Hive が破損している場合は、 <strong>Hvcheckhive</strong>のリターンコード (使用可能な場合)</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

レジストリで問題が発生しました。 カーネルデバッガーが使用可能な場合は、スタックトレースを取得します。この拡張機能は、バグチェックに関する情報を表示[**し、根本**](-analyze.md)原因を特定するのに非常に役立ちます。その後、 [**k (スタックバックトレースの表示)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドのいずれかを入力して、呼び出し履歴を表示します。

このエラーは、ファイルの1つを読み取ろうとしているときに、レジストリで i/o エラーが発生したことを示している可能性があります。 これは、ハードウェアの問題またはファイルシステムの破損によって発生する可能性があります。

また、更新操作の失敗によっても発生することがあります。これは、セキュリティシステムによってのみ使用され、リソースの制限が発生した場合にのみ使用されます。

 

 




