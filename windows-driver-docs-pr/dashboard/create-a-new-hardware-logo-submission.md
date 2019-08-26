---
title: 新しい WLK デバイス認定申請の作成
description: 新しい WLK デバイス認定申請の作成
ms.assetid: e812eee1-768d-42d6-918e-c716b5c29ea2
ms.topic: article
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3543b86f5c1ceed26137740c85331c97206423e0
ms.sourcegitcommit: 9e91fcdfcc0b4d05ca2f1f8a30b627adc607f7af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2019
ms.locfileid: "69621140"
---
# <a name="create-a-new-wlk-device-certification-submission"></a>新しい WLK デバイス認定申請の作成


ロゴ認定の取得に向けて Windows Server 2008 (およびそれ以前) のハードウェアを準備するには、**WQReady.xml** ファイルを作成して提出する必要があります。 このファイルを提出すると、ダッシュボードがデバイスをテストし、パフォーマンスに関するレポートを返すことができるようになります。 このレポートには、デバイスと Windows 標準とを比較した詳しいリストが含まれています。

## <a name="creating-a-wqreadyxml-file"></a>WQReady.xml ファイルの作成

1.  [Windows Logo Kit (WLK)](https://go.microsoft.com/fwlink/p/?LinkId=219237) をダウンロードします。 必ず、認定を受けるそれぞれのオペレーティング システム上で、適切な認定キットを使って対象の (1 つまたは複数の) ドライバーをテストしてください。

2.  Winqual Submission Tool (WST) を開き、 **[Add]** (追加) をクリックします。

3.  **.cpk** ファイル (WLK テスト結果) を参照し、 **[Load]** (読み込み) をクリックします。

4.  デバイスがインボックスではない場合は、 **[Driver Package]** (ドライバー パッケージ)、 **[Driver Locales]** (ドライバー ロケール)、 **[Symbols (optional)]** (シンボル (省略可能)) に、必要な情報を入力します。 **注意**:ドライバー パッケージの相対パスとファイル名の合計は、160 文字未満にする必要があります。 これを超えた場合、送信処理が失敗します。

5.  **[Add DTM Results]** (DTM 結果の追加) ダイアログ ボックスを閉じます。

6.  新しいエントリを編集するには、目的のエントリを選び、 **[Edit]** (編集) をクリックします。

7.  すべてのエントリを追加したら、 **[Create Package]** (パッケージの作成) をクリックして、 **.cab** 提出パッケージを作成します。

8.  ツールがエラーを検出すると、パッケージの作成が中止され、エラーが発生したエントリが赤色で強調表示されます。 エラーを表示するには、 **[View Errors]** (エラーの表示) をクリックします。 **[Edit]** (編集) をクリックし、ドライバーまたはテスト結果を更新して、エラーを修正します。 パッケージを作成するには、すべてのエラーが修正されている必要があります。

9.  ツールによって、申請に使われる **WQReady.xml** ファイルが生成されます。

    **注**  
    **WQReady.xml** は既定のファイル名です。この名前は変更できます。

## <a name="submitting-your-file"></a>ファイルの提出

1. パートナー センターにサインインし、 **[Submit new hardware]\(新しいハードウェアの申請\)** を選択します。 これにより、提出を作成するためのウィザードが読み込まれます。

2. **[Packages and signing properties]** (パッケージと署名プロパティ) セクションで、ドライバー提出の名前を選びます。 この名前は、ドライバー提出の検索と整理に使うことができます。

3. Winqual Submission Tool を使用して作成した **.cab** ファイルのうち、申請するものをドラッグ アンド ドロップするか、参照します。 ファイルのアップロードが開始されます。

![WLK cab ファイルのアップロードと WQReadyXML のアップロード コントロールを示すスクリーン ショット](images/upload-wlk.png)

4. 次に、申請する **WQReady.xml** ファイルをドラッグ アンド ドロップするか、参照します。 これでアップロードが完了します

5. 「[新しいハードウェア申請の作成](create-a-new-hardware-submission.md)」の手順 6 から続きの作業を行い、申請を完了します。
