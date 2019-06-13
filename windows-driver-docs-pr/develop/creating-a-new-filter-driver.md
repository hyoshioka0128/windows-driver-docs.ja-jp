---
ms.assetid: AB4E6021-FDF9-40D0-818C-9602E1AEA564
title: 新しいフィルター ドライバーの作成
description: このトピックでは、Visual Studio を使って新しいフィルター ドライバーの作成を始める方法について説明します。 フィルター ドライバーは、デバイス ファンクション ドライバー、ソフトウェア ドライバー、ファイル システム ドライバーとは異なります。それらのドライバーについては、別のトピックで説明しています。
keywords: フィルター ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d6807e13500558450dafd4be1f37989cc956c45
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63382414"
---
# <a name="creating-a-new-filter-driver"></a>新しいフィルター ドライバーの作成

このトピックでは、Visual Studio を使って新しいフィルター ドライバーの作成を始める方法について説明します。 フィルター ドライバーは、デバイス ファンクション ドライバー、ソフトウェア ドライバー、ファイル システム ドライバーとは異なります。それらのドライバーについては、別のトピックで説明しています。 フィルター ドライバーと、他の種類のドライバーとの違いについて詳しくは、以下のトピックをご覧ください。

-   [ドライバーとは](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554678)
-   [ドライバー モデルの選択](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554652)
-   [デバイス ノードとデバイス スタック](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554721)
-   [フィルター ドライバー](https://msdn.microsoft.com/Library/Windows/Hardware/Ff545890)
-   [WDM ドライバーの種類](https://msdn.microsoft.com/Library/Windows/Hardware/Ff564862)

まず、どのドライバー モデルがフィルター ドライバーに適しているかを判断します。 どのモデルが最適かの判断については、「[ドライバー モデルの選択](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554652)」をご覧ください。 ハードウェア デバイスのフィルター ドライバーを作成する場合は、「[デバイスとドライバーのテクノロジ](https://msdn.microsoft.com/Library/Windows/Hardware/Ff557557)」にあるテクノロジの一覧で、デバイスがどれに適合するかを特定します。 特定したテクノロジのドキュメントに、フィルター ドライバー モデルの選択に関するガイダンスがあるかどうかを確認します。 適切なフィルター ドライバー モデルは、テクノロジごとに異なります。 一部のテクノロジのドキュメントでは、ユーザー モード ドライバー フレームワーク (UMDF)、カーネル モード ドライバー フレームワーク (KMDF)、または Windows Driver Model (WDM) を使うことを勧めています。 他のテクノロジのドキュメントでは、フィルター ドライバーの作成方法について、具体的に詳しく説明しています。 一部のテクノロジには、ミニフィルター モデルがあります。 テクノロジによっては、フィルター ドライバー モデルについて何も推奨されていない場合もあります。

次に、勧められているドライバー モデルが以下のどのケースと一致しているかを判断し、その手順に従います。

## <a name="span-idcase1thedocumentationforyourtechnologyrecommendsumdfspanspan-idcase1thedocumentationforyourtechnologyrecommendsumdfspancase-1-the-documentation-for-your-technology-recommends-umdf"></a><span id="case_1__the_documentation_for_your_technology_recommends_umdf."></span><span id="CASE_1__THE_DOCUMENTATION_FOR_YOUR_TECHNOLOGY_RECOMMENDS_UMDF."></span>ケース 1: テクノロジのドキュメントで UMDF が勧められている。


1.  Visual Studio の **[ファイル]** メニューで、 **[新規作成]、[プロジェクト]** の順にクリックします。
2.  [新しいプロジェクト] ダイアログ ボックスの左側のウィンドウで、 **[Visual C++]、[Windows Driver] (Windows ドライバー)、[WDF]** を探してクリックします。
3.  中央のウィンドウで、 **[User Mode Driver (UMDF)] (ユーザー モード ドライバー (UMDF))** をクリックします。
4.  **[名前]** ボックスと **[場所]** ボックスに入力し、 **[OK]** をクリックします。 詳しくは、「[テンプレートを使った UMDF ドライバーの作成](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439659)」をご覧ください。
    **注**  新しい UMDF ドライバーを作成する場合、32 文字以下のドライバー名を選ぶ必要があります。 この長さの制限は、wdfglobals.h で定義されています。
5.  この時点で、ほとんどの UMDF ドライバーに必要な一般的なコードを実装したドライバー プロジェクトができています。 これで、フィルター固有のコードを追加できるようになりました。

## <a name="span-idcase2thedocumentationforyourtechnologyrecommendskmdfspanspan-idcase2thedocumentationforyourtechnologyrecommendskmdfspancase-2-the-documentation-for-your-technology-recommends-kmdf"></a><span id="case_2__the_documentation_for_your_technology_recommends_kmdf."></span><span id="CASE_2__THE_DOCUMENTATION_FOR_YOUR_TECHNOLOGY_RECOMMENDS_KMDF."></span>ケース 2: テクノロジのドキュメントで KMDF が勧められている。


1.  Visual Studio の **[ファイル]** メニューで、 **[新規作成]、[プロジェクト]** の順にクリックします。
2.  [新しいプロジェクト] ダイアログ ボックスの左側のウィンドウで、 **[WDF]** を探してクリックします。
3.  中央のウィンドウで、 **[Kernel Mode Driver (KMDF)] (カーネル モード ドライバー (KMDF))** をクリックします。
4.  **[名前]** ボックスと **[場所]** ボックスに入力し、 **[OK]** をクリックします。 詳しくは、「[テンプレートを使った KMDF ドライバーの作成](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439654)」をご覧ください。
    **注**  新しい KMDF ドライバーを作成する場合、32 文字以下のドライバー名を選ぶ必要があります。 この長さの制限は、wdfglobals.h で定義されています。
5.  この時点で、ほとんどの KMDF ドライバーに必要な一般的なコードを実装したドライバー プロジェクトができています。 これで、フィルター固有のコードを追加できるようになりました。

## <a name="span-idcase3thedocumentationforyourtechnologydescribesaspecificfilterorminifiltermodelspanspan-idcase3thedocumentationforyourtechnologydescribesaspecificfilterorminifiltermodelspancase-3-the-documentation-for-your-technology-describes-a-specific-filter-or-mini-filter-model"></a><span id="case_3__the_documentation_for_your_technology_describes_a_specific_filter_or_mini_filter_model."></span><span id="CASE_3__THE_DOCUMENTATION_FOR_YOUR_TECHNOLOGY_DESCRIBES_A_SPECIFIC_FILTER_OR_MINI_FILTER_MODEL."></span>ケース 3: テクノロジのドキュメントで特定のフィルター モデルまたはミニフィルター モデルについて説明されている。


デバイス テクノロジに特定のフィルターまたはミニフィルター モデルがある場合は、Visual Studio にそのモデル用のテンプレートがあるかどうかを確認します。

1.  Visual Studio の **[ファイル]** メニューで、 **[新規作成]、[プロジェクト]** の順にクリックします。
2.  [新しいプロジェクト] ダイアログ ボックスの左側のウィンドウで、 **[テンプレート]、[Visual C++]、[Windows Driver] (Windows ドライバー)** を探してクリックします。
3.  インストールされているテンプレートの一覧で、作成するフィルターの種類のテンプレートを探します。 たとえば、 **[Filter Driver: NDIS]\(フィルター ドライバー: NDIS\)** テンプレートを **[Networking]\(ネットワーク\)** で選択します。
4.  該当するフィルター ドライバーの種類のテンプレートが **[Windows Driver]** (Windows ドライバー) にない場合は、 **[Online]** (オンライン) をクリックして、オンラインで利用できるテンプレートを参照します。
5.  該当するフィルター ドライバーの種類のテンプレートが見つかった場合は、そのテンプレートを選び、 **[名前]** ボックスと **[場所]** ボックスに入力して、 **[OK]** をクリックします。
6.  この時点で、フィルター ドライバーに必要な一般的なコードを実装したドライバー プロジェクトができています。 これで、フィルター固有のコードを追加できるようになりました。 実装する必要がある関数について詳しくは、テクノロジのドキュメントをご覧ください。

デバイス テクノロジに特定のフィルター モデルまたはミニフィルター モデルがあり、そのフィルター ドライバーの種類のテンプレートが見つからない場合は、テクノロジ固有のドキュメントで、UMDF、KMDF、WDM のどれを使うかを判断するためのガイダンスをご覧ください。

## <a name="span-idcase4thedocumentationforyourtechnologyrecommendswdmspanspan-idcase4thedocumentationforyourtechnologyrecommendswdmspancase-4-the-documentation-for-your-technology-recommends-wdm"></a><span id="case_4__the_documentation_for_your_technology_recommends_wdm."></span><span id="CASE_4__THE_DOCUMENTATION_FOR_YOUR_TECHNOLOGY_RECOMMENDS_WDM."></span>ケース 4: テクノロジのドキュメントで WDM が勧められている。


1.  Visual Studio の **[ファイル]** メニューで、 **[新規作成]、[プロジェクト]** の順にクリックします。
2.  Visual Studio の [新しいプロジェクト] ダイアログ ボックスで、 **[Windows Driver]** (Windows ドライバー) の **[WDM]** をクリックします。
3.  **[名前]** ボックスと **[場所]** ボックスに入力し、 **[OK]** をクリックします。
4.  この時点で、空の WDM ドライバー プロジェクトができます。 ソリューション エクスプローラー ウィンドウでドライバー プロジェクトを右クリックし、 **[追加]、[新しい項目]** の順にクリックします。
5.  [新しい項目の追加] ダイアログ ボックスで **[C++ ファイル (.cpp)]** を選び、ファイルの名前を入力して **[OK]** をクリックします。

    **注**  .cpp ファイルでなく .c ファイルを作成する場合は、拡張子が **.c** の名前を入力します。
6.  フィルターに必要な関数を実装します。 関数の実装と整理が進むにつれて、.cpp または .c ファイルの追加が必要になる場合があります。

## <a name="span-idcase5thedocumentationforyourtechnologydoesnothavearecommendationforafilterdrivermodelspanspan-idcase5thedocumentationforyourtechnologydoesnothavearecommendationforafilterdrivermodelspancase-5-the-documentation-for-your-technology-does-not-have-a-recommendation-for-a-filter-driver-model"></a><span id="case_5__the_documentation_for_your_technology_does_not_have_a_recommendation_for_a_filter_driver_model."></span><span id="CASE_5__THE_DOCUMENTATION_FOR_YOUR_TECHNOLOGY_DOES_NOT_HAVE_A_RECOMMENDATION_FOR_A_FILTER_DRIVER_MODEL."></span>ケース 5: テクノロジのドキュメントにフィルター ドライバー モデルについての推奨がない。


1.  フィルター ドライバーに最適なモデルが UMDF、KMDF、WDM のどれであるかを判断します。 ヘルプについては、「[ドライバー モデルの選択](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554652)」をご覧ください。
2.  Visual Studio の **[ファイル]** メニューで、 **[新規作成]、[プロジェクト]** の順にクリックします。
3.  Visual Studio の [新しいプロジェクト] ダイアログ ボックスの **[Windows Driver]** (Windows ドライバー) で、以下のいずれかのテンプレートを選びます。

    -   **WDF | ユーザー モード ドライバー (UMDF)**
    -   **WDF | カーネル モード ドライバー (KMDF)**
    -   **WDM | 空のカーネル ドライバー**

    **注**  新しい KMDF ドライバーか UMDF ドライバーを作成する場合、32 文字以下のドライバー名を選ぶ必要があります。 この長さの制限は、wdfglobals.h で定義されています。
4.  フィルターに必要な関数を実装します。 必要に応じて、新しい .c または .cpp ファイルを作成します。

使用するテンプレートが不明な場合は、[Windows ハードウェア WDK とドライバー開発](https://go.microsoft.com/fwlink/p?LinkID=252169)のフォーラムで、記事を読んだり、投稿したりすることを検討します。

 

 



