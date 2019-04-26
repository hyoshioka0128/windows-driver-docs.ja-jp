---
title: SO_BROADCAST
description: SO_BROADCAST
ms.assetid: 24b93d4e-461d-44c3-b721-85cf41a1680a
ms.date: 08/08/2017
keywords: -:So_broadcast ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: afa77d7a6ef19f0ea47f1f1787216698aff9f137
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342592"
---
# <a name="sobroadcast"></a>したがって\_ブロードキャスト


SO の状態\_ブロードキャスト ソケット オプションは、データグラム ソケット経由でブロードキャスト メッセージを送信できるかどうかを決定します。 このソケット オプションは、データグラム ソケットだけに適用されます。

WSK アプリケーションを呼び出すこのソケット オプションの状態を設定する、 [ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)関数は次のパラメーター。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_BROADCAST</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>取得</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof(ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>新しいソケット オプションの状態の値を含む ULONG に型指定された変数へのポインター。</p>
<p>0:ブロードキャスト メッセージを許可しません。</p>
<p>1:メッセージのブロードキャストを許可します。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

 

このソケット オプションの状態を取得するには、WSK アプリケーションが呼び出す、 **WskControlSocket**関数は次のパラメーター。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_BROADCAST</p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>取得</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof(ULONG)</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>ソケット オプションの状態の値を受信する ULONG に型指定された変数へのポインター。</p>
<p>0:メッセージのブロードキャストが許可されていません</p>
<p>1:メッセージのブロードキャストが許可されます。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

 

呼び出すときに、WSK アプリケーションは IRP へのポインターを指定する必要があります、 **WskControlSocket**などの状態を取得または設定する関数\_ブロードキャスト ソケット オプション。

このソケット オプションの既定の状態は、ブロードキャスト メッセージは許可されません。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ws2def.h (Wsk.h を含む)</td>
</tr>
</tbody>
</table>

 

 




