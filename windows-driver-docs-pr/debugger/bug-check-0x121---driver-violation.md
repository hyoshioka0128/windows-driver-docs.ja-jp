---
title: バグチェック 0x121 DRIVER_VIOLATION
description: DRIVER_VIOLATION のバグチェックには、0x00000121 という値が指定されています。 このバグチェックは、ドライバーによって違反が発生したことを示します。
ms.assetid: 4a5d1d84-a958-45a6-9511-b5b4ecd4c067
keywords:
- バグチェック 0x121 DRIVER_VIOLATION
- DRIVER_VIOLATION
ms.date: 10/08/2019
topic_type:
- apiref
api_name:
- DRIVER_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 83cf10eb1350145369abcbb64821dda0b6d697fd
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534845"
---
# <a name="bug-check-0x121-driver_violation"></a>バグチェック 0x121: ドライバー \_ 違反

ドライバー違反のバグチェックには、 \_ 0x00000121 という値が指定されています。 このバグチェックは、ドライバーによって違反が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="driver_violation-parameters"></a>ドライバー \_ 違反パラメーター

パラメーター1は違反の種類を示します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>現在の IRQL。</p></td>
<td align="left"><p>必要な IRQL。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ドライバーは、特定の IRQL でのみ呼び出すことができる関数を呼び出しました。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

カーネルデバッガーを使用して呼び出し履歴を表示し、違反の原因となったドライバーの名前を確認します。 [デバッグの[**分析**](-analyze.md)] 拡張にはバグチェックに関する情報が表示され、根本原因の特定に役立つことがあります。その後、いずれかの[**k (スタックバックトレース)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドを入力して呼び出し履歴を表示します。
