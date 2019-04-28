---
title: フィルム スキャナー用基本スキャン
description: フィルム スキャナー用基本スキャン
ms.assetid: ca25c14d-120e-4e53-9d57-ba5663536bae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c055b8743eeb97b505a6f2daf8efc79232580dd8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373332"
---
# <a name="basic-scanning-for-film-scanners"></a>フィルム スキャナー用基本スキャン





WIA アプリケーションでは、スキャナーのサポートされる機能を判断するためのスキャナー項目ツリーの最上位のアイテムを列挙します。 次に、アプリケーションは、スキャンのソースとして、最上位の項目を使用します。 たとえば、フラット ベッド スキャナーの項目は、ベッドからスキャン使用され、フィーダーのアイテムがドキュメント フィーダーからスキャンするために使用されます。

プログラミングとフィルムの項目の動作のスキャンは、フラット ベッド項目のほとんどと同じです。

スキャナーのフィルムの項目をプログラムとは必ずしもこの順序で、アプリケーションは通常、次の操作に従います。

-   マークされている WIA 項目を検索、WIA の最上位項目を列挙、 **WiaItemTypeProgrammableDataSource**項目のフラグと[ **WIA\_IPA\_項目\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff551581) WIA の設定\_カテゴリ\_フィルム。

-   有効な値を読み取る[ **WIA\_IP\_フィルム\_スキャン\_モード**](https://msdn.microsoft.com/library/windows/hardware/ff552598)フィルムのスキャン設定を確認します。 この設定は正のイメージまたは負のイメージ (つまり、写真のネガ) のサポートのスキャンを示します。

-   正または負の光源を選択して、WIA を設定して\_IP\_フィルム\_スキャン\_モード プロパティです。

-   スキャナーの lamp の現在の設定を読み取るしを使用して必要な場合は、ランプを有効にする、 [ **WIA\_IP\_LAMP** ](https://msdn.microsoft.com/library/windows/hardware/ff552603)プロパティ (サポートされている) 場合。

-   有効な値を読み取る[ **WIA\_IPA\_TYMED** ](https://msdn.microsoft.com/library/windows/hardware/ff551656)と[ **WIA\_IPA\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff551553).

-   データの最終的な形式を選択して、WIA を設定して\_IPA\_FORMAT プロパティ。

-   イメージの設定を選択します[ **WIA\_IPA\_深さ**](https://msdn.microsoft.com/library/windows/hardware/ff551546)、 [ **WIA\_IPA\_DATATYPE**。 ](https://msdn.microsoft.com/library/windows/hardware/ff551543)、および[ **WIA\_IPA\_ビット\_1 秒あたり\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff551526)します。

-   (サポートされている) 場合は、1 つまたは複数ページを選択するには、WIA ファイル転送\_IPA\_TYMED プロパティ。

-   既存のフレームを検索する子アイテムを列挙します。

-   読み取り、 [ **WIA\_IP\_サポート\_子\_項目\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff552653)スキャナーが作成をサポートするかどうかを判断する項目新しいフレーム。

-   (フレームの作成のサポート) に応じて、新しいフレームを作成または既存のフィルム項目フレームを調整します。

-   読み取り、WIA\_IP\_をサポートしています\_子\_項目\_フィルム スキャナーの項目が、特別なフォルダーの取得機能をサポートしているかどうかを決定するプロパティを作成します。

-   次の操作のいずれかを実行します。
    -   WIA フィルム スキャナーの項目を (ではなく、フォルダーの取得機能を使用して) を使用してデータを転送します。 領域をスキャンする完全なフィルムが 1 つのイメージとして返されます。
    -   WIA フィルム スキャナーの項目を (機能を使用して、フォルダーの取得) を使用してデータを転送します。 WIA フィルム スキャナー子アイテムのみ (つまり、フレーム) は、アプリケーションに転送されます。
    -   フレームの各項目に移動し、その WIA 項目を転送します。

スキャンする単位をスキャンするスキャナーのフィルムを使用する場合、ドライバーは通常、次の操作を実行します。

1.  呼び出す[ **IWiaMiniDrv::drvValidateItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff545017)と[ **IWiaMiniDrv::drvReadItemProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545005)します。 WIA ドライバーでは、アプリケーションのプロパティの設定フェーズ中にプロパティの設定を検証する必要があります。

2.  呼び出す[ **IWiaMiniDrv::drvWriteItemProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545020)します。 渡される WIA コンテキスト アイテムは、フィルム スキャナーの項目または、ドライバーは、アプリケーションがスキャナーのフィルムの単位のスキャンを使用してスキャンすることを認識できるように、項目のフレームをスキャン フィルムに属しています。 スキャナーの機種によっては、フィルムをスキャンするため、flatbeds を使用します。 適切な照明のスキャナーを構成する必要があります (、WIA に基づいて\_IP\_フィルム\_スキャン\_モード プロパティ) とフィルムをスキャンするためのエクステント変更します。

3.  呼び出す[ **IWiaMiniDrv::drvAcquireItemData**](https://msdn.microsoft.com/library/windows/hardware/ff543956)します。 渡される WIA コンテキスト アイテムは、フィルム スキャナーの項目または項目のフレームをスキャンするフィルムに属しています。 ドライバーは、アプリケーションが単体のスキャン フィルムを使用してスキャンすることを簡単に判断できます。

4.  デバイスをプログラミングし、フィルムの単位を現在のフィルム項目プロパティ (子フレームのすべてのプロパティを含む) を使用してスキャンからスキャンします。 スキャン モード フィルムに WIA ドライバーがない場合は、スキャンは、このモードに切り替えるしようとします。 負と正のライトの間でのみ、アプリケーションを切り替えることができます。 アプリケーションとドライバーの間のコントラクトは、フィルム スキャナーの項目を使用してスキャンするにはデータ転送のフィルム スキャナーの機能のスキャンを使用することが一致します。

フィルム スキャナーの項目に配置されている WIA プロパティは、その設定として、スキャンの前に、スキャナーの一部をスキャンするフィルムに適用されるドライバーで使用する必要があります。 WIA ドライバーによって返されるデータのヘッダーを常に信頼するには、WIA アプリケーションが必要です。 たとえば、スキャナーは、指定したイメージの幅とニーズの値を丸めるでスキャンできませんを判断しました。 ドライバーは、アプリケーションが適切なデータがあるできるように更新された幅情報を使用してイメージのヘッダーを更新する必要があります。 WIA ドライバーでは、WIA プロパティのセットは、デバイスから返される実際のデータ情報を常に更新する必要があります。

 

 




