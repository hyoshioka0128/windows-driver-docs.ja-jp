---
title: ヘッダーのバッファーを割り当てる
description: ヘッダーのバッファーを割り当てる
ms.assetid: 7a6e87ce-a0b8-45ce-961e-f09d5ca919cb
keywords:
- ヘッダー データの分割 WDK、バッファーの割り当て
- ヘッダーの最大サイズの WDK ヘッダー データの分割
- WDK のヘッダー データ バッファーの割り当てを分割します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7af30ffb732817fba0b7516b09d357b4052606cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531483"
---
# <a name="allocating-the-header-buffer"></a>ヘッダーのバッファーを割り当てる





NDIS ミニポート ドライバーに割り当てる必要がありますヘッダーの最大サイズを指定する、 **MaxHeaderSize**のメンバー、 [ **NDIS\_HD\_分割\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565694)構造体。 ヘッダー データの分割の属性を設定する方法についての詳細については、次を参照してください。[ヘッダー データの分割プロバイダーの初期化](initializing-a-header-data-split-provider.md)します。

指定したイーサネット フレームのヘッダー部分のサイズを超えない NIC では、ヘッダーと受信したイーサネット フレーム内のデータを分割、ときに、 **MaxHeaderSize**値。

IP ヘッダーには、IPv4 オプション、IPsec のヘッダー、または IPv6 拡張ヘッダーが含まれている場合、およびヘッダーを超えた場合、 **MaxHeaderSize**値、NIC がフレームに分割する必要があります。

UDP ヘッダー、TCP ヘッダーまたは TCP オプションを含むヘッダーを超えた場合、 **MaxHeaderSize**値、NIC にフレームを分割する必要がありますか、[上のレイヤー プロトコル ヘッダーの先頭](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)しない必要がありますかフレームに分割します。

 

 





