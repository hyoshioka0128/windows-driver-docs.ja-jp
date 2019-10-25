---
title: TCP ペイロードでのフレームの分割
description: TCP ペイロードでのフレームの分割
ms.assetid: 3d7c6f75-4523-4ad3-b15d-53f9d4ee1074
keywords:
- イーサネットフレーム分割 WDK ネットワーク、TCP ペイロード
- TCP ペイロード WDK ヘッダー-データの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5d3a9467efcee35ab6b1300b4e3ca258424e039
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841864"
---
# <a name="splitting-frames-at-the-tcp-payload"></a>TCP ペイロードでのフレームの分割





ヘッダーデータの分割をサポートする NDIS ミニポートアダプターは、TCP フレームの上位層プロトコルヘッダーでフレームの分割をサポートする必要があります。 ただし、tcp ヘッダーに TCP オプションが含まれていない場合、NIC は TCP ペイロードの先頭にフレームを分割する必要があります。

結果のヘッダーバッファーの長さが最大ヘッダーサイズより長い場合、NIC は TCP フレームを分割できない可能性があります。 ヘッダーの最大サイズを超えたときのフレームの分割の詳細については、「[ヘッダーバッファーの割り当て](allocating-the-header-buffer.md)」を参照してください。

また、Nic では、タイムスタンプオプションだけを使用して TCP ヘッダーの分割をサポートする必要があります。 つまり、timestamp オプションは、必須の唯一の TCP オプションです。 それ以外の場合、TCP オプションを使用した TCP ヘッダーのサポートは省略可能です。 フレームの TCP ヘッダーに認識されない TCP オプションが含まれている場合、NIC は、TCP ヘッダーの先頭 (つまり、上位層のプロトコルヘッダー) にフレームを分割するか、フレームを分割しないようにする必要があります。

ヘッダーデータ要件のために IPv4 オプション、IPv6 拡張ヘッダー、または TCP オプションをサポートする  は、NIC が要素を認識し、その長さを決定して、ヘッダー MDL に含め、その末尾を特定できるように**することを**意味します。フレーム内の次の要素の先頭。

 

上位層のプロトコルヘッダーの先頭にフレームを分割する方法の詳細については、「[上位層のプロトコルヘッダーの先頭にフレームを分割](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)する」を参照してください。

ヘッダーデータの分割プロバイダーが TCP ペイロードでフレームを分割する場合、指定された[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造には、\_TCP および NDIS\_NBL\_フラグ\_NBL\_フラグが\_設定されている必要があり\_SPLIT は、 **Nblflags**メンバーで設定された\_上位\_レイヤー\_プロトコル\_ペイロードフラグを\_分割します。 ヘッダーの設定の詳細については、「ネットワーク\_バッファー\_リストフラグの設定」を参照してください。[ネットワーク\_バッファーの設定\_リストの情報](setting-net-buffer-list-information.md)

 

 





