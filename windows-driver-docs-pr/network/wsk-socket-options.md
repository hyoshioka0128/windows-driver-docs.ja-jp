---
title: WSK ソケット オプション
description: WSK ソケット オプション
ms.assetid: 640681a3-ea68-44c5-be2b-a3bc21bfdb7c
ms.date: 07/18/2017
keywords:
- WSK ソケット オプション ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 5e825b4ca84cf0ac3953f3cc051442a9c1288cce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379720"
---
# <a name="wsk-socket-options"></a>WSK ソケット オプション


SOL で、次のソケット オプションをサポートする、WSK サブシステム\_ソケット レベル。

[**したがって\_ブロードキャスト**](https://docs.microsoft.com/windows-hardware/drivers/network/so-broadcast)

[**したがって\_条件付き\_ACCEPT**](https://docs.microsoft.com/windows-hardware/drivers/network/so-conditional-accept)

[**したがって\_EXCLUSIVEADDRUSE**](https://docs.microsoft.com/windows-hardware/drivers/network/so-exclusiveaddruse)

[**したがって\_KEEPALIVE**](https://docs.microsoft.com/windows-hardware/drivers/network/so-keepalive)

[**したがって\_RCVBUF**](https://docs.microsoft.com/windows-hardware/drivers/network/so-rcvbuf)

[**したがって\_REUSEADDR**](https://docs.microsoft.com/windows-hardware/drivers/network/so-reuseaddr)

[**したがって\_WSK\_イベント\_コールバック**](so-wsk-event-callback.md)

[**したがって\_WSK\_セキュリティ**](so-wsk-security.md)

基になるネットワーク プロトコルは、追加のソケット オプションをサポート可能性があります。

詳細の各ソケット オプションに関する情報だけでなく SOL 以外のレベルでのソケット オプションに関する情報の\_ソケット、Microsoft Windows SDK ドキュメントの「Windows Sockets 2"セクションを参照してください。

<a name="requirements"></a>要件
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

 

 




