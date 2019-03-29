---
title: 手順 5 の送信、Microsoft Store デバイス アプリ
description: このトピックでは、Microsoft Store のダッシュ ボードに UWP デバイス アプリを送信する方法について説明します。
ms.assetid: B25F9953-6EFD-4A08-AFD6-B334C46E910F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92891a52939342af36043ee4601db0e072524101
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573759"
---
# <a name="step-5-submit-the-microsoft-store-device-app"></a>手順 5:Microsoft Store のデバイス アプリを送信します。


![デバイス アプリのワークフロー、手順 5](images/5-device-app-workflow.png)

このトピックでは、Microsoft Store のダッシュ ボードに UWP デバイス アプリを送信する方法について説明します。 アプリを送信する前に、送信シーケンス」セクションを確認[構築 UWP デバイス アプリ](the-workflow.md)します。 このトピックでは、一連のステップ バイ ステップの一部です。 参照してください[ステップ バイ ステップの UWP デバイスのアプリをビルド](build-a-uwp-device-app-step-by-step.md)導入します。

**注**  特権を持つアプリとしてアプリが指定されたに対して自動インストールが構成されていない場合は、特権を持つアプリを送信する前に、Windows デベロッパー センター ハードウェア ダッシュ ボードに、デバイス メタデータを送信できます、Microsoft Store。 ここでは、この手順 5 は、の場所を取得できます[手順 6](step-6--submit-device-metadata.md)します。

 

UWP デバイスのアプリは、内部や周辺機器デバイスに対応するとして機能するデバイスの製造元が作成した UWP アプリの特別な種類です。 デバイスのメタデータを使用すると、デバイス アプリがデバイスの更新など、特権操作を実行できます。 UWP デバイスのアプリに関する詳細については、次を参照してください。[満たす UWP デバイス アプリ](meet-uwp-device-apps.md)します。

## <a name="span-idbeforeyoubeginspanspan-idbeforeyoubeginspanspan-idbeforeyoubeginspanbefore-you-begin"></a><span id="Before_you_begin"></span><span id="before_you_begin"></span><span id="BEFORE_YOU_BEGIN"></span>始める前に


このトピックでは、アプリの開発が完了したら、デバイス メタデータの準備ができました前提としています。

## <a name="span-idstartappsubmissionspanspan-idstartappsubmissionspanspan-idstartappsubmissionspanstart-app-submission"></a><span id="Start_app_submission"></span><span id="start_app_submission"></span><span id="START_APP_SUBMISSION"></span>アプリの送信を開始します。


移動して、 [Microsoft Store のダッシュ ボード](https://go.microsoft.com/fwlink/p/?LinkId=273050)クリック**新しいアプリを送信**。

## <a name="span-idaddinstructionsfortestersspanspan-idaddinstructionsfortestersspanspan-idaddinstructionsfortestersspanadd-instructions-for-testers"></a><span id="Add_instructions_for_testers"></span><span id="add_instructions_for_testers"></span><span id="ADD_INSTRUCTIONS_FOR_TESTERS"></span>テスト担当者の命令を追加します。


**テスト担当者について**、"This is UWP デバイス アプリです". テキストを入力することを確認 これは、ことを示しますアプリ送信のテスト担当者にアプリを UWP デバイス アプリ。

## <a name="span-idreviewsubmissiondetailsspanspan-idreviewsubmissiondetailsspanspan-idreviewsubmissiondetailsspanreview-submission-details"></a><span id="Review_submission_details"></span><span id="review_submission_details"></span><span id="REVIEW_SUBMISSION_DETAILS"></span>送信の詳細を確認してください。


アプリを送信する前に、次を確認します。

-   アプリの説明は、アプリに必要なハードウェアを明確に記述する必要があります。

-   UWP デバイスのアプリとしてアプリを認識する Microsoft Store のアプリ パッケージで StoreManifest.xml ファイルを含める必要があります。

-   アプリを起動すると、アプリは、アプリが動作する前に、デバイスを接続することが必要な場合は、ときに、必要があります明確に規定よう"に接続してください、 &lt;*ブランドに固有のデバイス名*&gt;"。

-   **パッケージ名**でアプリの作成時に指定する 1 つとして同じ[手順 1.](step-1--create-a-uwp-device-app.md)します。 1 年以内にアプリが送信しない場合に、パッケージ名が期限切れことに注意してください。

-   アプリはすべて完全に準拠する必要があります、 [Microsoft Store の認定要件](https://go.microsoft.com/fwlink/p/?LinkId=273052)します。

-   アプリは、あらゆる年齢層の適切なである必要があります。

-   アプリは、空きとしてマークされます必要があります。

## <a name="span-idconfirmsellingdetailsspanspan-idconfirmsellingdetailsspanspan-idconfirmsellingdetailsspanconfirm-selling-details"></a><span id="Confirm_selling_details"></span><span id="confirm_selling_details"></span><span id="CONFIRM_SELLING_DETAILS"></span>販売の詳細を確認します


アプリの送信中に確認、**販売詳細**ストアの送信のチェックリストに項目を表示することを確認してください。

**UWP デバイスのアプリのためには、アプリは無料でなければなりません。**

**アプリは、無料の販売し、証明に合格した後にリリース schedued が。**

アプリの提出 UI は、アプリがデバイスに関連付けられている UWP デバイス アプリでかどうかをチェックの唯一の手段として StoreManifest.xml を探すように設計されています。 設定した販売詳細で、アプリがない試用版を無料に設定されているかどうかを確認することを明示的にオーバーライドしたらその決定が、(これらの値を変更しようとする場合、コントロールを無効にして、**販売詳細**ページ)。 これは、チェックリストのページに反映されます。

表示されない場合**UWP デバイスのアプリのために、アプリが無料にする必要があります**で、**販売詳細** ページとではなく、アプリ プロジェクトのルート フォルダーで StoreManifest.xml が正しく含まれることを確認します。ソリューションのルート フォルダー。

## <a name="span-idsubmissionresultsspanspan-idsubmissionresultsspanspan-idsubmissionresultsspansubmission-results"></a><span id="Submission_results"></span><span id="submission_results"></span><span id="SUBMISSION_RESULTS"></span>送信結果


Microsoft Store がアプリを受け取ると、すべての UWP アプリに共通する自動テストのスイートが実行されます。 一連のアプリに固有のテストも実行します。

場合は、アプリが Microsoft Store によって適用されるテストに合格、約 1 ~ 4 日間にアプリ カタログに追加するされます。 カタログでは後、は使用も、Microsoft Store からです。 送信に失敗した場合、原因に関する通知されます。

## <a name="span-idvalidationspanspan-idvalidationspanspan-idvalidationspanvalidation"></a><span id="Validation"></span><span id="validation"></span><span id="VALIDATION"></span>検証


Microsoft Store のダッシュ ボードは、Microsoft Store に送信された後に、デバイスの Microsoft Store アプリ パッケージを検証します。 デバイスのメタデータに送信され、Windows デベロッパー センター ハードウェア ダッシュ ボードによって検証します。 検証プロセスでは、メタデータで指定されたアプリが、ストア チェックがあるため、アプリが Microsoft Store、上でライブでは、メタデータを提出する必要があります。 ハードウェア ダッシュ ボードのロゴの提出マテリアルの一部として個別に、ドライバーを検証します。

## <a name="span-idnextstepspanspan-idnextstepspanspan-idnextstepspannext-step"></a><span id="Next_step"></span><span id="next_step"></span><span id="NEXT_STEP"></span>次の手順


[手順 6:デバイス メタデータを提出します。](step-6--submit-device-metadata.md)

 

 





