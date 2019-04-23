---
title: バグ チェック 0x27 RDR_FILE_SYSTEM
description: RDR_FILE_SYSTEM のバグ チェックでは、0x00000027 の値を持ちます。 これは、SMB リダイレクターのファイル システムで問題が発生したことを示します。
ms.assetid: 1294022d-7281-45d2-89c8-40d11ce202f0
keywords:
- バグ チェック 0x27 RDR_FILE_SYSTEM
- RDR_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- RDR_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: faed326e57c284b4c1bad5dc070386bb4510465a
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902384"
---
# <a name="bug-check-0x27-rdrfilesystem"></a>バグ チェック 0x27:RDR\_ファイル\_システム


RDR\_ファイル\_システムのバグ チェックが 0x00000027 の値を持ちます。 これは、SMB リダイレクターのファイル システムで問題が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="rdrfilesystem-parameters"></a>RDR\_ファイル\_システム パラメーター


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
<td align="left"><p>上位 16 ビット ("0 x"の後に最初の 4 つの 16 進数字) は、問題の種類を識別します。 有効な値は次のとおりです。</p>
<p>0xCA550000 RDBSS_BUG_CHECK_CACHESUP</p>
<p>0xC1EE0000 RDBSS_BUG_CHECK_CLEANUP</p>
<p>0xC10E0000 RDBSS_BUG_CHECK_CLOSE</p>
<p>0xBAAD0000 RDBSS_BUG_CHECK_NTEXCEPT</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>場合<strong>RxExceptionFilter</strong>はスタックで、このパラメーターは例外レコードのアドレスを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>場合<strong>RxExceptionFilter</strong>はスタックで、このパラメーターはコンテキスト レコードのアドレスを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このバグ チェックの 1 つの考えられる原因は、非ページ プール メモリの不足です。 非ページ プール メモリは完全になくなると、このエラーは、システムを停止できます。 ただし、インデックス作成のプロセス中に使用可能な非ページ プール メモリの量が非常に低い場合別のカーネル モード ドライバーを非ページ プール メモリを必要とすることができますもこのエラーをトリガーします。

<a name="resolution"></a>解決方法
----------

**この問題をデバッグします。** 使用して、 [ **.cxr (コンテキスト レコードの表示)** ](-cxr--display-context-record-.md)パラメーター 3 では、コマンドを使用して[ **kb (Display Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)します。

**非ページ プール メモリの枯渇問題を解決するには。** コンピューターに新しい物理メモリを追加します。 これにより、カーネルで使用できる非ページ プール メモリの量が増加します。

 

 




