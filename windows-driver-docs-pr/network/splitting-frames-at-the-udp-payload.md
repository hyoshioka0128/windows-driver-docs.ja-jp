---
title: UDP ペイロードでフレームを分割する
description: UDP ペイロードでフレームを分割する
ms.assetid: 10116077-89d2-4d07-9807-46b6281e9851
keywords:
- イーサネットフレーム分割 WDK ネットワーク、UDP ペイロード
- UDP ペイロード WDK ヘッダー-データの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a72cd08e833641f95e76db34205fb6cbe20bf50
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841862"
---
# <a name="splitting-frames-at-the-udp-payload"></a>UDP ペイロードでフレームを分割する





ヘッダーデータの分割をサポートする NDIS ミニポートアダプターは、UDP フレームの上位層プロトコルヘッダーでフレームの分割をサポートする必要があります。 ただし、NIC はまず、UDP ペイロードの先頭にフレームを分割する必要があります。

結果のヘッダーバッファーの長さが最大ヘッダーサイズより長い場合、NIC は UDP フレームを分割できない可能性があります。 ヘッダーの最大サイズを超えたときのフレームの分割の詳細については、「[ヘッダーバッファーの割り当て](allocating-the-header-buffer.md)」を参照してください。

NIC が UDP ペイロードでフレームを分割できない場合、NIC は、上位層のプロトコルヘッダーの先頭にフレームを分割するか、フレームを分割しないようにする必要があります。 上位層のプロトコルヘッダーの先頭にフレームを分割する方法の詳細については、「[上位層のプロトコルヘッダーの先頭にフレームを分割](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)する」を参照してください。

ヘッダーデータ分割プロバイダーが UDP ペイロードでフレームを分割する場合、指定された[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造には、NDIS\_NBL\_フラグ\_\_UDP および NDIS\_NBL\_フラグが設定されている必要があり\_SPLIT は、 **Nblflags**メンバーで設定された\_上位\_レイヤー\_プロトコル\_ペイロードフラグを\_分割します。 ヘッダーの設定の詳細については、「ネットワーク\_バッファー\_リストフラグの設定」を参照してください。[ネットワーク\_バッファーの設定\_リストの情報](setting-net-buffer-list-information.md)

 

 





