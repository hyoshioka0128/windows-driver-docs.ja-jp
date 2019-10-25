---
title: フィルムスキャナーの基本的なスキャン
description: フィルムスキャナーの基本的なスキャン
ms.assetid: ca25c14d-120e-4e53-9d57-ba5663536bae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: beaf60e61309798c8810a1e0afd07aea39578d75
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840890"
---
# <a name="basic-scanning-for-film-scanners"></a>フィルムスキャナーの基本的なスキャン





WIA アプリケーションは、スキャナーの項目ツリーの最上位項目を列挙して、スキャナーのサポートされている機能を判別します。 その後、アプリケーションは最上位レベルの項目をスキャンソースとして使用します。 たとえば、フラットベッドスキャナーの項目は、フラットベッドからのスキャンに使用され、フィーダー項目はドキュメントフィーダーからのスキャンに使用されます。

フィルム項目のプログラミング動作とスキャン動作は、フラットな項目の動作とほぼ同じです。

通常、アプリケーションは、スキャナーのフィルム項目をプログラムするときに次の操作を実行しますが、必ずしもこの順序ではありません。

-   最上位レベルの WIA 項目を列挙し、 **WiaItemTypeProgrammableDataSource** item フラグでマークされている wia 項目を検索します。また、WIA\_カテゴリ\_フィルムの\_カテゴリ設定を使用して、WIA [ **\_IPA\_項目**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)を検索します。

-   フィルムスキャンの設定を確認するには、 [**WIA\_ip\_フィルム\_スキャン\_モード**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-film-scan-mode)の有効な値を確認します。 この設定は、ポジ画像またはネガ画像 (つまり、写真ネガ) のスキャンサポートを示します。

-   [WIA\_IP\_フィルム\_スキャン\_モード] プロパティを設定して、正または負の光源を選択します。

-   スキャナーランプの現在の設定を読み取り、必要に応じて、WIA の [ [ **\_ip\_ランプ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-lamp)] プロパティ (サポートされている場合) を使用して、ランプをオンにします。

-   [**Wia\_IPA\_TYMED**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)および[**wia\_IPA\_形式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)の有効な値を確認します。

-   [WIA\_IPA\_形式] プロパティを設定して、データの最終的な形式を選択します。

-   画像の設定を選択します。たとえば、 [**wia\_IPA\_DEPTH**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)、 [**wia\_IPA\_DATATYPE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)、 [**WIA\_IPA\_\_チャネルあたりのビット数**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-bits-per-channel)\_です。

-   WIA\_IPA\_TYMED プロパティを設定して、1つまたは複数ページ (サポートされている場合) のファイル転送を選択します。

-   子項目を列挙して既存のフレームを検索します。

-   新しいフレームの作成がスキャナーでサポートされているかどうかを判断するには[ **\_子\_項目\_作成項目をサポートする WIA\_ip\_** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-supports-child-item-creation)を読み取ります。

-   既存のフィルム項目のフレームを調整するか、新しいフレームを作成します (フレーム作成のサポートによって異なります)。

-   \_子\_項目\_作成プロパティをサポートしている WIA\_IP\_を読み取り、フィルムスキャナー項目が特別なフォルダー取得機能をサポートしているかどうかを確認します。

-   次のいずれかの操作を実行します。
    -   (フォルダー取得機能を使用せずに) WIA フィルムスキャナー項目を使用してデータを転送します。 フルフィルムスキャン領域は、1つのイメージとして返されます。
    -   (フォルダー取得機能を使用して) [WIA フィルムスキャナー] 項目を使用してデータを転送します。 アプリケーションに転送されるのは、WIA フィルムスキャナーの子項目 (フレーム) だけです。
    -   各フレーム項目に移動し、その WIA 項目を転送します。

ドライバーは通常、スキャナーのフィルムスキャンユニットを使用してスキャンするときに、次の操作を実行します。

1.  [**IWiaMiniDrv::D rvvalidateitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)と[**IWiaMiniDrv::d rvreaditemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)を呼び出します。 WIA ドライバーは、アプリケーションのプロパティ設定フェーズ中にプロパティ設定を検証する必要があります。

2.  [**IWiaMiniDrv::D rvwriteitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)を呼び出します。 渡された WIA 項目コンテキストは、フィルムスキャナー項目またはフィルムスキャン項目フレームに属しているため、アプリケーションがスキャンするためにスキャナーのフィルムスキャンユニットを使用することが認識されます。 一部のスキャナーでは、フィルムスキャンに flatbeds を使用しています。 スキャナーは、(WIA\_IP\_フィルム\_スキャン\_モード プロパティに基づいて) 適切な照明を構成し、フィルムスキャンのために変更を行う必要があります。

3.  [**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)を呼び出します。 渡された WIA 項目コンテキストは、フィルムスキャナー項目またはフィルムスキャン項目フレームに属します。 このドライバーは、アプリケーションがフィルムスキャンユニットを使用してスキャンすることを簡単に判断できます。

4.  現在のフィルム項目のプロパティ (子フレームのプロパティも含む) を使用して、デバイスをプログラムし、フィルムスキャンユニットからスキャンします。 WIA ドライバーがフィルムスキャンモードでない場合は、スキャン用にこのモードに切り替えようとします。 アプリケーションを切り替えることができるのは、負と正の両方の光だけです。 フィルムスキャナー項目を使用したスキャンは、アプリケーションとドライバーの間のコントラクトです。データ転送には、スキャナーのフィルムスキャン機能が使用されるということに同意します。

フィルムスキャナー項目にある WIA プロパティは、スキャンの前にスキャナーのフィルムスキャン部分に適用される設定として、ドライバーによって使用されます。 Wia アプリケーションは、WIA ドライバーによって返されるデータのヘッダーを常に信頼する必要があります。 たとえば、スキャナーは、指定されたイメージの幅をスキャンできず、値を丸める必要があると判断しました。 ドライバーは、アプリケーションに適切なデータが含まれるように、更新された幅情報でイメージヘッダーを更新する必要があります。 WIA ドライバーは、常に、デバイスから返される実際のデータ情報を使用して、WIA プロパティセットを更新する必要があります。

 

 




