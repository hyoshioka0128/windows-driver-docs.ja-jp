---
title: Visual Studio でのサービス メタデータの提出パッケージの作成
description: Visual Studio でのサービス メタデータの提出パッケージの作成
ms.assetid: 93C2F66B-EAD3-4C7B-A761-E0AF861101D0
keywords:
- Visual Studio でのサービス メタデータの提出パッケージの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad5168e4e74f1fb56cdd6c4cb92dd548ff857cc0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529803"
---
# <a name="creating-a-service-metadata-submission-package-in-visual-studio"></a>Visual Studio でのサービス メタデータの提出パッケージの作成


提出パッケージを作成するのにには、Microsoft Visual Studio での送信ツールを使用します。

### <a name="span-idtocreateasubmissionpackagespanspan-idtocreateasubmissionpackagespanspan-idtocreateasubmissionpackagespanto-create-a-submission-package"></a><span id="To_create_a_submission_package"></span><span id="to_create_a_submission_package"></span><span id="TO_CREATE_A_SUBMISSION_PACKAGE"></span>提出パッケージを作成するには

1.  をクリックして、**ドライバー**メニューの **デバイス メタデータ**、し、**送信**します。
2.  クリックして**メタデータ パッケージの追加**および検索、およびメタデータ パッケージを選択し、順にクリックします**オープン**します。
3.  確認、**パッケージ名**と**モデル名**、し、**プレビュー**パッケージをプレビューする場合。

    **注**  、**モデル名**フィールドは、**サービス プロバイダー**サービス メタデータ パッケージの一部として指定されている名前。

     

4.  **[次へ]** をクリックします。
5.  レビュー、**モデル名**、**ハードウェア Id**、および**ID エクスペリエンス**します。
6.  横に**エクスペリエンス名前**経験の名前を入力します。
    **注**  サブミッション パッケージのすべては、この手順が必要です。

     

7.  横に**認定**を選択します**このデバイスには、関連付けられているロゴまたは unclassified 送信**一覧から。
8.  前に、パッケージが送信される場合は、選択**更新プログラムのエクスペリエンス**します。
9.  **[次へ]** をクリックします。
10. モバイル ブロード バンド プロバイダーの情報を確認するには、ハードウェア ID の情報 (IMSI または ICCID など) を再入力します。 プレーン テキストのハードウェア ID の情報は、メタデータ パッケージで指定されたハッシュのハードウェア Id を確認する、Windows デベロッパー センター ハードウェア ダッシュ ボードで使用されます。
11. パッケージが署名していない場合は、署名にこれらの手順に従います。

    1.  証明書ファイルを検索し、ダブルクリックしてインストールします。
    2.  ユーザー ストアに格納され、コンピューター ストアではなく、証明書ファイルをインストールすることを確認します。
    3.  クリックして**署名ウィザードを起動して**します。
    4.  クリックして**選択ストア**します。
    5.  ダイアログ ボックスから、証明書を選択します。
        **注**  署名ウィザード内のファイル名は、受信したものを送信メタデータのウィザードの完了後します。 したがって、特定の理由がある場合は、しない限り変更しないでファイル名またはパス。

         

    6.  署名プロセスを完了します。

12. をクリックしてパッケージを送信する準備ができたら、**起動 Windows デベロッパー センター - ハードウェア ダッシュ ボード**します。

パッケージを送信する方法の詳細については、[デバイス メタデータ パッケージの申請](https://go.microsoft.com/fwlink/p/?linkid=226302)を参照してください。

Devicemanifest ファイルに関する詳細については、[モバイル ブロード バンドの UWP アプリを送信](https://go.microsoft.com/fwlink/p/?linkid=248426)を参照してください。

Bulkmetadata ファイルに関する詳細については、[バルク メタデータ パッケージの申請](https://go.microsoft.com/fwlink/p/?linkid=248427)を参照してください。

 

 





