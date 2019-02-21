---
title: バグ チェック 0xBC NETWORK_BOOT_DUPLICATE_ADDRESS
description: NETWORK_BOOT_DUPLICATE_ADDRESS のバグ チェックでは、0x000000BC の値を持ちます。 これは、ネットワークから起動中にこのコンピューターに重複する IP アドレスが割り当てられたことを示します。
ms.assetid: 54c45e73-7054-4dba-abe4-91f5f5a064a4
keywords:
- バグ チェック 0xBC NETWORK_BOOT_DUPLICATE_ADDRESS
- NETWORK_BOOT_DUPLICATE_ADDRESS
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- NETWORK_BOOT_DUPLICATE_ADDRESS
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 57e46a09a4a95f2ae5bee8c73c903f035fa6ccf2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552342"
---
# <a name="bug-check-0xbc-networkbootduplicateaddress"></a>バグ チェック 0xBC の。ネットワーク\_ブート\_複製\_アドレス


ネットワーク\_ブート\_複製\_アドレス バグ チェックが 0x000000BC の値を持ちます。 これは、ネットワークから起動中にこのコンピューターに重複する IP アドレスが割り当てられたことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="networkbootduplicateaddress-parameters"></a>ネットワーク\_ブート\_複製\_アドレス パラメーター


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
<td align="left"><p>IP アドレスは、DWORD として表示されます。 フォームのアドレス<em>aa.bb.cc.dd</em> 0xDDCCBBAA として表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>その他のマシンのハードウェアのアドレス。 (イーサネット接続では、次の注を参照してください)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>その他のマシンのハードウェアのアドレス。 (イーサネット接続では、次の注を参照してください)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>その他のマシンのハードウェアのアドレス。 (イーサネット接続では、この 0 になります。)</p></td>
</tr>
</tbody>
</table>

 

**注**  パラメーター 4 の場合に 0 に等しい、これは、イーサネット接続を示します。 その場合は、MAC アドレスは、パラメーター 2 と 3 のパラメーターに格納します。 フォームのイーサネットの MAC アドレス*aa-bb-cc-dd-ee-ff* 0xAABBCCDD、等しくパラメーター 2 と等しく 0xEEFF0000 パラメーター 3 になります。

 

<a name="cause"></a>原因
-----

このエラーは、ARP その IP アドレスを TCP/IP が送信されると、応答が重複する IP アドレスを示す別のコンピューターからを行うことを示します。

ネットワークから Windows を起動すると、ときに致命的なエラーになります。

 

 




