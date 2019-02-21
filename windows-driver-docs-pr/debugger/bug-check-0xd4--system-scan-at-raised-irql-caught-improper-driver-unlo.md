---
title: バグ チェック 0xD4 SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD
description: SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD のバグ チェックでは、0x000000D4 の値を持ちます。 これは、ドライバーがアンロードの前の保留中の操作キャンセルしなかったことを示します。
ms.assetid: 4c0e69d1-737c-4dd7-b52a-4cd5eeadcbb9
keywords:
- バグ チェック 0xD4 SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD
- SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 87c6fca5c369c86a3aa70a6e47468022c95d8149
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557859"
---
# <a name="bug-check-0xd4-systemscanatraisedirqlcaughtimproperdriverunload"></a>バグ チェック 0xD4 の。システム\_スキャン\_で\_発生\_IRQL\_例外が発生しました\_不適切な\_ドライバー\_アンロード


システム\_スキャン\_で\_発生\_IRQL\_例外が発生しました\_不適切な\_ドライバー\_アンロードのバグ チェックが 0x000000D4 の値を持ちます。 これは、ドライバーがアンロードの前の保留中の操作キャンセルしなかったことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="systemscanatraisedirqlcaughtimproperdriverunload-parameters"></a>システム\_スキャン\_で\_発生\_IRQL\_例外が発生しました\_不適切な\_ドライバー\_アンロード パラメーター


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
<td align="left"><p>参照されるメモリ</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>IRQL の参照時に</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>書き込み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>メモリ アドレス</p></td>
</tr>
</tbody>
</table>

 

その名前がブルー スクリーンに印刷され、場所のメモリに格納されているドライバーのエラーの原因が識別できる場合 (PUNICODE\_文字列) **KiBugCheckDriver**します。

<a name="cause"></a>原因
-----

このドライバーは、ルック アサイド リスト、Dpc、ワーカー スレッド、またはアンロードする前にこのようなその他の項目をキャンセルできませんでした。 その後、システムは、発生した IRQL でドライバーの以前の場所にアクセスしようとしました。

<a name="resolution"></a>解決方法
----------

デバッグを開始するには、カーネル デバッガーを使用して、スタック トレースを取得します。 エラーが発生したドライバーが指定されている場合は、Driver Verifier をアクティブ化し、このバグをレプリケートしようとしてください。

詳細については、Driver Verifier は、Windows ドライバー キットを参照してください。

 

 




