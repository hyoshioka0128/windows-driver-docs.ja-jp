---
title: Visual Studio でのサービス メタデータ申請パッケージの作成
description: Visual Studio でのサービス メタデータ申請パッケージの作成
ms.assetid: 93C2F66B-EAD3-4C7B-A761-E0AF861101D0
keywords:
- Visual Studio でのサービス メタデータ申請パッケージの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cef866f572eeeeb80afab105a978bf36cadeb669
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769532"
---
# <a name="creating-a-service-metadata-submission-package-in-visual-studio"></a>Visual Studio でのサービス メタデータ申請パッケージの作成


送信パッケージを作成するには、Microsoft Visual Studio の送信ツールを使用します。

### <a name="span-idto_create_a_submission_packagespanspan-idto_create_a_submission_packagespanspan-idto_create_a_submission_packagespanto-create-a-submission-package"></a><span id="To_create_a_submission_package"></span><span id="to_create_a_submission_package"></span><span id="TO_CREATE_A_SUBMISSION_PACKAGE"></span>送信パッケージを作成するには

1.  [**ドライバー** ] メニューをクリックし、[**デバイスメタデータ**] を選択して、[**送信**] を選択します。
2.  [**メタデータパッケージの追加**] をクリックし、メタデータパッケージを検索して選択し、[**開く**] をクリックします。
3.  パッケージ**名**と**モデル名**を確認し、パッケージをプレビューする場合は [**プレビュー** ] を選択します。

    **メモ**   [**モデル名**] フィールドは、サービスメタデータパッケージの一部として指定された**サービスプロバイダー**名です。

     

4.  **[次へ]** をクリックします。
5.  **モデル名**、**ハードウェア Id**、および**エクスペリエンス ID**を確認します。
6.  [**エクスペリエンス名**] の横に、エクスペリエンスの名前を入力します。
    **メモ**   この手順は、すべてのパッケージの送信に必要です。

     

7.  [**修飾**] の横にある [**このデバイスには、関連付けられたロゴまたは未分類の送信が**ある] を選択します。
8.  パッケージが前に送信されている場合は、[**更新エクスペリエンス**] を選択します。
9.  **[次へ]** をクリックします。
10. ハードウェア ID 情報 (IMSI や ICCID など) を再入力して、モバイルブロードバンドプロバイダーの情報を確認します。 プレーンテキストのハードウェア ID 情報は、Windows デベロッパーセンターのハードウェアダッシュボードで、メタデータパッケージに指定されているハッシュされたハードウェア Id を確認するために使用されます。
11. パッケージに署名していない場合は、次の手順に従って署名します。

    1.  証明書ファイルを探し、ダブルクリックしてインストールします。
    2.  証明書ファイルは、コンピューターストアではなく、ユーザーストアにインストールしてください。
    3.  [**署名ウィザードの起動**] をクリックします。
    4.  [**ストアの選択] を**クリックします。
    5.  ダイアログボックスから証明書を選択します。
        **メモ**   署名ウィザードのファイル名は、メタデータの送信ウィザードの完了後に表示されます。 そのため、特定の理由がない限り、ファイル名またはパスを変更しないでください。

         

    6.  署名プロセスを完了します。

12. パッケージを送信する準備ができたら、[ **Windows デベロッパーセンターの起動-ハードウェアダッシュボード**] をクリックします。

パッケージを送信する方法の詳細については、「[デバイスメタデータパッケージを送信](https://docs.microsoft.com/windows-hardware/drivers/dashboard/submit-a-device-metadata-package--dashboard-help-)する」を参照してください。

デバイスマニフェストファイルの詳細については、「[モバイルブロードバンドデバイスマニフェストパッケージを送信する](https://docs.microsoft.com/windows-hardware/drivers/dashboard/submit-a-mobile-broadband-device-manifest-package)」を参照してください。

Bulkmetadata ファイルの詳細については、「[一括メタデータパッケージの送信](https://docs.microsoft.com/windows-hardware/drivers/dashboard/submit-a-bulk-metadata-package)」を参照してください。

 

 





