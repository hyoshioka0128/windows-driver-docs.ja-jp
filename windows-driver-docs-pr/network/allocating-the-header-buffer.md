---
title: ヘッダー バッファーの割り当て
description: ヘッダー バッファーの割り当て
ms.assetid: 7a6e87ce-a0b8-45ce-961e-f09d5ca919cb
keywords:
- ヘッダー-データ分割 WDK、バッファー割り当て
- 最大ヘッダーサイズ WDK ヘッダー-データの分割
- バッファー割り当て WDK ヘッダー-データ分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2d9a25c77f490659062b7a0d5d5f2eda7cf74fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835289"
---
# <a name="allocating-the-header-buffer"></a>ヘッダー バッファーの割り当て





NDIS は、ミニポートドライバーが[**ndis\_HD\_SPLIT\_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)構造体の**maxheadersize**メンバーで割り当てる必要がある最大ヘッダーサイズを指定します。 ヘッダーデータの分割属性の設定の詳細については、「[ヘッダーデータの分割プロバイダーの初期化](initializing-a-header-data-split-provider.md)」を参照してください。

NIC が受信したイーサネットフレーム内のヘッダーとデータを分割する場合、指定されたイーサネットフレームのヘッダー部分のサイズが**Maxheadersize**値を超えないようにする必要があります。

IP ヘッダーに IPv4 オプション、IPsec ヘッダー、または IPv6 拡張ヘッダーが含まれていて、ヘッダーが**Maxheadersize**値を超えている場合、NIC はフレームを分割できません。

UDP ヘッダー、TCP ヘッダー、または TCP オプションを含むヘッダーが**Maxheadersize**値を超えている場合、NIC は、[上位層プロトコルヘッダーの先頭](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)にフレームを分割するか、フレームを分割しないようにする必要があります。

 

 





