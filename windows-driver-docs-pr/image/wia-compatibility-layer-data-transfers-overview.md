---
title: WIA 互換性レイヤーのデータ転送の概要
description: WIA 互換性レイヤーのデータ転送の概要
ms.assetid: 4c88474e-f776-4876-a15f-c9d6fb0d20e5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72dd82a8b3253e6ccd432aa83c348a7abb0a67eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840722"
---
# <a name="wia-compatibility-layer-data-transfers-overview"></a>WIA 互換性レイヤーのデータ転送の概要


転送互換性レイヤーがない場合、Windows Vista WIA ドライバーは、レガシおよび Windows Vista アプリケーションからのデータ転送を実行するために、TYMED とストリームベースのデータ転送スタイルの両方を実装する必要がありました。 同様に、Windows Vista WIA アプリケーションでは、レガシおよび Windows Vista ドライバーからのデータ転送を実行できるようにするために、(コールバック実装が異なる) 両方の転送スタイルを実装する必要がありました。 WIA 互換性レイヤーでは、ドライバーの種類は WIA アプリケーションに対して透過的であり、Windows Vista WIA ドライバーは従来の転送コードを処理する必要はありません。

互換性レイヤーが必要とされる転送ケースは2つあります。これらはそれぞれ、次の2つのサブカテゴリに分類できます。

1.  Windows Vista ドライバーからデータを転送するレガシアプリケーション:
    1.  ファイル転送: アプリケーションは**IWiaDataTransfer:: idtGetBandedData**を呼び出します。
    2.  コールバックの転送: アプリケーションは**IWiaDataTransfer:: idtGetData**を呼び出します。

2.  レガシドライバーからデータを転送する Windows Vista アプリケーション:
    1.  ファイル転送: 互換性レイヤーは、レガシドライバーを使用したファイル転送を開始します。
    2.  コールバック転送: 互換性レイヤーは、レガシドライバーを使用してコールバック転送を開始します。

互換性レイヤーを使用するかどうかを判断するための最初の手順は、WIA ドライバーが Windows Vista ドライバーであるか、レガシドライバーであるかを判断することです。 このことは、WIA サービスによって、ドライバーが[**Iws-at usd:: GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities)から返すバージョン番号を確認することによって決定されます。 レガシドライバーは、バージョン番号の STI\_バージョンを返します。一方、Windows Vista ドライバーは、STI\_バージョン\_3 を返す必要があります。 このバージョン番号は、Windows Vista プロパティ、WIA\_DIP\_STI\_ドライバー\_バージョンの wia COM プロキシ (および WIA アプリケーション) に公開されます。

互換性レイヤーを使用するかどうかを判断するための次の手順は、アプリケーションが Windows Vista WIA アプリケーションであるか、レガシ WIA アプリケーションであるかを判断することです。アプリケーションが**IWiaDataTransfer:: idtGetBandedData** **を呼び出すか、IWiaDataTransfer:: idtGetData**これは従来の wia アプリケーションです。アプリケーションが**IWiaTransfer::D o)** を呼び出した場合、これは WINDOWS Vista の wia アプリケーションです。

新しいストリームベースのデータ転送モデルを使用すると、WIA サービスでは、TYMED\_コールバックと TYMED\_ファイル (または、TYMED\_マルチページ\_コールバックと TYMED\_マルチページ\_ファイル) が区別されなくなります。 代わりに、\_ファイルと TYMED\_のマルチページ\_ファイルのみが存在します。 ドライバーがマルチページ TIFF (または PDF) スキャンをサポートできるようにするには、TYMED\_マルチページ\_ファイルが必要です。 TYMED 定数の詳細については、「 [TYMED](understanding-tymed.md)について」を参照してください。

Windows Vista ドライバーでは、WIA ではメモリビットマップ形式**Wiaimgfmt\_MEMORYBMP**はサポートされません。

Windows Vista ドライバーでは、更新メッセージを送信してデータを転送し、転送中にイメージ全体をキャッシュすることができます。 この形式の転送は、スキャン中にデータを転送する場合に便利です。たとえば、スクロールフィードスキャナーを使用したスキャンなど、転送される画像のサイズをすぐに判断できない場合です。 イメージデータをバンドで転送するには、ドライバーは[**Iwiatransfercallback:: GetNextStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiatransfercallback-getnextstream)で渡されたストリームに対して**IStream:: Seek**を呼び出す必要があります。

TYMED とストリームベースの転送の詳細については、「[データ転送](data-transfers.md)」を参照してください。

**IWiaDataTransfer**、 **IWiaTransfer**、および**IStream**の各インターフェイスについては、Microsoft Windows SDK のドキュメントで説明します。

 

 




