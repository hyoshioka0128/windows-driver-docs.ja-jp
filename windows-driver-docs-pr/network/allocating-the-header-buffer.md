---
title: ヘッダー バッファーの割り当て
description: ヘッダー バッファーの割り当て
ms.assetid: 7a6e87ce-a0b8-45ce-961e-f09d5ca919cb
keywords:
- ヘッダー データの分割 WDK、バッファーの割り当て
- ヘッダーの最大サイズの WDK ヘッダー データの分割
- WDK のヘッダー データ バッファーの割り当てを分割します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da6252aaf3691551266ac65aecf9e0765a0f9226
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384413"
---
# <a name="allocating-the-header-buffer"></a>ヘッダー バッファーの割り当て





NDIS ミニポート ドライバーに割り当てる必要がありますヘッダーの最大サイズを指定する、 **MaxHeaderSize**のメンバー、 [ **NDIS\_HD\_分割\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_hd_split_attributes)構造体。 ヘッダー データの分割の属性を設定する方法についての詳細については、次を参照してください。[ヘッダー データの分割プロバイダーの初期化](initializing-a-header-data-split-provider.md)します。

指定したイーサネット フレームのヘッダー部分のサイズを超えない NIC では、ヘッダーと受信したイーサネット フレーム内のデータを分割、ときに、 **MaxHeaderSize**値。

IP ヘッダーには、IPv4 オプション、IPsec のヘッダー、または IPv6 拡張ヘッダーが含まれている場合、およびヘッダーを超えた場合、 **MaxHeaderSize**値、NIC がフレームに分割する必要があります。

UDP ヘッダー、TCP ヘッダーまたは TCP オプションを含むヘッダーを超えた場合、 **MaxHeaderSize**値、NIC にフレームを分割する必要がありますか、[上のレイヤー プロトコル ヘッダーの先頭](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)しない必要がありますかフレームに分割します。

 

 





