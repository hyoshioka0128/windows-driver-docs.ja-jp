---
title: 上部レイヤーのプロトコルヘッダーでフレームを分割する
description: 上位レイヤーの先頭にフレームを分割する-プロトコルヘッダー
ms.assetid: 2559ac20-46dc-4116-9d12-b2cd634e501b
keywords:
- 上層プロトコルからのイーサネットフレームの分割 WDK ネットワーク
- 上位層プロトコル WDK ヘッダー-データの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ac667525619b94bd67b5e6b6a653d2c4073edfa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841868"
---
# <a name="splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers"></a>上位レイヤーの先頭にフレームを分割する-プロトコルヘッダー





*上位層プロトコル*は、TCP、UDP、ICMP などの IP トランスポートプロトコルです。

**注**  IPsec は、ヘッダーデータの分割要件では、上位層プロトコルとは見なされません。 IPsec フレームの分割の詳細については、「 [Ipsec フレームの分割](splitting-ipsec-frames.md)」を参照してください。

 

NIC が上層プロトコルヘッダーの先頭にイーサネットフレームを分割した場合、指定された[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)には、ちょうど2つの mdls が含まれている必要があります。 最初の MDL が記述するバッファーは、イーサネットフレーム (MAC ヘッダー) の最初のバイトで始まり、2番目の MDL が記述するバッファーは、上位層のプロトコルヘッダーの最初のバイトで始まる必要があります。

NIC が tcp または UDP のペイロードで TCP フレームと UDP フレームを分割できる  に**注意**してください。 詳細については、「 [TCP ペイロードでのフレームの分割](splitting-frames-at-the-tcp-payload.md)」と「[フレームの UDP ペイロードでの分割](splitting-frames-at-the-udp-payload.md)」を参照してください。

 

ヘッダーデータの分割プロバイダーが上位層プロトコルのヘッダーの先頭にフレームを分割する場合、指定された[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造には、 **nblflags**メンバーで設定された\_上\_レイヤー\_プロトコル\_ヘッダーフラグに\_を分割\_するように、NDIS\_NBL\_フラグが設定されている必要があります。 ヘッダーの設定の詳細については、「ネットワーク\_バッファー\_リストフラグの設定」を参照してください。[ネットワーク\_バッファーの設定\_リストの情報](setting-net-buffer-list-information.md)

結果のヘッダーバッファーの長さが最大ヘッダーサイズよりも長い場合、NIC はフレームを分割しないでください。 ヘッダーの最大サイズを超えたときのフレームの分割の詳細については、「[ヘッダーバッファーの割り当て](allocating-the-header-buffer.md)」を参照してください。

 

 





