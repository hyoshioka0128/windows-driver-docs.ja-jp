---
title: サポートヘッダー-プロトコルとフィルタードライバーでのデータの分割
description: サポートヘッダー-プロトコルドライバーとフィルタードライバーでのデータの分割
ms.assetid: ba1566f2-7da6-4472-b00b-e25bf7acc294
keywords:
- ヘッダー-データ分割 WDK、プロトコルドライバー
- ヘッダー-データ分割 WDK、フィルタードライバー
- プロトコルドライバー WDK ネットワーク, ヘッダー-データの分割
- フィルタードライバーの WDK ネットワーク, ヘッダー-データの分割
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fcfc782692858c430ccd9559511f2d511423e36
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841798"
---
# <a name="supporting-header-data-split-in-protocol-drivers-and-filter-drivers"></a>サポートヘッダー-プロトコルドライバーとフィルタードライバーでのデータの分割





NDIS 6.0 以降のプロトコルドライバーとフィルタードライバーでは、連続していないバッファーのヘッダーとデータを使用した受信表示をサポートする必要があります。

[**NET\_のバッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造に含まれる MDL が1つだけであるとは限りません。 プロトコルドライバーとフィルタードライバーは、ヘッダーデータの分割登録をサポートするために特別な処理を行う必要はありません。 ただし、ドライバーの受信処理コードは、MDL チェーン内の複数の MDL を処理する必要があります。また、MDL チェーンにアクセスするには、次の NDIS MDL マクロを使用する必要があります。

-   [**NET\_BUFFER\_最初\_MDL**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-first-mdl)

-   [**現在\_MDL\_NET\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-current-mdl)

-   [**NET\_BUFFER\_現在の\_MDL\_オフセット**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-current-mdl-offset)

分割バッファーを使用すると、net\_バッファー構造に関連付けられているデータ長 ( [**net\_バッファー\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_data)構造体の**DataLength**メンバー内) は、複数の mdls に分割されます。 たとえば、プロトコルドライバーが最初の MDL のデータバッファー全体にアクセスしようとした場合、ドライバーは無効なデータにアクセスする可能性があります。

受信通知呼び出しがミニポートドライバーに戻ると、ミニポートドライバーがヘッダー MDLs を再利用できることに**注意**してください  。 受信通知の呼び出しがミニポートドライバーに戻ると、それ以降のドライバーまたはそのクライアントはヘッダー MDLs にアクセスできません。 この制限は、ミニポートドライバーが NDIS の状態で受信したデータを示していない場合にも適用され、\_フラグ\_リソース\_受信します。

 

 

 





