---
title: フラットベッドスキャナーの基本的なスキャン
description: フラットベッドスキャナーの基本的なスキャン
ms.assetid: a1100a8d-752a-4109-b1dc-cf7c4bf5a100
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 429bca95d77a8a80a8615382e99b2bc53190c0b2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840888"
---
# <a name="basic-scanning-for-flatbed-scanners"></a>フラットベッドスキャナーの基本的なスキャン





WIA アプリケーションは、スキャナーの項目ツリーのルート項目と最上位の子項目を列挙して、スキャナーのサポートされている機能を判別します。 次に、アプリケーションはこの子項目をスキャンソースとして使用します。 たとえば、フラットベッドスキャナーの項目は、フラットベッドからのスキャンに使用されます。一方、フィーダー項目はドキュメントフィーダーからのスキャンに使用されます。

Windows Vista のフラットベッド項目のプログラミング動作とスキャン動作は、Windows XP および Windows Me で使用されるオーバーロードシステムと同じです。 このオーバーロードシステムは、すべての WIA 属性フラグを項目ツリー内の最初の子項目に対してプログラムします。

通常、アプリケーションは、スキャナーのフラットベッドをプログラムするときに、次の操作を実行しますが、必ずしもこの順序ではありません。

-   最上位レベルの WIA 項目を列挙し、 **WiaItemTypeProgrammableDataSource** item フラグでマークされた項目を探します。また、 [**wia\_IPA\_item\_CATEGORY**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)プロパティを WIA\_category\_フラットベッドに設定します。

-   [**Wia\_IPA\_TYMED**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)および[**wia\_IPA\_形式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)のプロパティの有効な値を確認します。

-   WIA\_IPA\_TYMED プロパティを設定して、メモリ転送またはファイル転送の種類を選択します。 使用できる転送の種類の詳細については、「[データ転送](data-transfers.md)」を参照してください。 **IStream**ベースの転送の場合、WIA\_IPA\_tymed は既定で tymed\_ファイルに設定されます。変更することはできません。

-   [WIA\_IPA\_形式] プロパティを設定して、データの最終的な形式を選択します。

-   画像の設定 ( [**wia\_IPA\_DEPTH**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth) 、 [**wia\_IPA\_DATATYPE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)など) を選択します。

-   この WIA 項目を使用してデータを転送します。

ドライバーは通常、スキャナーのフラットベッドを使用してスキャンするときに、次の操作を実行します。

1.  [**IWiaMiniDrv::D rvvalidateitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)と[**IWiaMiniDrv::d rvreaditemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)を呼び出します。 WIA ドライバーは、アプリケーションのプロパティ設定フェーズ中にプロパティ設定を検証する必要があります。

2.  [**IWiaMiniDrv::D rvwriteitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)を呼び出します。 渡された WIA 項目コンテキストは、アプリケーションがスキャナーのフラットベッドを使用してスキャンすることを認識するように、フラットベッドスキャナー項目に属しています。

3.  [**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)を呼び出します。 渡された WIA 項目コンテキストは、フラットベッドスキャナー項目に属しているので、ドライバーは、アプリケーションがフラットなガラスを使用してスキャンすることを簡単に判断できます。

4.  現在のフラットベッド項目のプロパティを使用して、デバイスをプログラムし、フラットベッドからスキャンします。 WIA ドライバーがフラットベッドスキャンモードでない場合は、スキャン用にこのモードに切り替えようとします。 アプリケーションがフラットベッドを使用するように切り替える特別な設定はありません。 フラットベッド項目を使用したスキャンは、アプリケーションとドライバーの間のコントラクトです。データ転送には、フラットベッドを使用することに同意します。

ドライバーは、スキャンの前にスキャナーのフラットベッド部分に適用する設定として、フラットベッドスキャナー項目の WIA プロパティを使用する必要があります。 Wia アプリケーションは、WIA ドライバーによって返されるデータのヘッダーを常に信頼する必要があります。 たとえば、スキャナーが、指定された幅の画像をスキャンできないと判断し、その結果、スキャン可能な幅に値を丸める場合、ドライバーは、変更された幅情報でイメージヘッダーを更新する必要があります。 この更新により、アプリケーションで正しい情報を使用できるようになります。 WIA ドライバーは、デバイスから返された実際の情報を使用して、WIA のプロパティを更新しようとします。

### <a name="advanced-scanning-for-flatbed-scanners"></a>フラットベッドスキャナーの高度なスキャン

フラットベッドからのマルチリージョンスキャンは、手動で構成することも、 [WIA のセグメンテーションフィルター](wia-segmentation-filter.md)を使用して自動的に行うこともできます。 セグメンテーションフィルターは、アプリケーションとの違いはありませんが、このような処理を実行できないことに注意してください。 セグメンテーションフィルターについて説明されているのと同じ手順をアプリケーションで直接実行して、新しいスキャン領域の子項目を作成することもできます。

 

 




