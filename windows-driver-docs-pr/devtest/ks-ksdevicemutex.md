---
title: KsDeviceMutex ルール)
description: KsDeviceMutex ルールでは、ミニポート ドライバーをストリーミング カーネルが正しい順序で、KsAcquireDevice と KsReleaseDevice を使用することを指定します。 つまり、KsAcquireDevice、呼び出すたびには、KsReleaseDevice に対応する呼び出しが必要です。
ms.assetid: 6F69B273-6780-4A01-8266-2B056E4F2C84
ms.date: 05/21/2018
keywords:
- KsDeviceMutex ルール)
topic_type:
- apiref
api_name:
- KsDeviceMutex
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 809a997167904da95814b2b068af6c9e3ca73fd5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559339"
---
# <a name="ksdevicemutex-rule-"></a>KsDeviceMutex ルール)


**KsDeviceMutex**ルールでは、ミニポート ドライバーをストリーミング カーネルが使用するように指定[ **KsAcquireDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560911)と[ **KsReleaseDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff566783)正しい順序で。 すべての呼び出しには、 **KsAcquireDevice**に対応する呼び出しがあります。 **KsReleaseDevice**します。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00081001) |

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
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 

 





