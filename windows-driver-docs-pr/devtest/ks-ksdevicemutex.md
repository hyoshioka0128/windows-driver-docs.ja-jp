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
ms.openlocfilehash: 37d3ae4f5c59c1cbaf3cd1717a591121cf5d9710
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918140"
---
# <a name="ksdevicemutex-rule-"></a>KsDeviceMutex rule ()


**KsDeviceMutex**ルールは、カーネルストリーミングミニポートドライバーが[**KsAcquireDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksacquiredevice)と[**ksreleasedevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksreleasedevice)を正しい順序で使用することを指定します。 つまり、 **KsAcquireDevice**を呼び出すたびに、対応する**ksk releasedevice**への呼び出しが必要になります。

**ドライバーモデル: KS**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツールで \_ 検出された \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00081001) |

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
<p>たとえば、次のように入力します。</p>
<p><strong>verifier/domain ks</strong> [<em>オプション</em>] <strong>/driver</strong> <em> &lt; ドライバー &gt; </em>の設定</p>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 

 





