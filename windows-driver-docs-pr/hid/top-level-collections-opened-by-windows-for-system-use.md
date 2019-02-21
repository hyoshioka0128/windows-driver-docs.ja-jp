---
title: システムの使用、Windows によって開かれた最上位のコレクション
description: システムの使用、Windows によって開かれた最上位のコレクション
ms.assetid: e489ce46-379e-4ba9-a0e3-5848b1f4a17b
keywords:
- WDK を非表示に最上位のコレクション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80f4c7794f4dada8b79d887a7b334539e40771f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551036"
---
# <a name="top-level-collections-opened-by-windows-for-system-use"></a>システムの使用、Windows によって開かれた最上位のコレクション





Windows は、次を開く[最上位のコレクション](top-level-collections.md)システムを使用します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>デバイスの種類</th>
<th>使用状況 ページ</th>
<th>使用状況 ID</th>
<th>Windows クライアント</th>
<th>アクセス モード</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ポインター</p></td>
<td><p>0x01</p></td>
<td><p>0x01</p></td>
<td><p>Win32 サブシステム</p></td>
<td><p>［排他］</p></td>
</tr>
<tr class="even">
<td><p>マウス</p></td>
<td><p>0x01</p></td>
<td><p>0x02</p></td>
<td><p>Win32 サブシステム</p></td>
<td><p>［排他］</p></td>
</tr>
<tr class="odd">
<td><p>ジョイスティック</p></td>
<td><p>0x01</p></td>
<td><p>0x04</p></td>
<td><p>DirectInput</p></td>
<td><p>共有</p></td>
</tr>
<tr class="even">
<td><p>ゲーム パッド</p></td>
<td><p>0x01</p></td>
<td><p>0x05</p></td>
<td><p>DirectInput</p></td>
<td><p>共有</p></td>
</tr>
<tr class="odd">
<td><p>キーボード</p></td>
<td><p>0x01</p></td>
<td><p>0x06</p></td>
<td><p>Win32 サブシステム</p></td>
<td><p>［排他］</p></td>
</tr>
<tr class="even">
<td><p>キーパッド</p></td>
<td><p>0x01</p></td>
<td><p>0x07</p></td>
<td><p>Win32 サブシステム</p></td>
<td><p>［排他］</p></td>
</tr>
<tr class="odd">
<td><p>システム コントロール</p></td>
<td><p>0x01</p></td>
<td><p>0x80</p></td>
<td><p>Win32 サブシステム</p></td>
<td><p>共有</p></td>
</tr>
<tr class="even">
<td><p>コンシューマー オーディオ コントロール</p></td>
<td><p>0x0C</p></td>
<td><p>0x01</p></td>
<td><p>Windows 2000 および Microsoft Windows xp (SVC ホスト サービスの 1 つ) hidserv.dll hidserv.exe</p></td>
<td><p>共有</p></td>
</tr>
</tbody>
</table>

 

 

 




