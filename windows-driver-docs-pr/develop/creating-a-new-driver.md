---
ms.assetid: A637B75C-C227-495A-AB5B-B42DDF7842B9
title: 新しいデバイス ファンクション ドライバーの作成
description: このトピックでは、Visual Studio を使って新しいデバイス ファンクション ドライバーの作成を始める方法について説明します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 081e1172c2b1f8fa988da2002037f5308a0c59ba
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63382424"
---
# <a name="creating-a-new-device-function-driver"></a>新しいデバイス ファンクション ドライバーの作成

このトピックでは、Visual Studio を使って新しいデバイス ファンクション ドライバーの作成を始める方法について説明します。 デバイス ファンクション ドライバーは、フィルター ドライバー、ソフトウェア ドライバー、ファイル システム ドライバーとは異なります。それらのドライバーについては、別のトピックで説明しています。 デバイス ファンクション ドライバーと、他の種類のドライバーとの違いについて詳しくは、「[ドライバーとは](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554678)」、「[ドライバー モデルの選択](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554652)」、「[デバイス ノードとデバイス スタック](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554721)」をご覧ください。

はじめに、「[デバイスとドライバーのテクノロジ](https://msdn.microsoft.com/Library/Windows/Hardware/Ff557557)」にあるテクノロジの一覧で、デバイスがどれに適合するかを特定します。 デバイスに使用できるドライバー モデルを調べるには、その特定のテクノロジのドキュメントを参照してください。 適切なドライバー モデルは、テクノロジごとに異なります。 一部のテクノロジのドキュメントでは、ユーザー モード ドライバー フレームワーク (UMDF) またはカーネル モード ドライバー フレームワーク (KMDF) を使うことを勧めています。 他のテクノロジのドキュメントでは、ドライバー ペアの一部であるミニドライバーを作成する方法を説明しています。 ミニドライバーは、ミニポート、ミニクラスなど、さまざまな名前で呼ばれています。

次に、勧められているドライバー モデルが以下のどのケースと一致しているかを判断し、その手順に従います。

### <a name="span-idcase1thedocumentationforyourtechnologyrecommendsumdfspanspan-idcase1thedocumentationforyourtechnologyrecommendsumdfspanspan-idcase1thedocumentationforyourtechnologyrecommendsumdfspancase-1-the-documentation-for-your-technology-recommends-umdf"></a><span id="Case_1__The_documentation_for_your_technology_recommends_UMDF."></span><span id="case_1__the_documentation_for_your_technology_recommends_umdf."></span><span id="CASE_1__THE_DOCUMENTATION_FOR_YOUR_TECHNOLOGY_RECOMMENDS_UMDF."></span>ケース 1: テクノロジのドキュメントで UMDF が勧められている。

1.  Visual Studio の **[ファイル]** メニューで、 **[新規作成]、[プロジェクト]** の順にクリックします。
2.  [新しいプロジェクト] ダイアログ ボックスの左側のウィンドウで、 **[Visual C++]、[Windows Driver] (Windows ドライバー)、[WDF]** を探してクリックします。
3.  中央のウィンドウで、 **[User Mode Driver (UMDF)] (ユーザー モード ドライバー (UMDF))** をクリックします。
4.  **[名前]** ボックスと **[場所]** ボックスに入力し、 **[OK]** をクリックします。 詳しくは、「[テンプレートを使った UMDF ドライバーの作成](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439659)」をご覧ください。
    **注**  新しい UMDF ドライバーを作成する場合、32 文字以下のドライバー名を選ぶ必要があります。 この長さの制限は、wdfglobals.h で定義されています。
5.  この時点で、ほとんどの UMDF ドライバーに必要な一般的なコードを実装したドライバー プロジェクトができています。 これで、デバイス固有のコードを追加できるようになりました。 実装する必要があるインターフェイスについて詳しくは、テクノロジのドキュメントをご覧ください。

### <a name="span-idcase2thedocumentationforyourtechnologyrecommendskmdfspanspan-idcase2thedocumentationforyourtechnologyrecommendskmdfspanspan-idcase2thedocumentationforyourtechnologyrecommendskmdfspancase-2-the-documentation-for-your-technology-recommends-kmdf"></a><span id="Case_2__The_documentation_for_your_technology_recommends_KMDF."></span><span id="case_2__the_documentation_for_your_technology_recommends_kmdf."></span><span id="CASE_2__THE_DOCUMENTATION_FOR_YOUR_TECHNOLOGY_RECOMMENDS_KMDF."></span>ケース 2: テクノロジのドキュメントで KMDF が勧められている。

1.  Visual Studio の **[ファイル]** メニューで、 **[新規作成]、[プロジェクト]** の順にクリックします。
2.  [新しいプロジェクト] ダイアログ ボックスの左側のウィンドウで、 **[WDF]** を探してクリックします。
3.  中央のウィンドウで、 **[Kernel Mode Driver (KMDF)] (カーネル モード ドライバー (KMDF))** をクリックします。
4.  **[名前]** ボックスと **[場所]** ボックスに入力し、 **[OK]** をクリックします。 詳しくは、「[テンプレートを使った KMDF ドライバーの作成](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439654)」をご覧ください。
    **注**  新しい KMDF ドライバーを作成する場合、32 文字以下のドライバー名を選ぶ必要があります。 この長さの制限は、wdfglobals.h で定義されています。
5.  この時点で、ほとんどの KMDF ドライバーに必要な一般的なコードを実装したドライバー プロジェクトができています。 これで、デバイス固有のコードを追加できるようになりました。 実装する必要があるメソッドについて詳しくは、テクノロジのドキュメントをご覧ください。

### <a name="span-idcase3thedocumentationforyourtechnologydescribesaminidrivermodelspanspan-idcase3thedocumentationforyourtechnologydescribesaminidrivermodelspanspan-idcase3thedocumentationforyourtechnologydescribesaminidrivermodelspancase-3-the-documentation-for-your-technology-describes-a-minidriver-model"></a><span id="Case_3__The_documentation_for_your_technology_describes_a_minidriver_model."></span><span id="case_3__the_documentation_for_your_technology_describes_a_minidriver_model."></span><span id="CASE_3__THE_DOCUMENTATION_FOR_YOUR_TECHNOLOGY_DESCRIBES_A_MINIDRIVER_MODEL."></span>ケース 3: テクノロジのドキュメントでミニドライバー モデルについて説明されている。

デバイス テクノロジにミニポート、ミニクラス、その他の種類のミニドライバー モデルがある場合は、Visual Studio にそのモデル用の固有のテンプレートがあるかどうかを確認します。

1.  Visual Studio の **[ファイル]** メニューで、 **[新規作成]、[プロジェクト]** の順にクリックします。
2.  [新しいプロジェクト] ダイアログ ボックスの左側のウィンドウで、 **[テンプレート]、[Visual C++]、[Windows Driver] (Windows ドライバー)** を探してクリックします。
3.  インストールされているテンプレートの一覧で、作成するミニドライバーの種類のテンプレートを探します。
4.  該当するミニドライバーの種類のテンプレートが **[Windows Driver]** (Windows ドライバー) にない場合は、 **[Online]** (オンライン) をクリックして、オンラインで利用できるテンプレートを参照します。
5.  該当するミニドライバーの種類のテンプレートが見つかった場合は、そのテンプレートを選び、 **[名前]** ボックスと **[場所]** ボックスに入力して、 **[OK]** をクリックします。
6.  この時点で、ミニドライバーに必要な一般的なコードを実装したドライバー プロジェクトができています。 これで、デバイス固有のコードを追加できるようになりました。 実装する必要がある関数について詳しくは、テクノロジのドキュメントをご覧ください。

デバイス テクノロジにミニドライバー モデルがあり、そのミニドライバーの種類の固有のテンプレートが見つからない場合は、通常、Windows Driver Model (WDM) テンプレートをベースにするのが適しています。 ガイダンスについては、テクノロジ固有のドキュメントをご覧ください。 まれに、ミニドライバーの作成に KMDF を使える場合がありますが、多くの場合は WDM が出発点になります。

1.  Visual Studio の **[ファイル]** メニューで、 **[新規作成]、[プロジェクト]** の順にクリックします。
2.  Visual Studio の [新しいプロジェクト] ダイアログ ボックスで、 **[Windows Driver]** (Windows ドライバー) の **[WDM]** をクリックします。
3.  **[名前]** ボックスと **[場所]** ボックスに入力し、 **[OK]** をクリックします。
4.  この時点で、空の WDM ドライバー プロジェクトができます。 ソリューション エクスプローラー ウィンドウでドライバー プロジェクトを右クリックし、 **[追加]、[新しい項目]** の順にクリックします。
5.  [新しい項目の追加] ダイアログ ボックスで **[C++ ファイル (.cpp)]** を選び、ファイルの名前を入力して **[OK]** をクリックします。

    **注**  .cpp ファイルでなく .c ファイルを作成する場合は、拡張子が **.c** の名前を入力します。
6.  実装する必要がある関数について詳しくは、テクノロジのドキュメントをご覧ください。 関数の実装と整理が進むにつれて、.cpp または .c ファイルの追加が必要になる場合があります。

 

 





