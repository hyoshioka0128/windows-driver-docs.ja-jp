---
title: TCP ペイロードでのフレームの分割
description: TCP ペイロードでのフレームの分割
ms.assetid: 3d7c6f75-4523-4ad3-b15d-53f9d4ee1074
keywords:
- WDK のネットワー キング、TCP ペイロードを分割するイーサネット フレーム
- TCP ペイロード WDK のヘッダー データの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdeea28393f3c062c2e608c87910b8c000c09be1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383615"
---
# <a name="splitting-frames-at-the-tcp-payload"></a>TCP ペイロードでのフレームの分割





ヘッダー データの分割をサポートする NDIS ミニポート アダプターでは、TCP フレーム上のレイヤー プロトコル ヘッダーを分割のフレームをサポートする必要があります。 ただし、TCP ヘッダーに、TCP オプションが含まれていない場合、NIC は、TCP ペイロードの先頭のフレームを分割する必要があります。

NIC できない結果のヘッダーのバッファーがある最大ヘッダー サイズより大きい長さ場合 TCP フレームに分割することがあります。 ヘッダーの最大サイズを超えたときに、フレームを分割の詳細については、次を参照してください。[ヘッダーのバッファーを割り当てる](allocating-the-header-buffer.md)します。

Nic には、タイムスタンプのオプションのみを使用して分割の TCP ヘッダーもサポートする必要があります。 つまり、タイムスタンプ オプションは必須である TCP オプションのみです。 それ以外の場合、TCP オプションを使用して、TCP ヘッダーのサポートは省略可能です。 NIC が TCP ヘッダーの先頭のフレームを分割する必要がありますか、フレームの TCP ヘッダーに認識できない TCP オプションが含まれている場合 (つまり、上のレイヤー プロトコル ヘッダーを)、フレームを分割または。

**注**  ヘッダー データの要件のため、IPv4 オプション、IPv6 拡張ヘッダーまたは TCP オプションをサポートしている要素を認識、その長さを決定、MDL ヘッダーに含めるのための NIC の能力を意味し、フレームの末尾と次の要素の先頭を探します。

 

上のレイヤー プロトコル ヘッダーの先頭のフレームの分割の詳細については、次を参照してください。[上のレイヤー プロトコル ヘッダーの先頭のフレームの分割](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)します。

プロバイダーが TCP ペイロードを指定された位置のフレームを分割する場合は、ヘッダー データの分割[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体は、NDIS をいる必要があります\_NBL\_フラグ\_IS\_TCP および NDIS\_NBL\_フラグ\_分割\_で\_上限\_レイヤー\_プロトコル\_ペイロードのフラグのセット、 **NblFlags**メンバー。 ヘッダー データの設定の詳細については、NET を分割の\_バッファー\_フラグの一覧を参照してください[設定 NET\_バッファー\_情報を一覧表示](setting-net-buffer-list-information.md)します。

 

 





