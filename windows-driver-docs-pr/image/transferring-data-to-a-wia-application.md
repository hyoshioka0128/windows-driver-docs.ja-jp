---
title: WIA アプリケーションへのデータ転送
description: WIA アプリケーションへのデータ転送
ms.assetid: 3ad906c9-968f-43d7-ae17-fc570440883d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d440d8f90f6d2fba3b2ed3a4760607097c065143
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358213"
---
# <a name="transferring-data-to-a-wia-application"></a>WIA アプリケーションへのデータ転送





WIA サービスを呼び出すアプリケーションは、データ転送を開始するときに、 [ **IWiaMiniDrv::drvAcquireItemData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)転送を実行するメソッド。 このメソッドは、デバイスからのデータの取得と送信を使用して、アプリケーションにデータを戻すことを[ **IWiaMiniDrvCallBack::MiniDrvCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvcallback-minidrvcallback)メソッド。

Microsoft Windows Millennium Edition (me) および Windows XP では、WIA ミニドライバーで 2 つの種類のデータ転送を処理するためにできる必要があります: ファイルおよびメモリです。 転送の種類、アプリケーションの開始を確認するのにようにミニドライバーを読み取る必要があります、 [ **WIA\_IPA\_TYMED** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)プロパティ値またはチェック、 **tymed**のメンバー、 [ **MINIDRV\_転送\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/ns-wiamindr_lh-_minidrv_transfer_context)構造体。 2 番目のオプションは、WIA ミニドライバーと呼ばれる場合にのみ有効ですが、 [ **wiasGetImageInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetimageinformation)関数を最初にサービスします。 **WiasGetImageInformation**サービス関数が、WIA を自動的に読み取って\_IPA\_TYMED プロパティに値が割り当てられます、 **tymed** MINIDRVのメンバー\_転送\_CONTEXT 構造体。

推奨される方法は、WIA を読み取る WIA ミニドライバー\_IPA\_TYMED プロパティの値。 これにより、ミニドライバーが適切な型の取得を実行しています。

Windows Vista 以降、簡略化されたストリーム ベースの転送方法が導入されました。 詳細については、このデータ転送メソッドを参照してください[IStream Data Transfers](istream-data-transfers.md)します。

このセクションでは、次のトピックについて説明します。

[TYMED を理解します。](understanding-tymed.md)

[データのメモリの割り当てください。](allocating-memory-for-data.md)

[データ転送をキャンセル](canceling-a-data-transfer.md)

[保留中の I/O 操作のキャンセル](canceling-pending-i-o-operations.md)

[RAW 形式のデータ転送](raw-format-data-transfer.md)

TYMED (メモリ内およびファイル転送) を使用してデータに関する基本的な情報の転送およびストリーム ベースの転送を参照してください[Data Transfers](data-transfers.md)します。

 

 




