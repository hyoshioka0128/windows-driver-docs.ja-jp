---
ms.assetid: eaefc81a-b5e3-4763-bf51-8ec47f620e72
title: ドライバー パッケージの作成
description: ドライバー パッケージの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a778114e57284cba6a460c4a257e766fa4d76d37
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "67370810"
---
# <a name="creating-a-driver-package"></a>ドライバー パッケージの作成

## <a name="span-iddriver_projects_and_packagesspanspan-iddriver_projects_and_packagesspanspan-iddriver_projects_and_packagesspandriver-projects-and-packages"></a><span id="Driver_projects_and_packages"></span><span id="driver_projects_and_packages"></span><span id="DRIVER_PROJECTS_AND_PACKAGES"></span>ドライバー プロジェクトとドライバー パッケージ


ドライバー *プロジェクト*とは、(.sys ファイルなどの) ドライバー バイナリを生成し、場合によってはドライバーの INF ファイルを生成する Microsoft Visual Studio プロジェクトです。

ドライバー *パッケージ*とは、ドライバーのインストールに使われるファイルを集めたものです。 パッケージには、INF ファイルと、その INF ファイルによって参照されるファイルおよびバイナリが含まれます。 Visual Studio では、ドライバー パッケージを使ってリモート ターゲットに対して自動でドライバーを展開し、デバッグします。

ドライバー パッケージは、ドライバー プロジェクトなどの 1 つ以上のプロジェクトから出力を収集する一種のプロジェクトです。 ドライバー パッケージのプロジェクトはビルドされると、Visual Studio がドライバーの展開に使うドライバー パッケージを生成します。

![Visual Studio のソリューション エクスプローラーのドライバー パッケージ プロジェクト](images/VsSlnExplorer.png)

**注:**  

 

ドライバー テンプレートを使ってドライバー ソリューションを作成すると、テンプレートによってプロジェクトを 2 つ備えたソリューションが自動で作成されます。 プロジェクトは 1 つがドライバー用、もう 1 つがドライバー パッケージ用です。
## <a name="span-idmanually_creating_a_driver_packagespanspan-idmanually_creating_a_driver_packagespanspan-idmanually_creating_a_driver_packagespanmanually-creating-a-driver-package"></a><span id="Manually_creating_a_driver_package"></span><span id="manually_creating_a_driver_package"></span><span id="MANUALLY_CREATING_A_DRIVER_PACKAGE"></span>ドライバー パッケージを手動で作成する


ソリューションにドライバー パッケージがなければ、Visual Studio で新しく作成できます。これには、 **[ファイル]** メニューで **[新規作成] &gt; [プロジェクト]** をクリックします。 ドライバー パッケージを作成する方法の例については、「[初めてのドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/writing-your-first-driver)」をご覧ください。

ドライバー パッケージのないソリューションに新しいドライバー パッケージを作成するには、"ドライバー インストール パッケージ" テンプレートを使います。 **[ファイル]、[新規]、[プロジェクト]** の順に選択します。 次に、ダイアログで、 **[Windows ドライバー] &gt; [パッケージ] &gt; [ドライバー インストール パッケージ]** をクリックします。 次に、 **[ソリューション]** ドロップダウン リストで **[ソリューションに追加]** を選択し、 **[OK]** をクリックします。

## <a name="span-idmodifying_an_existing_driver_packagespanspan-idmodifying_an_existing_driver_packagespanspan-idmodifying_an_existing_driver_packagespanmodifying-an-existing-driver-package"></a><span id="Modifying_an_existing_driver_package"></span><span id="modifying_an_existing_driver_package"></span><span id="MODIFYING_AN_EXISTING_DRIVER_PACKAGE"></span>既にあるドライバー パッケージを変更する


ソリューションに既にドライバー パッケージが含まれている場合には、ソリューションの他のプロジェクトを参照するように変更できます。

[ソリューション エクスプローラー] ウィンドウでドライバー パッケージ プロジェクトを開き、 **[参照]** を右クリックして、 **[参照の追加...]** を選択し、参照するプロジェクトを選択します。

既にあるプロジェクトへの参照を削除するには、参照を削除するプロジェクトを右クリックして、 **[削除]** をクリックしてください。

![ドライバー パッケージのプロパティ](images/VsDrvrPkgProps.png)

## <a name="span-idmultiple_drivers_in_a_solutionspanspan-idmultiple_drivers_in_a_solutionspanspan-idmultiple_drivers_in_a_solutionspanmultiple-drivers-in-a-solution"></a><span id="Multiple_drivers_in_a_solution"></span><span id="multiple_drivers_in_a_solution"></span><span id="MULTIPLE_DRIVERS_IN_A_SOLUTION"></span>1 つのソリューションに複数のドライバーを含める


ソリューションには、複数のドライバーとそのパッケージを追加できます。 「既にあるドライバー パッケージを変更する」と同様に、新しいドライバー ソリューションを作成することも、既にあるソリューションに参照を追加することもできます。 ソリューションに既にドライバー パッケージが含まれている場合は、パッケージを変更して、ソリューション内の他のドライバー プロジェクトへの参照を追加できます。

[ソリューション エクスプローラー] ウィンドウでドライバー パッケージ プロジェクトを開き、 **[参照]** を右クリックして、 **[参照の追加...]** を選択し、参照するプロジェクトを選択します。

既にあるプロジェクトへの参照を削除するには、参照を削除するプロジェクトを右クリックして、 **[削除]** をクリックしてください。

複数のドライバーを含むソリューションの例については、"Toaster サンプル ドライバー" をご覧ください。![1 つのソリューション内の複数のドライバー](images/MultipleDriversSingleSolution.png)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [ドライバーへの署名](signing-a-driver.md)
 

 






