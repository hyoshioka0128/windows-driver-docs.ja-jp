---
title: セグメンテーション フィルターのインターフェイス
description: セグメンテーション フィルターのインターフェイス
ms.assetid: 428f6fce-d76c-4485-aa92-39f2b608160d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e033ca9312ea22e0eff8b874f85504ea551b005b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358898"
---
# <a name="interfaces-for-segmentation-filters"></a>セグメンテーション フィルターのインターフェイス





WIA は、Windows Vista 以降、セグメント化フィルターをサポートします。 セグメント化フィルターを実装する必要があります、 [IWiaSegmentationFilter インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff545035)します。

**IWiaSegmentationFilter**インターフェイスは、(Windows Vista) の新しいインターフェイスに依存**IWiaItem2**のスーパー セットは、このセクションでは、全体で使用される**IWiaItem**. 加え、 **IWiaItem** 、メソッド、 **IWiaItem2**インターフェイスには、メソッドが含まれています**IWiaItem2::GetExtension**、WIA を作成するアプリケーションで使用する。拡張機能、セグメント化フィルターなど。 **IWiaItem**と**IWiaItem2**インターフェイスが、Microsoft Windows SDK ドキュメントに記載されています。

**IWiaSegmentationFilter**インターフェイスが 1 つのメソッドを実装する**DetectRegions**します。 このメソッドは 3 つのパラメーター、 *lFlags*、 *pInputStream*、および*pWiaItem2*します。

*LFlags*パラメーターは現在使用されていません。

*PInputStream*パラメーターは、セグメント化を実行するイメージへのポインター。 通常これは、フラット ベッドのスキャンの表面全体を表すプレビュー イメージです。 アプリケーションにストリームが作成されたその**IWiaTransferCallback::GetNextStream**メソッド。 このメソッド画像を取得中に呼び出されます。 ドライバー、イメージを取得したデータ ストリームに書き込みますを**IWiaTransferCallback::GetNextStream**メソッドを返します。 これは、アプリケーションによってセグメント化のフィルターに渡す必要があるストリームです。 **IWiaTransferCallback**インターフェイスは、Windows SDK のドキュメントで説明します。

*PWiaItem2*パラメーターは、WIA アイテムへのポインター *pInputStream*取得されました。 親アイテムとも呼ばれます。 たとえば、項目を*pWiaItem2*へのポインターには、フラット ベッド項目可能性があります。

[ **IWiaSegmentationFilter::DetectRegions** ](https://msdn.microsoft.com/library/windows/hardware/ff545030)によって表されるイメージのサブ領域を判断するメソッドが使用される*pInputStream*します。 検出されると、各サブ地域の**IWiaSegmentationFilter::DetectRegions**によって示される項目の下に新しい子 WIA 項目を作成します。 *pWiaItem2*します。 各子項目のセグメント化、フィルターは、次の WIA プロパティの値を設定する必要があります。[**WIA\_IP\_XPOS**](https://msdn.microsoft.com/library/windows/hardware/ff552663)、 [ **WIA\_IP\_YPOS**](https://msdn.microsoft.com/library/windows/hardware/ff552671)、 [ **WIA\_IP\_XEXTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552661)、および[ **WIA\_IP\_YEXTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552669)します。 これらのプロパティは、スキャンする領域の外接する四角形を表します。 高度なセグメント化フィルターすることも、他の WIA プロパティを設定します。 [WIA プロパティ セグメント化フィルターを](wia-properties-for-segmentation-filters.md)デスキュー場合、ドライバーをサポートしています。

次の図は、セグメント化フィルターがアプリケーション項目のツリーを変更する方法を示します。 この図では、セグメント化フィルターが、ベッドで 3 つのイメージを検出し、イメージごとに、フラット ベッド項目の下に新しい子項目が作成します。

![セグメント化フィルターがアプリケーション項目のツリーを変更する方法を示す図](images/art-segmentation2.png)

セグメント化フィルターでは、拡張するドライバーでサポートされるすべてのイメージ形式をサポートする必要があります。 Microsoft が提供するセグメント化フィルターでは、BMP、GIF、JPEG、PNG、TIFF 形式をサポートします。 したがって、このフィルターを使用するすべてのドライバーは、これらの形式に制限されます。

セグメント化を子項目を作成するには、呼び出しをフィルター処理、 **IWiaItem2::CreateChildItem**メソッド。 このような呼び出しの例を次に示します。

```cpp
lItemFlags = WiaItemTypeGenerated | WiaItemTypeTransfer | WiaItemTypeImage | WiaItemTypeFile |
 WiaItemTypeProgrammableDataSource;

lCreationFlags = COPY_PARENT_PROPERTY_VALUES;

pWiaItem2->CreateChildItem(lItemFlags,
                           lCreationFlags,
                           bstrItemName,
                           &pChildItem);
```

**IWiaItem2::CreateChildItem**とは若干異なります**IWiaItem::CreateChildItem**します。 **IWiaItem2::CreateChildItem**メソッドが新しいパラメーター、 *lCreationFlags*;**IWiaItem2::CreateChildItem**メソッドの*lItemFlags*パラメーターに対応、 *lFlags*パラメーターの**IWiaItem:。CreateChildItem**します。 コピーを渡して\_親\_プロパティ\_値で、 *lCreationFlags*すべて読み取り/書き込み可能な設定を WIA サービスがサービスへのパラメーターの前のコード スニペットに示すわかります親のと同じ値に子項目の WIA プロパティ。 セグメント化フィルターは、このフラグを渡す必要があります理由は、イメージのフォーマットと新しく作成された子項目を解像度などのプロパティは、同じことを確認する親項目です。 解像度が同じである子項目にセグメント化フィルターを設定する範囲のプロパティが、画像の解像度に依存するために重要です。 イメージのフォーマットと解像度が同じである子項目にアプリケーションをプレビュー コンポーネント (Microsoft Windows SDK のドキュメントで説明) を使用する必要がある場合が重要です。 最終的なイメージを取得する前に、アプリケーションは、スキャナーから高品質のイメージを取得する解像度を変更できます。

セグメント化、フィルターは、できること確認と、実行できないことで、アプリケーションと同じ制約で連結する重要です。 これは、アプリケーションが、セグメント化フィルターを作成する子項目を変更できることを意味します。 たとえば、ユーザー可能性がある満たされていない領域にセグメント化フィルターが検出され、その角をドラッグしてこのリージョンを変更するには、アプリケーションを調べることができます。 アプリケーションできますもセグメント化フィルターによって作成された子項目を削除するだけでなく新しいものを追加します。

セグメント化フィルターが作成した子項目を「クリーンアップ」責任を負うことに注意してください。 そのため、アプリケーションを呼び出す場合**IWiaSegmentationFilter::DetectRegions**複数回、アプリケーションには最初の呼び出しで作成された子アイテムが削除する必要があります最初、 **IWiaSegmentationFilter::DetectRegions**メソッド。 セグメント化フィルターがリセットを担当することも、 *pInputStream*パラメーター。 アプリケーションでは、セグメント化フィルターを呼び出す前に、ストリームの先頭にシーク ポインターを設定したことを確認する必要があります。

フィルム項目と、フラット ベッド項目にのみ、セグメント化フィルターを使用してください。 フィルムをスキャンするため、スキャナーはよく固定のフレームを持つ場合ドライバーを作成、子項目 (を参照してください[WIA スキャナー項目のツリー レイアウト](wia-scanner-item-tree-layout.md)詳細については)。 この場合、アプリケーションでは領域の検出および子項目の作成のセグメント化フィルターを呼び出す必要がありますされません。

セグメント化フィルターを使用した場合、ドライバーを実装しなければなりません、 [ **WIA\_IP\_セグメンテーション**](https://msdn.microsoft.com/library/windows/hardware/ff552649)ベッドと映画 WIA アイテムのプロパティ。 この読み取り専用プロパティでは、2 つの有効な値があります。WIA\_使用\_セグメンテーション\_フィルターと WIA\_不要\_使用\_セグメンテーション\_フィルターで、ドライバーの設定。 このプロパティは、特定の項目領域の検出に、ドライバーのセグメント化フィルターを使用する場合、アプリケーションを使用できます。

スキャナーは、フィルムをスキャンするため、固定のフレームを使用している場合、このプロパティを設定 WIA を\_不要\_使用\_セグメンテーション\_フィルム項目フィルター。 この場合、アプリケーションを試みるのでフィルムのプレビューが取得されたされた後、セグメント化フィルターを読み込む代わりに、ドライバーによって作成された子アイテムが列挙にする必要があります。 これらの子項目は、固定のフレームを表します。

WIA 項目に渡されるため、 **IWiaSegmentationFilter::DetectRegions**、セグメント化フィルターの項目、つまり、フラット ベッドまたはフィルムのカテゴリによって異なるアルゴリズムを使用することができます。 項目のカテゴリが格納されている、 [ **WIA\_IPA\_項目\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff551581)プロパティ。

アプリケーションで任意のプロパティが変更された場合*pWiaItem2*間でイメージを取得する*pInputStream*アプリケーションの呼び出しと**IWiaSegmentationFilter::DetectRegions**、元のプロパティ設定 (つまり、項目が、ストリームが取得されたときにプロパティ設定) を復元する必要があります。 これを使用して、 **IWiaPropertyStorage::GetPropertyStream**と**IWiaPropertyStorage::SetPropertyStream**メソッド。 これらの変更を復元する必要がある理由は、セグメント化フィルターでは、必要なのですが、いないイメージ ヘッダーに格納されている、WIA 項目内の情報があることです。 このような情報の例としてに格納されたデータ、 [ **WIA\_IP\_XPOS**](https://msdn.microsoft.com/library/windows/hardware/ff552663)、 [ **WIA\_IP\_YPOS** ](https://msdn.microsoft.com/library/windows/hardware/ff552671)、および[ **WIA\_IP\_回転**](https://msdn.microsoft.com/library/windows/hardware/ff552648)プロパティ。 **IWiaPropertyStorage**インターフェイスとそのメソッドは、Windows SDK のドキュメントで説明します。

アプリケーションで呼び出すことによって、セグメント化フィルターのインスタンスを取得**IWiaItem2::GetExtension** (Windows SDK のドキュメントで説明)。 通常、アプリケーションは、プレビュー ウィンドウを表示する前にこのメソッドを呼び出します。 これは、ドライバーがなど、サポートされていないボタンを表示しないように知っておく必要が、UI の場合、セグメント化フィルターに付属していないため**実行セグメント化**します。

 

 




