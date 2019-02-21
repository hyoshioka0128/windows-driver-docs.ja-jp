---
title: バグ チェック 0xC0000218 STATUS_CANNOT_LOAD_REGISTRY_FILE
description: STATUS_CANNOT_LOAD_REGISTRY_FILE のバグ チェックでは、0xC0000218 の値を持ちます。 これは、レジストリ ファイルが読み込めなかったことを示します。
ms.assetid: cdcf68fa-8beb-4e21-bc6b-7a9f4c6e9e80
keywords:
- バグ チェック 0xC0000218 STATUS_CANNOT_LOAD_REGISTRY_FILE
- STATUS_CANNOT_LOAD_REGISTRY_FILE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- STATUS_CANNOT_LOAD_REGISTRY_FILE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8876d3a3503008aec28ab33006ab3fdc91e5b336
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552191"
---
# <a name="bug-check-0xc0000218-statuscannotloadregistryfile"></a>バグ チェック 0xC0000218 の。ステータス\_できない\_ロード\_レジストリ\_ファイル


ステータス\_できない\_ロード\_レジストリ\_ファイル バグ チェックが 0xC0000218 の値を持ちます。 これは、レジストリ ファイルが読み込めなかったことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="statuscannotloadregistryfile-parameters"></a>ステータス\_できない\_ロード\_レジストリ\_ファイル パラメーター


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
<td align="left"><p>読み込まれていないレジストリ ハイブの名前のアドレス。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0 (予約済み)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0 (予約済み)</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0 (予約済み)</p></td>
</tr>
</tbody>
</table>

 

このバグ チェックでは、わかりやすいテキスト メッセージが表示されます。 破損したファイルの名前は、メッセージの一部として表示されます。

<a name="cause"></a>原因
-----

このエラーは、必要なレジストリ ハイブ ファイルを読み込むことができない場合に発生します。 通常は、ファイルが壊れているかが不足しているを意味します。

まれに、メモリ内のレジストリのイメージが破損しているドライバーか、このリージョンでメモリ エラーに、このエラーが発生することができます。

<a name="resolution"></a>解決方法
----------

オペレーティング システムによって提供されるスタートアップ回復メカニズム (スタートアップ修復、回復コンソール、または緊急回復ディスクなど) を使用してください。 問題が見つからないか壊れているレジストリ ファイルの場合は、通常は問題を解決します。

 

 




