---
title: プロトコルとフィルター ドライバーで分割ヘッダー データのサポート
description: プロトコルおよびフィルター ドライバーでのヘッダー データの分割のサポート
ms.assetid: ba1566f2-7da6-4472-b00b-e25bf7acc294
keywords:
- ヘッダー データの分割 WDK、プロトコル ドライバー
- ヘッダー データのフィルター ドライバー WDK の分割
- プロトコル ドライバー WDK ネットワー キング、ヘッダー データの分割
- フィルター ドライバー WDK ネットワー キング、ヘッダー データの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef6b2ddf0327e6bc7f5bdad31e6ba5741aa77b54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381188"
---
# <a name="supporting-header-data-split-in-protocol-drivers-and-filter-drivers"></a>プロトコルおよびフィルター ドライバーでのヘッダー データの分割のサポート





NDIS 6.0 とそれ以降のプロトコル ドライバーとフィルター ドライバーがサポートする必要が連続していないバッファーでの受信ヘッダーとデータを表示します。

1 つの MDL のみがあることを想定する必要があります、 [ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造体。 プロトコルおよびフィルター ドライバーは、特定のヘッダー データの登録の分割をサポートするために何もする必要はありません。 ただし、ドライバーの受信処理コード MDL チェーン内の 1 つ以上の MDL を処理する必要があり、MDL チェーンへのアクセスには次の NDIS MDL マクロを使用する必要があります。

-   [**NET\_バッファー\_最初\_MDL**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-first-mdl)

-   [**NET\_バッファー\_現在\_MDL**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-current-mdl)

-   [**NET\_バッファー\_現在\_MDL\_オフセット**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-current-mdl-offset)

分割のバッファーに、データの長さに関連付けられている、NET\_バッファーの構造 (で、 **DataLength**のメンバー、 [ **NET\_バッファー\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_data)構造) は複数 MDLs に分かれます。 たとえば、プロトコル ドライバーでは、データ全体の最初の MDL バッファーにアクセスしようとして、ドライバーは無効なデータをアクセスでした。

**注**  ミニポート ドライバーに受信を示す値の呼び出しが返されると、ミニポート ドライバーが MDLs ヘッダーを再利用できます。 上にあるドライバーやそのクライアントしてする必要があります、ミニポート ドライバーに受信を示す値の呼び出しが戻った後 MDLs ヘッダーはアクセスできません。 この制限がもときに、ミニポート ドライバーがいないを示す NDIS の状態で、受信したデータを適用しても\_受信\_フラグ\_リソース。

 

 

 





