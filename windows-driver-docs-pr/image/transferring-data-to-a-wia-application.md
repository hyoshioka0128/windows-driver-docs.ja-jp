---
title: WIA アプリケーションへのデータ転送
description: WIA アプリケーションへのデータ転送
ms.assetid: 3ad906c9-968f-43d7-ae17-fc570440883d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 601f1c1a982410e27220af651b9a1e253e8fa201
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840731"
---
# <a name="transferring-data-to-a-wia-application"></a>WIA アプリケーションへのデータ転送





アプリケーションでデータ転送が開始されると、WIA サービスは[**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)メソッドを呼び出して転送を実行します。 このメソッドは、 [**IWiaMiniDrvCallBack:: MiniDrvCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)メソッドを使用して、デバイスからデータを取得し、そのデータをアプリケーションに送り返す役割を担います。

Microsoft Windows Millennium Edition (Me) と Windows XP では、WIA ミニドライバーは、ファイルとメモリという2種類のデータ転送を処理できる必要があります。 アプリケーションが開始された転送の種類を確認するには、ミニドライバーは、 [**WIA\_IPA\_TYMED**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)プロパティ値を読み取るか、 [**MINIDRV\_transfer\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context)構造体の**TYMED**メンバーを確認する必要があります。 2番目のオプションは、WIA ミニドライバーが[**wiasGetImageInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetimageinformation) service 関数を最初に呼び出した場合にのみ有効です。 **WiasGetImageInformation** service 関数は、WIA\_IPA\_TYMED プロパティを自動的に読み取り、MINIDRV\_TRANSFER\_CONTEXT 構造体の**TYMED**メンバーに値を割り当てます。

使用する方法としては、WIA ミニドライバーで WIA\_IPA\_TYMED プロパティ値を読み取る方法が挙げられます。 これにより、ミニドライバーが適切な種類の取得を実行していることが保証されます。

Windows Vista 以降では、簡略化されたストリームベースの転送方法が導入されました。 このデータ転送方法の詳細については、「 [IStream データ転送](istream-data-transfers.md)」を参照してください。

このセクションでは、次のトピックについて説明します。

[TYMED について](understanding-tymed.md)

[データのメモリの割り当て](allocating-memory-for-data.md)

[データ転送の取り消し](canceling-a-data-transfer.md)

[保留中の i/o 操作の取り消し](canceling-pending-i-o-operations.md)

[未加工の形式データ転送](raw-format-data-transfer.md)

TYMED (メモリ内およびファイル転送) とストリームベースの転送を使用したデータ転送に関する基本的な情報については、「[データ転送](data-transfers.md)」を参照してください。

 

 




