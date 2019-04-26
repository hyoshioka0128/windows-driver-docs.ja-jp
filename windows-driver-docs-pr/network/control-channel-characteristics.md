---
title: コントロール チャネルの特性
description: コントロール チャネルの特性
ms.assetid: b289f21c-a53e-424c-be31-b7a869e335c4
keywords:
- コントロール チャネルの特性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a0dba41cb510802285d5a1b5ecc3d9f181af33f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357417"
---
# <a name="control-channel-characteristics"></a>コントロール チャネルの特性





デバイスのコントロール チャネルは、その USB コントロール エンドポイントです。 ホストからデバイスへのコントロール メッセージは送信として送信\_カプセル化\_コマンド転送します。 この転送は、次の表で定義されます。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">BmRequestType</th>
<th align="left">bRequest</th>
<th align="left">wValue</th>
<th align="left">wIndex</th>
<th align="left">wLength</th>
<th align="left">データ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x21</p></td>
<td align="left"><p>0x00</p></td>
<td align="left"><p>0x0000</p></td>
<td align="left"><p><em>bInterfaceNumber</em>通信クラス インターフェイスの記述子フィールド</p></td>
<td align="left"><p>コントロールのメッセージ ブロックのバイト長</p></td>
<td align="left"><p>コントロールのメッセージ ブロック</p></td>
</tr>
</tbody>
</table>

 

ホストは、入力コントロールのメッセージの USB コントロール エンドポイントを継続的にポーリングしません。 そのコントロール エンドポイント上のコントロール メッセージを配置すると、デバイスは、デバイスがコントロールのメッセージを返すたびに、ホストはポーリング、通信クラス インターフェイスの割り込みのエンドポイントで通知を返す必要があります。 デバイスの割り込みのエンドポイントからホストへの転送とは、標準の USB の割り込みの転送です。 唯一の定義済みのデバイスの通知は、応答\_使用可能な通知、次の表で定義されています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オフセット (バイト)</th>
<th align="left">長さ (バイト)</th>
<th align="left">フィールド</th>
<th align="left">データ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>通知</p></td>
<td align="left"><p>RESPONSE_AVAILABLE (0X00000001)</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

応答の受信時に\_使用可能な通知は、ホスト コントロールからメッセージを読み取り、GET を使用して、コントロール エンドポイント\_カプセル化\_応答転送では、次の表で定義されています。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bmRequestType</th>
<th align="left">bRequest</th>
<th align="left">wValue</th>
<th align="left">wIndex</th>
<th align="left">wLength</th>
<th align="left">データ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0xA1</p></td>
<td align="left"><p>0x01</p></td>
<td align="left"><p>0x0000</p></td>
<td align="left"><p><em>bInterfaceNumber</em>通信クラス インターフェイスの記述子フィールド</p></td>
<td align="left"><p>0x0400 (これはホストによって投稿されたバッファーの最小バイト数)</p></td>
<td align="left"><p>コントロールのメッセージ ブロック</p></td>
</tr>
</tbody>
</table>

 

デバイスが、GET を受信する何らかの理由の場合\_カプセル化\_応答と、コントロール エンドポイントで有効なデータで応答することが 1 バイトのパケット コントロール エンドポイントを停止するのではなく、0x00 に設定を返す必要があります。

 

 





