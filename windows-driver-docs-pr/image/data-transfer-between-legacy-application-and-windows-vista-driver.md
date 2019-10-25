---
title: レガシ アプリケーションと Windows Vista ドライバー間のデータ転送
description: レガシ アプリケーションと Windows Vista ドライバー間のデータ転送
ms.assetid: 83817277-3526-4f64-8e7c-7e02c8cd77bd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05f67fd84e93d8c7662adf7c2ce69c59dc2b4c6a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840861"
---
# <a name="data-transfer-between-legacy-application-and-windows-vista-driver"></a>レガシ アプリケーションと Windows Vista ドライバー間のデータ転送


互換性レイヤーでは、ドライバーのイメージ処理フィルターが常に呼び出されるようにする必要があります。また、 **LocalService**アカウントを明示的にサポートしていないレガシアプリケーションでも、データ転送を実行できます。 **LocalService**アカウントは、MICROSOFT Windows XP 以降のオペレーティングシステムで使用できます。

レガシドライバーは、少なくとも、TYMED\_ファイルと TYMED\_コールバックの両方を公開する必要があります。ただし、Windows Vista のドライバーは、TYMED\_コールバック (または TYMED\_のマルチページ\_コールバック) を公開しません。 互換性レイヤーの転送部分では、レガシアプリケーションが、Windows Vista ドライバーによって実装されていなくても、TYMED\_コールバックを参照するようにします。 TYMED\_マルチページ\_コールバックは、Windows Vista ドライバーからは公開されません。

レガシアプリケーションでは、Windows Vista ドライバーによって公開されている、\_のマルチページ\_ファイルに対してサポートされている形式が表示されます\_。 TYMED\_コールバックの場合、レガシアプリケーションでは、ドライバーが TYMED\_ファイル用に公開するのと同じ形式が使用されます。ただし、例外が1つあります。 **wiaimgfmt\_BMP**を公開する代わりに、互換性レイヤーは**Wiaimgfmt を公開します\_MEMORYBMP**をレガシアプリケーションに適用します。 これを行うには、互換性レイヤーを使用して[**IWiaMiniDrv::D rvgetwiaformatinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo)に対する呼び出しを "インターセプト" し、すべての Windows Vista ドライバーの TYMED\_ファイル形式を追加します ( **Wiaimgfmt\_BMP**は除き /**Wiaimgfmt\_MEMORYBMP**)TYMED\_コールバックの場合。 ほとんどの場合、互換性レイヤーは、データ転送時に独自のレガシコールバックオブジェクトを作成します。これにより、Windows Vista 転送メッセージとストリームに書き込まれたデータが従来の転送メッセージに変換されます。

TYMED 定数の詳細については、「 [TYMED](understanding-tymed.md)について」を参照してください。

互換性レイヤーでは、2つのコールバックオブジェクトが WIA COM プロキシに作成されます。1つはコールバック転送用で、もう1つはファイル転送用です。 WIA COM プロキシは、 [Iwiatransのコールバックインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiatransfercallback)を実装します。 このコールバックオブジェクトは、ストリームベースの転送と "旧形式の" 転送の間の変換を処理します。 また、WIA 互換レイヤーでは、互換性レイヤーのコールバックオブジェクトに渡されるドライバーのイメージ処理フィルターが開始されます。 そのため、イメージ処理フィルターは、Windows Vista 転送と同様に、常にアプリケーションのコンテキストで実行されます。

次の図は、互換性レイヤーが Windows Vista ドライバーとレガシアプリケーションでどのように機能するかを示しています。

![レガシアプリケーションと windows vista ドライバー間のデータ転送を示す図](images/vistaapp-legacydrv.png)

WIA COM プロキシ内のレガシコールバックオブジェクトは、Windows Vista 転送メッセージとストリームに書き込まれたデータを従来の転送メッセージに変換し、データをファイルまたは帯状データコールバックに書き込みます。

ドライバーが、 [**IWiaMiniDrvTransferCallback:: GetNextStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvtransfercallback-getnextstream)メソッドから受信した**istream**インターフェイスによって公開されているメソッドを呼び出す場合 (注: ドライバーは**istream:: Write**、 **istream:: Seek**のみを呼び出す必要があります。**IStream:: SetSize**)。 このため、互換性レイヤーは、WIA COM プロキシが提供する**istream**インターフェイスを単にラップするカスタム**istream**実装を作成します。

レガシファイル転送は簡単です。 このような転送の例として、レガシアプリケーションが**IWiaDataTransfer:: idtGetData**を呼び出す場合があります。 互換性レイヤーは、STGMEDIUM 構造体でアプリケーションによって指定されたデータストリームをファイルに作成します。 このストリームは、 [**Iwiatransfercallback:: GetNextStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiatransfercallback-getnextstream)を呼び出すときにドライバーまたはイメージ処理フィルターに渡され、すべての転送メッセージが従来の転送メッセージに簡単にマップされます。 メッセージがどのようにマップされるかの詳細については、「 [WIA Compatibility Layer データ転送の実装](wia-compatibility-layer-message-mapping.md)」を参照してください。

**IWiaDataTransfer::D tGetData メソッド**を呼び出すと、互換性レイヤーはより厳密なパラメーターチェックを実行します。 たとえば、互換性レイヤーでは、 [Tymed\_ファイル](understanding-tymed.md)では**IWiaDataTrasnfer:: idtGetData**メソッドを呼び出すことができません。また、ページ数は、互換性レイヤーを使用しないデータ転送に含まれています。**IWiaDataTrasnfer:: idtGetData**メソッドと TYMED\_ファイルがあり、1つ大きいページ数が含まれています。

従来のコールバック転送は少し複雑です。 Windows Vista ドライバーでは、レガシドライバーに必要な**wiaimgfmt\_MEMORYBMP**がサポートされていないため、互換性レイヤーのコールバックオブジェクトは**wiaimgfmt\_BMP**から wiaimgfmt への変換を処理する必要があり **\_MEMORYBMP**。 また、転送メッセージ間のマッピングも簡単ではありません。 互換性レイヤーによって独自のストリーム実装が作成されます。 互換性レイヤーは、アプリケーションによる**IStream:: Write**メソッドの呼び出し時に、アプリケーションのコールバックに MSG\_データメッセージ\_送信します。

互換性レイヤーの実装の一部として、 **IWiaTransfer**インターフェイスに変更を加える必要がありました。関数**IWiaTransfer:: EnumWIA\_FORMAT\_INFO**が**IWiaTransfer**に追加され、TYMED\_マルチページ\_ファイル転送が可能になります。 この追加は互換性レイヤーの結果ではありませんが、 **IWiaTransfer**インターフェイスから**IWiaDataTransfer**インターフェイスを取得したり、 **IWiaItem2**インターフェイスから**iwiaitem**にアクセスしたりすることはできないため、必要になります。efi.

**IWiaDataTransfer**、 **IWiaTransfer**、 **iwiaitem**、 **IWiaItem2**、および**IStream**の各インターフェイスと STGMEDIUM 構造体については Microsoft Windows SDK のドキュメントで説明します。

## <a name="related-topics"></a>関連トピック
[**IWiaMiniDrvTransferCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrvtransfercallback)  



