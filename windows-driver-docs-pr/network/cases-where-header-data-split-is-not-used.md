---
title: ヘッダー データの分割が使用されないケース
description: ヘッダー データの分割が使用されないケース
ms.assetid: e5d3071e-a0d1-4a66-b8aa-6823e737f242
keywords:
- ヘッダー データを使用しない場合は、WDK を分割
- 使用しない場合は、WDK のネットワークを分割するイーサネット フレーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 082039603369df6496062444d400a2ca5b766d7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382791"
---
# <a name="cases-where-header-data-split-is-not-used"></a>ヘッダー データの分割が使用されないケース





このトピックでは、ヘッダー データがプロバイダーを分割するケースの概要については、イーサネット フレームを分割する必要があります。 プロバイダーが満たす必要のある最小要件の一覧についてはヘッダー データの分割をサポートするために「[ヘッダー データの分割のサポートの最小要件](minimum-requirements-for-supporting-header-data-split.md)します。

**注**  ヘッダー データ プロバイダーの要件の分割の外部で受信したフレームを分割できる場合があります。 つまり、ヘッダー データの分割の要件は、ヘッダー データ プロバイダーの分割にのみ適用されます。 このような場合は、決して分割 IP ヘッダー、IPv4 のオプション、IPsec のヘッダー、IPv6 拡張ヘッダー、またはプロトコル レイヤー上のヘッダー、途中でイーサネット フレームの最初の MDL 数以上のバイトを先読みサイズに指定された NDIS として含まれていない場合。

 

分割されないすべてのイーサネット フレームは、NDIS の一般的な規則と要件に従う必要があります。 受信した MDLs のチェーン内の最初の MDL など[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造体は、フレームの先読みの一部または全体のイーサネット フレーム (小さい方です) のいずれかを含める必要がありますで仮想的に連続するバッファー。 NDIS の先読みのサイズを設定する、 [OID\_GEN\_現在\_先読み](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-lookahead)OID。

ヘッダー データ プロバイダーを分割します。

-   非 IP フレームに分割しません。

-   これらの場所のいずれかで、分割できない場合は、フレームを分割しない: 上のレイヤー プロトコル ヘッダーの先頭、TCP ペイロードの先頭または UDP ペイロードの先頭にあります。

-   ヘッダーに分割できる場合を除き、構成されているヘッダーの最大サイズを超えるフレームに分割しない、[上のレイヤー プロトコル ヘッダーの先頭](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)します。 ヘッダーの最大サイズの詳細については、次を参照してください。[ヘッダーのバッファーを割り当てる](allocating-the-header-buffer.md)します。

-   NIC が認識されない IPv4 オプションを含むフレームに分割しません。

-   NIC を認識しない IPv6 拡張ヘッダーが含まれているフレームを分割しません。

-   TCP ヘッダーの先頭の分割しない限り、NIC が認識しない TCP オプションを含むフレームに分割しません。

 

 





