---
title: レガシ アプリケーションと Windows Vista ドライバー間のデータ転送
description: レガシ アプリケーションと Windows Vista ドライバー間のデータ転送
ms.assetid: 83817277-3526-4f64-8e7c-7e02c8cd77bd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06ef4b7699d2c7175a8e1883c24d47d26c9ec467
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360866"
---
# <a name="data-transfer-between-legacy-application-and-windows-vista-driver"></a>レガシ アプリケーションと Windows Vista ドライバー間のデータ転送


ドライバーのイメージの処理のフィルターが常に呼び出されること、および、レガシ アプリケーションを明示的に互換性レイヤーを確認する必要がありますサポート、 **LocalService**アカウントは、データ転送を実行できます。 **LocalService**アカウントは、Microsoft Windows XP 以降のオペレーティング システムで使用します。

従来、ドライバーには、少なくとも TYMED 両方を公開する必要があります\_ファイルと TYMED\_コールバックです。 ただし、Windows Vista のドライバーでは TYMED を公開しない\_コールバック (または TYMED\_マルチページ\_コールバック)。 互換レイヤーの転送部分 TYMED をレガシ アプリケーションが表示されることを確認すると、\_コールバックが、Windows Vista ドライバーは実装しません。 TYMED\_マルチページ\_コールバックは、Windows Vista ドライバーから公開しないでください。

TYMED でサポートされる形式をレガシ アプリケーションが表示されます\_ファイルと TYMED\_マルチページ\_ファイル、Windows Vista ドライバーを公開します。 ため TYMED\_コールバック、レガシ アプリケーションが表示されます、同じ形式のため TYMED、ドライバーが公開して\_例外が 1 つのファイル: 公開せずに**WiaImgFmt\_BMP**、互換性レイヤー公開**WiaImgFmt\_MEMORYBMP**レガシ アプリケーションにします。 これは、これには互換性レイヤー「切片」の呼び出しを持つ[ **IWiaMiniDrv::drvGetWiaFormatInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo)、Windows Vista ドライバーのすべてのフラグを追加し、\_ファイル形式 (で、例外の**WiaImgFmt\_BMP** /**WiaImgFmt\_MEMORYBMP**) ため TYMED\_コールバック。 最も重要なの互換性レイヤーでは、転送メッセージの Windows Vista と従来の転送メッセージには、そのストリームに書き込まれたデータを変換する独自の従来のコールバック オブジェクト、データ転送中に作成します。

TYMED 定数の詳細についてを参照してください[理解 TYMED](understanding-tymed.md)します。

互換レイヤーは、WIA COM プロキシで 2 つのコールバック オブジェクトを作成します。 コールバックのいずれかを転送し、転送ファイルのいずれか。 WIA COM プロキシの実装、 [IWiaTransferCallback インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiatransfercallback)します。 このコールバック オブジェクトは、ストリーム ベースの転送と「旧式」転送の間の変換で処理されます。 WIA 互換性レイヤーには、ドライバーの画像が互換性レイヤーのコールバック オブジェクトを渡してフィルターの処理も開始します。 したがって、イメージ処理のフィルターは、Windows Vista の転送と同様に、アプリケーションのコンテキストで実行常にされます。

次の図は、Windows Vista のドライバーとレガシ アプリケーションとの互換性レイヤーは連携を示しています。

![レガシ アプリケーションと windows vista ドライバー間データ転送を示す図](images/vistaapp-legacydrv.png)

WIA COM プロキシ内での従来のコールバック オブジェクトは、Windows Vista のメッセージの転送と従来の転送メッセージをストリームに書き込まれたデータに変換し、データ ファイルまたはコールバックの縞模様のデータを書き込みます。

ドライバーを呼び出すによって公開されるメソッドのいずれかと、 **IStream**インターフェイスから受信した、 [ **IWiaMiniDrvTransferCallback::GetNextStream** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvtransfercallback-getnextstream)メソッド (注、ドライバーはのみ呼び出す必要があります**IStream::Write**、 **IStream::Seek**、および**IStream::SetSize**)。 互換レイヤーがカスタムを作成するために、 **IStream**を単純にラップする実装、 **IStream** WIA COM プロキシを提供するインターフェイス。

従来のファイル転送は簡単です。 このような転送の例は、レガシ アプリケーションを呼び出すと**IWiaDataTransfer::idtGetData**します。 互換性レイヤーでは、アプリケーションを STGMEDIUM 構造体で指定するファイルにデータ ストリームを作成します。 このストリームはフィルターに渡される、ドライバーまたはイメージ処理を呼び出すときに[ **IWiaTransferCallback::GetNextStream** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nf-wia_lh-iwiatransfercallback-getnextstream)し、すべての転送メッセージは従来の転送メッセージを簡単にマップします。 メッセージにマップする方法の詳細については、次を参照してください。 [WIA 互換性レイヤーのデータ転送実装](wia-compatibility-layer-message-mapping.md)します。

呼び出すときに、 **IWiaDataTransfer::dtGetData メソッド**、互換性レイヤーでは、いくつかのより厳密なパラメーター チェックします。 互換レイヤーが呼び出し元を許可しないなど、 **IWiaDataTrasnfer::idtGetData**メソッド[TYMED\_ファイル](understanding-tymed.md)とするデータの転送し、上位のページ数がないです。呼び出すことが互換性レイヤーを利用、 **IWiaDataTrasnfer::idtGetData** TYMED メソッド\_ファイル カウントより大きなページがあると、1 つ。

従来のコールバックの転送はもう少し複雑です。 Windows Vista ドライバーがサポートされていないため**WiaImgFmt\_MEMORYBMP**、従来のドライバーに必要な互換性レイヤーのコールバック オブジェクトはからの変換を処理する必要があります**WiaImgFmt\_BMP**に**WiaImgFmt\_MEMORYBMP**します。 転送メッセージの間のマッピングも簡単にできません。 互換レイヤーは、独自のストリームの実装を作成します。 互換性レイヤー送信 IT\_MSG\_への呼び出し時に、アプリケーションのコールバックをデータ メッセージ、 **IStream::Write**アプリケーションによってメソッド。

変更ができるしなければ、 **IWiaTransfer** ; 互換性レイヤーの実装の一部としてインターフェイス関数は、 **IWiaTransfer::EnumWIA\_形式\_情報**に追加されます**IWiaTransfer**ため TYMED\_マルチページ\_ファイル転送。 この追加は互換性レイヤーの結果はありませんが必要なを取得することはできませんので、 **IWiaDataTransfer**からインターフェイス**IWiaTransfer**インターフェイスまたは、から**IWiaItem2**へのインターフェイス、 **IWiaItem**インターフェイス。

**IWiaDataTransfer**、 **IWiaTransfer**、 **IWiaItem**、 **IWiaItem2**、および**IStream**インターフェイスと STGMEDIUM 構造体は、Microsoft Windows SDK ドキュメントで説明します。

## <a name="related-topics"></a>関連トピック
[**IWiaMiniDrvTransferCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvtransfercallback)  



