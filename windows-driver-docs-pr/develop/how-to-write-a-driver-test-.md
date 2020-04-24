---
ms.assetid: 79AB7242-72D6-4198-9AF0-482CBFB756C7
title: ドライバー テスト テンプレートを使ってドライバー テストを作成する方法
description: Windows Driver Kit (WDK) for Windows 8 を使って、独自のドライバー テストを作成したり、提供されているテストの一部をカスタマイズしたりします。
ms.date: 03/26/2020
ms.localizationpriority: medium
ms.openlocfilehash: 40dafed4d6fa901505fcc57fa82c0d74b7a3de18
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80327567"
---
# <a name="how-to-write-a-driver-test-using-a-driver-test-template"></a>ドライバー テスト テンプレートを使ってドライバー テストを作成する方法

> [!NOTE]
> このトピックでは、Visual Studio 2013 でのみ使用できる機能について説明します。 以前の WDK および Visual Studio のエディションの詳細については、「[その他の WDK のダウンロード](../other-wdk-downloads.md)」を参照してください。
> 


Windows Driver Kit (WDK) for Windows 8 を使って、独自のドライバー テストを作成したり、提供されているテストの一部をカスタマイズすることができます。 Microsoft Visual Studio Ultimate 2012 用に WDK で提供されているドライバー テスト フレームワークを使って、作成したテストをリモート テスト コンピューターに展開できます。

WDK には、C++、C\#、スクリプト (JScript) で Windows ドライバー テスト プロジェクト用のスタート コードを作成するテンプレートが用意されています。 含めるテスト ケースを選択したり、空のプロジェクトから始めたりできます。 コードをカスタマイズして、ドライバー用の新しいテスト ケースに追加することができます。 ドライバー テスト フレームワークを使って、Visual Studio からテストを展開できます。

## <a name="span-idto_customize_a_driver_test_using_the_driver_test_template_for_c__spanspan-idto_customize_a_driver_test_using_the_driver_test_template_for_c__spanspan-idto_customize_a_driver_test_using_the_driver_test_template_for_c__spanto-customize-a-driver-test-using-the-driver-test-template-for-c"></a><span id="To_customize_a_driver_test_using_the_Driver_Test_template_for_C__"></span><span id="to_customize_a_driver_test_using_the_driver_test_template_for_c__"></span><span id="TO_CUSTOMIZE_A_DRIVER_TEST_USING_THE_DRIVER_TEST_TEMPLATE_FOR_C__"></span>C++ 用のドライバー テスト テンプレートを使ってドライバー テストをカスタマイズするには


1.  **[ファイル]** メニューの **[新規作成] &gt; [プロジェクト]** をクリックします。
2.  **[新しいプロジェクト]** ダイアログ ボックスのインストール済みのテンプレートの一覧で、 **[Visual C++] &gt; [Windows Driver (Windows ドライバー)] &gt; [テスト]** の順に選びます。
3.  **[Windows Driver Test in C++ (C++ での Windows ドライバーのテスト)]** を選びます。
4.  ドライバー テスト プロジェクトの名前と場所を指定します (または既定値を使います)。
5.  **[Windows Driver Test] (Windows ドライバーのテスト)** ダイアログ ボックスで、含めるテスト ケースか、空のドライバー テストを選択します。 テスト ケースについて詳しくは、「[Windows ドライバーのテスト ケース](#windows_driver_test_cases)」をご覧ください。
6.  必要なテスト メタデータを追加します。 詳しくは、「[テスト メタデータを追加する方法](to-add-test-metadata.md)」をご覧ください。
7.  ドライバー テストをビルドします。

## <a name="span-idto_customize_a_driver_test_using_the_driver_test_template_for_c_spanspan-idto_customize_a_driver_test_using_the_driver_test_template_for_c_spanspan-idto_customize_a_driver_test_using_the_driver_test_template_for_c_spanto-customize-a-driver-test-using-the-driver-test-template-for-c"></a><span id="To_customize_a_driver_test_using_the_Driver_Test_template_for_C_"></span><span id="to_customize_a_driver_test_using_the_driver_test_template_for_c_"></span><span id="TO_CUSTOMIZE_A_DRIVER_TEST_USING_THE_DRIVER_TEST_TEMPLATE_FOR_C_"></span>C\# 用のドライバー テスト テンプレートを使ってドライバー テストをカスタマイズするには


1.  **[ファイル]** メニューの **[新規作成] &gt; [プロジェクト]** をクリックします。
2.  **[新しいプロジェクト]** ダイアログ ボックスのインストール済みのテンプレートの一覧で、 **[Visual C]\# &gt;[Windows Driver]\(Windows ドライバー\)** の順に選びます。
3.  **[Windows Driver Test in C\#]\(C# での Windows ドライバーのテスト\)** を選びます。
4.  ドライバー テスト プロジェクトの名前と場所を指定します (または既定値を使います)。
5.  **[Windows Driver Test] (Windows ドライバーのテスト)** ダイアログ ボックスで、含めるテスト ケースか、空のドライバー テストを選択します。 テスト ケースについて詳しくは、「[Windows ドライバーのテスト ケース](#windows_driver_test_cases)」をご覧ください。
6.  必要なテスト メタデータを追加します。 詳しくは、「[テスト メタデータを追加する方法](to-add-test-metadata.md)」をご覧ください。
7.  ドライバー テストをビルドします。

## <a name="span-idto_customize_a_driver_test_using_the_driver_test_template_for_scriptspanspan-idto_customize_a_driver_test_using_the_driver_test_template_for_scriptspanspan-idto_customize_a_driver_test_using_the_driver_test_template_for_scriptspanto-customize-a-driver-test-using-the-driver-test-template-for-script"></a><span id="To_customize_a_driver_test_using_the_Driver_Test_template_for_Script"></span><span id="to_customize_a_driver_test_using_the_driver_test_template_for_script"></span><span id="TO_CUSTOMIZE_A_DRIVER_TEST_USING_THE_DRIVER_TEST_TEMPLATE_FOR_SCRIPT"></span>スクリプト用のドライバー テスト テンプレートを使ってドライバー テストをカスタマイズするには


1.  **[ファイル]** メニューの **[新規作成] &gt; [プロジェクト]** をクリックします。
2.  **[新しいプロジェクト]** ダイアログ ボックスのインストール済みのテンプレートの一覧で、 **[スクリプト] &gt; [Windows Driver (Windows ドライバー)]** の順に選びます。
3.  **[Windows Driver Test Script (Windows ドライバー テスト スクリプト)]** をクリックします。
4.  ドライバー テスト プロジェクトの名前と場所を指定します (または既定値を使います)。
5.  **[Windows Driver Test] (Windows ドライバーのテスト)** ダイアログ ボックスで、含めるテスト ケースか、空のドライバー テストを選択します。 テスト ケースについて詳しくは、「[Windows ドライバーのテスト ケース](#windows_driver_test_cases)」をご覧ください。
6.  必要なテスト メタデータを追加します。 詳しくは、「[テスト メタデータを追加する方法](to-add-test-metadata.md)」をご覧ください。
7.  ドライバー テストをビルドします。

## <a name="span-idmaking_the_driver_tests_you_create_available_for_deployment_on_test_computersspanspan-idmaking_the_driver_tests_you_create_available_for_deployment_on_test_computersspanspan-idmaking_the_driver_tests_you_create_available_for_deployment_on_test_computersspanmaking-the-driver-tests-you-create-available-for-deployment-on-test-computers"></a><span id="Making_the_driver_tests_you_create_available_for_deployment_on_test_computers"></span><span id="making_the_driver_tests_you_create_available_for_deployment_on_test_computers"></span><span id="MAKING_THE_DRIVER_TESTS_YOU_CREATE_AVAILABLE_FOR_DEPLOYMENT_ON_TEST_COMPUTERS"></span>作成したドライバー テストをテスト コンピューターに展開できるようにするには


ドライバー テストをビルドすると、新しいテストをテスト コンピューターに展開できるようになります。 既定では、作成したテストはテスト カテゴリの **[My Test Category] (個人用テスト カテゴリ)** に表示されます。 テストの名前は選択したテスト ケースに基づいたもので、**My Plug and Play Surprise Remove Test** のような名前になります。 テストをビルドするたびに、そのテストは上書きされます。 テストの最新のビルドをテスト コンピューターに展開して実行できます。

## <a name="span-idwindows_driver_test_casesspanspan-idwindows_driver_test_casesspanwindows-driver-test-cases"></a><span id="windows_driver_test_cases"></span><span id="WINDOWS_DRIVER_TEST_CASES"></span>Windows ドライバーのテスト ケース


WDK には、C++、C\#、スクリプトで Windows ドライバー テスト プロジェクト用のスタート コードが用意されています。 含めるテスト ケースを選択したり、空のプロジェクトから始めたりできます。 言語によっては、使えないテスト ケースもあります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プラグ アンド プレイ テスト ケース</th>
<th align="left">プラグ アンド プレイ (PnP) 関連の IRP のほとんどをドライバーに処理させるテスト ケース</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">無効化/有効化</td>
<td align="left">PnP デバイスを無効または有効にするテスト ケースにコードを提供します。</td>
</tr>
<tr class="even">
<td align="left">Remove</td>
<td align="left">PnP デバイスを削除するテスト ケースにコードを提供します。</td>
</tr>
<tr class="odd">
<td align="left">突然の削除</td>
<td align="left">PnP デバイスを突然削除するテスト ケースにコードを提供します。</td>
</tr>
<tr class="even">
<td align="left">電源管理テスト ケース</td>
<td align="left">システムのスリープ状態をドライバーに処理させるテスト ケース</td>
</tr>
<tr class="odd">
<td align="left">システムのスリープ状態</td>
<td align="left">システムがスリープ状態と電源状態を循環しているときにデバイス I/O を行うテスト ケースにコードを提供します。</td>
</tr>
<tr class="even">
<td align="left">ストレスと機能テスト ケース</td>
<td align="left">IOCTL および WMI インターフェイスの I/O ストレス テストと I/O 関数テストを実行するテスト ケースを提供します。</td>
</tr>
<tr class="odd">
<td align="left">I/O ストレス</td>
<td align="left">デバイス I/O ストレスを実行するテスト ケースを提供します。</td>
</tr>
<tr class="even">
<td align="left">IOCTL 機能インターフェイス</td>
<td align="left">IOCTL インターフェイス用の機能テスト ケースを作成するテンプレートを提供します。 (C++ でのみ利用できます)</td>
</tr>
<tr class="odd">
<td align="left">WMI 機能インターフェイス</td>
<td align="left">Windows Management Interface (WMI) 用の機能テスト ケースを作成するテンプレートを提供します。 (スクリプトでのみ利用できます)</td>
</tr>
<tr class="even">
<td align="left">空のテスト ケース</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">Windows ドライバー テスト プロジェクトの作成用の空のテンプレートを提供します。</td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [Test Authoring and Execution Framework](https://docs.microsoft.com/windows-hardware/drivers/taef/index)
* [Windows Driver Testing Framework](https://docs.microsoft.com/windows-hardware/drivers/wdtf/index)
* [テスト メタデータを追加する方法](to-add-test-metadata.md)
 

 






