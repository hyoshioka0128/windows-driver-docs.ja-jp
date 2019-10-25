---
title: KsDeviceMutex rule ()
description: KsDeviceMutex ルールは、カーネルストリーミングミニポートドライバーが KsAcquireDevice と KsReleaseDevice を正しい順序で使用することを指定します。 つまり、KsAcquireDevice を呼び出すたびに、対応する Ksk Releasedevice への呼び出しが必要になります。
ms.assetid: 6F69B273-6780-4A01-8266-2B056E4F2C84
ms.date: 05/21/2018
keywords:
- KsDeviceMutex rule ()
topic_type:
- apiref
api_name:
- KsDeviceMutex
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 244ade2d455ea1ece880b16e07c3b8b9e6f0c2a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840133"
---
# <a name="ksdevicemutex-rule-"></a>KsDeviceMutex rule ()


**KsDeviceMutex**ルールは、カーネルストリーミングミニポートドライバーが[**KsAcquireDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksacquiredevice)と[**ksreleasedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksreleasedevice)を正しい順序で使用することを指定します。 つまり、 **KsAcquireDevice**を呼び出すたびに、対応する**ksk releasedevice**への呼び出しが必要になります。

|              |     |
|--------------|-----|
| ドライバー モデル | KS  |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00081001) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>この規則を確認するには、コマンドプロンプトウィンドウを開きます。 ドライバー検証ツールコマンドを入力し、「 <strong>/domain ks</strong>」と指定します。</p>
<p>次に、例を示します。</p>
<p><strong>verifier/domain ks</strong> [<em>オプション</em>] <strong>/driver</strong> <em>&lt;ドライバー&gt;</em></p>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 

 





