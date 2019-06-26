---
title: KsTimedDeviceCallbacks ルール)
description: KsTimedDeviceCallbacks ルールでは、カーネル ストリーミング (KS) ミニポート ドライバーが 500 ミリ秒以内でデバイスのコールバック関数から返すことを指定します。
ms.assetid: 05393761-9018-4DAA-B8B5-EFEBBCDAB955
ms.date: 05/21/2018
keywords:
- KsTimedDeviceCallbacks ルール)
topic_type:
- apiref
api_name:
- KsTimedDeviceCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f41c5bd8f910f9fd2e508710ac94dd78ac1d415d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392723"
---
# <a name="kstimeddevicecallbacks-rule-"></a>KsTimedDeviceCallbacks ルール)


KsTimedDeviceCallbacks ルールでは、カーネル ストリーミング (KS) ミニポート ドライバーが 500 ミリ秒以内でデバイスのコールバック関数から返すことを指定します。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00082002) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>このルールを確認するには、コマンド プロンプト ウィンドウを開きます。 Driver Verifier のコマンドを入力し、指定<strong>/domain ks</strong>します。</p>
<p>次に、例を示します。</p>
<p><strong>verifier /domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>詳細については、次を参照してください。 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>します。</p></td>
</tr>
</tbody>
</table>

 

<a name="see-also"></a>関連項目
--------

[ロックおよびロック解除の Stream ポインター](https://docs.microsoft.com/windows-hardware/drivers/stream/locking-and-unlocking-stream-pointers)
 

 





