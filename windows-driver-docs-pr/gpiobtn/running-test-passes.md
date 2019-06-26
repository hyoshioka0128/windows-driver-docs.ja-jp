---
title: テスト パスの実行
description: ミット プラットフォームでは、テストの自動化と調査の対象となる送信される GPIO パターンをカスタマイズするオプションの両方を提供することにより、GPIO ボタンをテストできます。
ms.assetid: E24AD015-1E14-4EF9-8443-D0F38FA3321E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: aa2698456bdb74af8cf56962a742d05306d66a00
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373560"
---
# <a name="running-test-passes"></a>テスト パスの実行


ミット プラットフォームでは、テストの自動化と調査の対象となる送信される GPIO パターンをカスタマイズするオプションの両方を提供することにより、GPIO ボタンをテストできます。

ミット テスト ツールの詳細については、次にお問い合わせください。MittSupport@microsoft.comします。

最初に、次を参照してください。[ミットで GPIO テスト](https://docs.microsoft.com/windows-hardware/drivers/spb/gpio-tests-in-mitt)します。 インストーラーをダウンロード、コンテンツを展開し、読み取り、 **ReadMe**ファイル ツールの概要。

## <a name="span-idend-to-endindicatortestingforconvertiblesspanspan-idend-to-endindicatortestingforconvertiblesspanspan-idend-to-endindicatortestingforconvertiblesspanend-to-end-indicator-testing-for-convertibles"></a><span id="End-to-end_indicator_testing_for_convertibles"></span><span id="end-to-end_indicator_testing_for_convertibles"></span><span id="END-TO-END_INDICATOR_TESTING_FOR_CONVERTIBLES"></span>エンド ツー エンドのインジケーター コンバーチブルのテスト


エンド ツー エンドのインジケーター コンバーチブル次の領域における潜在的な問題を公開するためのテストを実行する必要があります。

-   システムを 1 つのモードから別のモードを変換する際のさまざまなタイミングです。
-   機械の詳細、変換可能なのです。

### <a name="span-idlaptoptoslateconversiontestscenariospanspan-idlaptoptoslateconversiontestscenariospanspan-idlaptoptoslateconversiontestscenariospanlaptop-to-slate-conversion-test-scenario"></a><span id="Laptop_to_slate_conversion_test_scenario"></span><span id="laptop_to_slate_conversion_test_scenario"></span><span id="LAPTOP_TO_SLATE_CONVERSION_TEST_SCENARIO"></span>スレートの変換のテスト シナリオにラップトップ コンピューター

ラップトップ モード (ショートカット キーにアクセスできる) で、システムを起動します。

1.  移動するウィンドウ ボタンを押して**開始**します。
2.  キーボードを使用して、開始文字のキーを押して**検索**します。
3.  編集フィールドにタップします。 *検証*:スクリーン キーボードのキーが展開する必要があります。
4.  システム (縦と横) を回転します。 *検証*:システムが回転する必要があります。
5.  スレートをラップトップから変換する (キーボードにアクセスできなくなります)。 このようなアクションの例: 回転または反転画面、キーボードなどをデタッチします。
6.  タップ、**検索**フィールドを編集します。 *検証*:スクリーン キーボードのキーを展開する必要があります。
7.  システム (縦と横) を回転します。 *検証*:システムが回転する必要があります。

**注**  ごと、システムは、タブレット モードに変換できる個別の方法の次の手順を繰り返します。

 

 

 




