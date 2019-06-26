---
title: バグ チェック 0x92 UP_DRIVER_ON_MP_SYSTEM
description: UP_DRIVER_ON_MP_SYSTEM のバグ チェックでは、0x00000092 の値を持ちます。 このバグ チェックでは、マルチプロセッサ システムでユニプロセッサ専用のドライバーが読み込まれたことを示します。
ms.assetid: 1e26c7b1-bfa5-4a32-a483-5ce8179ac6b7
keywords:
- バグ チェック 0x92 UP_DRIVER_ON_MP_SYSTEM
- UP_DRIVER_ON_MP_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- UP_DRIVER_ON_MP_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: caa3247387e2fa391b1feeac127f7f3e9a19877a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367284"
---
# <a name="bug-check-0x92-updriveronmpsystem"></a>バグ チェック 0x92:\_ドライバー\_ON\_MP\_システム


上向き\_ドライバー\_ON\_MP\_システムのバグ チェックが 0x00000092 の値を持ちます。 このバグ チェックでは、マルチプロセッサ システムでユニプロセッサ専用のドライバーが読み込まれたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="updriveronmpsystem-parameters"></a>\_ドライバー\_ON\_MP\_システム パラメーター


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
<td align="left"><p>ドライバーのベース アドレス</p></td>
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

ユニプロセッサ コンピューターでのみ動作するコンパイルされたドライバーが読み込まれたが、Microsoft Windows オペレーティング システムが 1 つ以上のアクティブなプロセッサを搭載したマルチプロセッサ システムで実行されています。

 
## <a name="resolution"></a>解決方法
[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。




