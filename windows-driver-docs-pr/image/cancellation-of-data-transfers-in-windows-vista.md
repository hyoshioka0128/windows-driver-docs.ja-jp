---
title: Windows Vista でのデータ転送のキャンセル
description: Windows Vista でのデータ転送のキャンセル
ms.assetid: 0cdc02bf-23fe-4122-8d5f-f42c3c07da8b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 810002b8f9a68bd69b7cfdee833131e087407567
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840878"
---
# <a name="cancellation-of-data-transfers-in-windows-vista"></a>Windows Vista でのデータ転送のキャンセル


Windows Vista には、アプリケーションがストリームベースのデータ転送を実行するために使用する新しいインターフェイス**IWiaTransfer** (Windows SDK のドキュメントで説明されています) があります。 新しい転送メソッドに加えて、このインターフェイスには、アプリケーションがデータ転送を取り消すために使用できる**cancel**メソッドが含まれています ([複数項目の転送](multipage-istream-transfers.md)を含む)。 この方法では、データ転送を非同期にキャンセルできます。 データ転送を取り消すには、この手順を使用することをお勧めします。 ただし、Windows Vista アプリケーションは、コールバックルーチンから S\_FALSE を返して転送を取り消すこともできます。

このため、Windows Vista の WIA アプリケーションで転送を取り消すには、次の2つの方法があります。

-   コールバックルーチンから S\_FALSE を返します。

-   **IWiaTransfer:: Cancel**を呼び出します。

Windows Vista ドライバーは、アプリケーションが転送を取り消した2つの方法で通知できます。

-   ドライバーは、 [**IWiaMiniDrv::D rvnotifypnpevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)の呼び出しを、WIA\_イベント\_、\_IO イベントにキャンセルします。 すべてのカーネルモードの読み取り操作または書き込み操作で重複 i/o を使用することをお勧めします。 *即時*キャンセルを保証するには、この手順を使用する必要があります。

-   S\_FALSE は、 **IWiaMiniDrvTransferCallback:: GetNextStream**と[**IWiaMiniDrvTransferCallback:: SendMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvtransfercallback-sendmessage)の2つのコールバック関数から返されます。

アプリケーションで**IWiaTransfer:: cancel**を呼び出す場合は、 **IWiaMiniDrv::d rvnotifypnpevent**メソッドを、WIA\_イベント\_使用してドライバーに呼び出し、IO\_をキャンセルする必要があります。 また、 [**IWiaMiniDrvTransferCallback:: GetNextStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvtransfercallback-getnextstream)および**IWiaMiniDrvTransferCallback:: SendMessage**コールバック関数は、転送が取り消された後、常に S\_FALSE を返す必要があります。

**IwiatransGetNextStream callback::** が、[マルチ項目転送](multipage-istream-transfers.md)中に\_項目をスキップする\_\_WIA を返す場合、アプリケーションは現在の項目をスキップします (つまり、転送しません)。 S\_FALSE の戻り値は、転送全体を取り消す必要があることを意味します。

**IWiaTransfer**および**Iwiatrancallback**インターフェイスについては、Microsoft Windows SDK のドキュメントを参照してください。

## <a name="related-topics"></a>関連トピック
[**IWiaMiniDrvTransferCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvtransfercallback)  



