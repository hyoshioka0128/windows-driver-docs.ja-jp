---
title: バグチェック 0x92 UP_DRIVER_ON_MP_SYSTEM
description: UP_DRIVER_ON_MP_SYSTEM バグチェックの値は0x00000092 です。 このバグチェックは、マルチプロセッサシステムにユニプロセッサ専用のドライバーが読み込まれたことを示します。
ms.assetid: 1e26c7b1-bfa5-4a32-a483-5ce8179ac6b7
keywords:
- バグチェック 0x92 UP_DRIVER_ON_MP_SYSTEM
- UP_DRIVER_ON_MP_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- UP_DRIVER_ON_MP_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e1728ae9a95a4cddc65bf50694d3e6cbe414eaa7
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534581"
---
# <a name="bug-check-0x92-up_driver_on_mp_system"></a>バグチェック 0x92: \_ \_ \_ MP \_ システムの UP DRIVER


\_ \_ \_ MP システムバグチェックの UP DRIVER の \_ 値は、0x00000092 です。 このバグチェックは、マルチプロセッサシステムにユニプロセッサ専用のドライバーが読み込まれたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="up_driver_on_mp_system-parameters"></a>\_ \_ \_ MP \_ システムパラメーターでの UP DRIVER


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
<td align="left"><p>ドライバーのベースアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

ユニプロセッサコンピューターでのみ動作するようにコンパイルされたドライバーが読み込まれましたが、Microsoft Windows オペレーティングシステムが複数のアクティブなプロセッサを搭載したマルチプロセッサシステムで実行されています。

 
## <a name="resolution"></a>解像度
! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。




