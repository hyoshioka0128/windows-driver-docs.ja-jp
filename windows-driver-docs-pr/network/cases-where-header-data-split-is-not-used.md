---
title: ヘッダー データの分割が使用されないケース
description: ヘッダー データの分割が使用されないケース
ms.assetid: e5d3071e-a0d1-4a66-b8aa-6823e737f242
keywords:
- ヘッダー-データ分割 WDK (使用されていない場合)
- イーサネットフレームの分割 WDK ネットワーク (使用されていない場合)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 501d3cf95cdc4e7d927410dff3d0f8e2641480ee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835241"
---
# <a name="cases-where-header-data-split-is-not-used"></a>ヘッダー データの分割が使用されないケース





このトピックでは、ヘッダーデータ分割プロバイダーがイーサネットフレームを分割できないケースの概要について説明します。 ヘッダーデータの分割をサポートするためにプロバイダーが満たす必要のある最小要件の一覧については、「[サポートヘッダーデータの分割の最小要件](minimum-requirements-for-supporting-header-data-split.md)」を参照してください。

  、受信したフレームがヘッダーデータ分割プロバイダーの要件を超えて分割される場合があることに**注意**してください。 つまり、ヘッダーデータの分割要件は、ヘッダーデータの分割プロバイダーにのみ適用されます。 このような場合は、最初の MDL に少なくとも、先読みサイズとして指定された NDIS のバイト数以上が含まれていない限り、IP ヘッダー、IPv4 オプション、IPsec ヘッダー、IPv6 拡張ヘッダー、または上層プロトコルヘッダーの途中でイーサネットフレームを分割しないでください。

 

分割されていないすべてのイーサネットフレームは、一般的な NDIS の規則と要件に従う必要があります。 たとえば、受信した[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造の mdls のチェーンにある最初の MDL には、事実上連続するバッファー内のフレームの先読み部分またはイーサネットフレーム全体 (より小さい方) のいずれかが含まれている必要があります。 NDIS は、[現在\_先読み OID\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-lookahead) 、先読みのサイズを OID\_GEN に設定します。

ヘッダー-データ分割プロバイダー:

-   非 IP フレームは分割しないでください。

-   これらの場所のいずれかで分割できない場合は、フレームを分割しないでください。上位層のプロトコルヘッダーの先頭、TCP ペイロードの先頭、または UDP ペイロードの先頭にあります。

-   [上位層のプロトコルヘッダーの先頭](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)でヘッダーを分割できない限り、構成された最大ヘッダーサイズを超えるフレームは分割しないでください。 ヘッダーの最大サイズの詳細については、「[ヘッダーバッファーの割り当て](allocating-the-header-buffer.md)」を参照してください。

-   NIC で認識されない IPv4 オプションを含むフレームは分割しないでください。

-   NIC で認識されない IPv6 拡張ヘッダーを含むフレームは分割しないでください。

-   Tcp ヘッダーの先頭で分割できる場合を除き、NIC で認識されない TCP オプションを含むフレームは分割しないでください。

 

 





