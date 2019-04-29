---
title: Windows によって開かれる最上位のコレクション (システムで使用)
description: Windows によって開かれる最上位のコレクション (システムで使用)
ms.assetid: e489ce46-379e-4ba9-a0e3-5848b1f4a17b
keywords:
- WDK を非表示に最上位のコレクション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80f4c7794f4dada8b79d887a7b334539e40771f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384355"
---
# <a name="top-level-collections-opened-by-windows-for-system-use"></a>Windows によって開かれる最上位のコレクション (システムで使用)





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

 

 

 




