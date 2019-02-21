---
title: バグ チェック 0x74 BAD_SYSTEM_CONFIG_INFO
description: BAD_SYSTEM_CONFIG_INFO のバグ チェックでは、0x00000074 の値を持ちます。 このバグ チェックでは、レジストリにエラーがあることを示します。
ms.assetid: c59ddc44-d860-4fbb-a975-ae7226fdce86
keywords:
- バグ チェック 0x74 BAD_SYSTEM_CONFIG_INFO
- BAD_SYSTEM_CONFIG_INFO
ms.date: 08/17/2018
topic_type:
- apiref
api_name:
- BAD_SYSTEM_CONFIG_INFO
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a659f649ce7950b466b85499c27d08123cb5ce40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531567"
---
# <a name="bug-check-0x74-badsystemconfiginfo"></a>バグ チェック 0x74 の。不適切な\_システム\_CONFIG\_情報


不適切な\_システム\_CONFIG\_情報のバグ チェックが 0x00000074 の値を持ちます。 このバグ チェックでは、レジストリにエラーがあることを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="badsystemconfiginfo-parameters"></a>不適切な\_システム\_CONFIG\_情報パラメーター


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
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>NT ステータス値/コード (使用可能な場合)</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

不適切な\_システム\_CONFIG\_情報のバグ チェックは、システムのシステム ハイブが壊れている場合に発生します。 ただし、この破損は、ハイブの読み込み時に、ブート ローダーのチェック ハイブが破損していないため、可能性があります。

このバグ チェックは、いくつかの重要なレジストリ キーと値が存在しない場合にも発生します。 ユーザーが手動でレジストリを編集する場合、または、アプリケーションまたはサービスに、レジストリが破損している場合に、キーと値を不足していることがあります。

追加情報を参照してくださいパラメーター 4 で返された NT ステータス値を調べることができます[NTSTATUS 値](https://msdn.microsoft.com/library/cc704588.aspx)一覧についてはします。 

<a name="resolution"></a>解決方法
----------

セーフ モードで起動してみてくださいし、通常どおり、OS を再起動します。 再起動に問題が解決しない場合、レジストリの破損があまり広範囲にわたってします。 次の手順を実行してください。

-   システム復元ポイントがある場合は、以前の復元ポイントに復元してみてください。
-   お使いの PC をリセットします。
-   インストール メディアを使用して、復元またはお使いの PC をリセットします。
-   インストール メディアを使用して、Windows を再インストールします。

詳細については、次を参照してください。 [Windows 10 での回復オプション](https://windows.microsoft.com/windows-10/windows-10-recovery-options#)します。

 

 




