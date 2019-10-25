---
title: セグメンテーションフィルターのインターフェイス
description: セグメンテーションフィルターのインターフェイス
ms.assetid: 428f6fce-d76c-4485-aa92-39f2b608160d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97309c6a71bbfb1eddbf8158e9882ec4f1ddb377
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840812"
---
# <a name="interfaces-for-segmentation-filters"></a>セグメンテーションフィルターのインターフェイス





Windows Vista 以降では、WIA でセグメンテーションフィルターがサポートされるようになります。 セグメンテーションフィルターでは、 [IWiaSegmentationFilter インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiasegmentationfilter)を実装する必要があります。

**IWiaSegmentationFilter**インターフェイスは、このセクション全体で使用される new (For Windows Vista) インターフェイス**IWiaItem2**に依存しています。これは**iwiaitem**のスーパーセットです。 **Iwiaitem**メソッドに加えて、 **IWiaItem2**インターフェイスには、 **IWiaItem2:: getextension**というメソッドが含まれています。これは、アプリケーションがセグメンテーションフィルターを含む WIA 拡張機能を作成するために使用します。 **Iwiaitem**インターフェイスと**IWiaItem2**インターフェイスについては、Microsoft Windows SDK のドキュメントを参照してください。

**IWiaSegmentationFilter**インターフェイスは、1つのメソッドである検出**領域**を実装します。 このメソッドには、 *Lflags*、 *pinputstream*、および*pWiaItem2*という3つのパラメーターがあります。

*Lflags*パラメーターは現在使用されていません。

*Pinputstream*パラメーターは、セグメント化を実行するイメージへのポインターです。 通常、これは、フラットベッドのスキャンサーフェイス全体を表すプレビューイメージです。 ストリームは、アプリケーションによって**Iwiatransfercallback:: GetNextStream**メソッドに作成されます。このメソッドは、イメージの取得中に呼び出されます。 ドライバーは、取得したイメージデータを**Iwiatransの callback:: GetNextStream**メソッドが返すストリームに書き込みます。 これは、アプリケーションによってセグメンテーションフィルターに渡されるストリームでもあります。 **Iwiatransのコールバック**インターフェイスについては、Windows SDK のドキュメントを参照してください。

*PWiaItem2*パラメーターは、 *pinputstream*が取得された WIA 項目へのポインターです。 親項目とも呼ばれます。 たとえば、 *pWiaItem2*が指す項目は、フラットな項目である可能性があります。

[**IWiaSegmentationFilter::D Etピン領域**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiasegmentationfilter-detectregions)メソッドは、 *pinputstream*によって表されるイメージの地区を決定するために使用されます。 検出された各サブ領域について、 **IWiaSegmentationFilter::D etが**、 *pWiaItem2*が指す項目の下に新しい子の WIA 項目を作成します。 セグメンテーションフィルターでは、各子項目について、次の WIA プロパティの値を設定する必要があります。 [**wia\_ips\_XPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)、 [**wia\_ip\_YPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)、 [**WIA\_ip\_xextent**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xextent)、および[**wia\_IP\_YEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yextent)。 これらのプロパティは、スキャンする領域の外接する四角形を表します。 さらに高度なセグメンテーションフィルターでは、ドライバーで deskewing がサポートされている場合に、[セグメンテーションフィルターの Wia プロパティ](wia-properties-for-segmentation-filters.md)など、他の wia プロパティを設定することもできます。

次の図は、セグメント化フィルターによってアプリケーション項目ツリーがどのように変更されるかを示しています。 この図では、セグメント化フィルターによって、フラット化された3つのイメージが検出され、各イメージに対して、フラット化された項目の下に新しい子項目が作成されています。

![セグメンテーションフィルターによってアプリケーション項目ツリーがどのように変更されるかを示す図](images/art-segmentation2.png)

セグメンテーションフィルターでは、拡張するドライバーでサポートされているすべてのイメージ形式をサポートする必要があります。 Microsoft が提供するセグメンテーションフィルターでは、BMP、GIF、JPEG、PNG、TIFF の各形式がサポートされています。 このため、このフィルターを使用するドライバーは、これらの形式に制限されます。

子項目を作成するために、セグメンテーションフィルターは**IWiaItem2:: CreateChildItem**メソッドを呼び出します。 このような呼び出しの例を次に示します。

```cpp
lItemFlags = WiaItemTypeGenerated | WiaItemTypeTransfer | WiaItemTypeImage | WiaItemTypeFile |
 WiaItemTypeProgrammableDataSource;

lCreationFlags = COPY_PARENT_PROPERTY_VALUES;

pWiaItem2->CreateChildItem(lItemFlags,
                           lCreationFlags,
                           bstrItemName,
                           &pChildItem);
```

**IWiaItem2:: CreateChildItem**は、 **Iwiaitem:: CreateChildItem**とは若干異なります。 **IWiaItem2:: CreateChildItem**メソッドに新しいパラメーター、 *l flags*があります。**IWiaItem2:: CreateChildItem**メソッドの*lItemFlags*パラメーターは、 **Iwiaitem:: CreateChildItem**の*lflags*パラメーターに対応しています。 前のコードスニペットに示されているように、コピー\_親\_プロパティ\_値を、 *Lのフラグ*パラメーターを持つ値として wia サービスに渡すと、子項目の読み取り可能または書き込み可能なすべての WIA プロパティがに設定されます。親のと同じ値です。 セグメンテーションフィルターがこのフラグを渡す理由は、新しく作成された子項目のイメージ形式や解像度などのプロパティが親項目としてであることを確認するためです。 セグメント化フィルターによって子項目に設定されるエクステントプロパティは、イメージの解像度に依存しているため、解決方法が同じであることが重要です。 また、アプリケーションでプレビューコンポーネント (Microsoft Windows SDK のドキュメントで説明されています) を使用する場合は、イメージの形式と解像度が子項目でも同じであることが重要です。 アプリケーションでは、最終的なイメージを取得する前に、スキャナーから品質の高いイメージを取得するように解像度を変更できます。

セグメンテーションフィルターは、アプリケーションと同じ制限によって制約され、実行できないことに注意する必要があります。 これは、アプリケーションがセグメンテーションフィルターによって作成される子項目を変更できることを意味します。 たとえば、セグメンテーションフィルターによって検出された領域でユーザーが満足されていない場合や、その領域をドラッグしてこの領域を変更するようにアプリケーションに指示する場合があります。 アプリケーションでは、セグメンテーションフィルターによって作成された子項目を削除したり、新しい子項目を追加したりすることもできます。

セグメンテーションフィルターでは、作成した子項目の "クリーンアップ" は行われないことに注意してください。 そのため、アプリケーションが**IWiaSegmentationFilter::D Etて region**を複数回呼び出す場合、アプリケーションは最初に**IWiaSegmentationFilter::D et region**メソッドの呼び出しで作成された子項目を削除する必要があります。 また、セグメント化フィルターは、 *Pinputstream*パラメーターのリセットも行いません。 アプリケーションでは、セグメント化フィルターを呼び出す前に、ストリームの先頭にシークポインターが設定されていることを確認する必要があります。

セグメンテーションフィルターは、フィルム項目とフラット化項目でのみ使用する必要があります。 フィルムスキャンでは、多くの場合、スキャナーに固定フレームが付属しています。この場合、ドライバーは子項目を作成します (詳細については、「 [WIA スキャナーの項目ツリーのレイアウト](wia-scanner-item-tree-layout.md)」を参照してください)。 この場合、アプリケーションでは、領域の検出と子項目の作成にセグメンテーションフィルターを呼び出すことはできません。

ドライバーにセグメンテーションフィルターが付属している場合は、そのフラットベッドおよびフィルムの WIA 項目に対して、 [**wia\_ip\_セグメンテーション**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-segmentation)プロパティを実装する必要があります。 この読み取り専用プロパティには、次の2つの有効な値があります。 WIA\_使用\_セグメンテーション\_フィルターおよび WIA\_、ドライバーが設定する\_のセグメンテーション\_フィルターを使用\_ません。 このプロパティを使用すると、特定の項目の地域の検出にドライバーのセグメンテーションフィルターを使用する必要があるかどうかをアプリケーションが認識できます。

スキャナーがフィルムスキャン用に固定フレームを使用している場合、このプロパティを [WIA] に設定すると、フィルム項目内のフィルター\_フィルター\_使用\_\_ません。 この場合、フィルムプレビューを取得した後、アプリケーションはセグメンテーションフィルターを読み込もうとしないでください。代わりに、ドライバーによって作成された子項目を列挙する必要があります。 これらの子項目は、固定フレームを表します。

WIA 項目は**IWiaSegmentationFilter::D Etて region**に渡されるため、セグメントフィルターでは、アイテムのカテゴリ (つまり、フラットベッドやフィルム) に応じて異なるアルゴリズムを使用することができます。 項目のカテゴリは、 [**WIA\_IPA\_item\_category**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)プロパティに格納されます。

アプリケーションが*pWiaItem2*のプロパティを変更した場合、 *pinputstream*のイメージを取得してから、アプリケーションの**IWiaSegmentationFilter::D etピン留め region**に対する呼び出し (プロパティの設定など) を変更します。項目は、ストリームが取得されたとき) を復元する必要があります。 これを行うには、 **Iwiapropertystorage:: getpropertystream**メソッドと**Iwiapropertystorage:: setpropertystream**メソッドを使用します。 これらの変更を復元する必要がある理由は、セグメント化フィルターに必要な情報が WIA 項目に含まれていても、イメージヘッダーに格納されていないことです。 このような情報の例としては、 [**wia\_ips\_XPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)、 [**wia\_ips\_YPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)、および[**wia\_ip\_ローテーション**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-rotation)の各プロパティに格納されているデータなどがあります。 **Iwiapropertystorage**インターフェイスとそのメソッドについては、Windows SDK のドキュメントを参照してください。

アプリケーションは、 **IWiaItem2:: GetExtension** (Windows SDK のドキュメントで説明) を呼び出すことによって、セグメンテーションフィルターのインスタンスを取得します。 通常、アプリケーションは、プレビューウィンドウを表示する前にこのメソッドを呼び出します。 これは、ドライバーにセグメンテーションフィルターが適用されていない可能性があるためです。この場合、UI は、セグメント化の**実行**など、サポートされていないボタンを表示しないことを認識している必要があります。

 

 




