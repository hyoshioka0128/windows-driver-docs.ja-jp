---
title: Visual Studio でのデバイス メタデータ申請パッケージの作成
description: Visual Studio でのデバイス メタデータ申請パッケージの作成
ms.assetid: 17CF8185-C9EE-4B25-BEE7-A1FFB8C92EE0
keywords:
- Visual Studio でのデバイス メタデータ申請パッケージの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9620ebccd59ad84eb556771421cfd082ab8bb82
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769692"
---
# <a name="creating-a-device-metadata-submission-package-in-visual-studio"></a>Visual Studio でのデバイス メタデータ申請パッケージの作成


デバイスメタデータ送信パッケージを作成するには、Microsoft Visual Studio の送信ツールを使用します。

1.  Visual Studio で、[**ドライバー** ] メニューをクリックし、[**デバイスメタデータ**] を選択して、[**送信**] を選択します。
2.  [**メタデータパッケージの追加**] をクリックし、パッケージを選択して [**開く**] をクリックします。
3.  **パッケージ名**と**モデル名**を確認し、パッケージをプレビューする場合は [**プレビュー** ] を選択し、[**次へ**] をクリックします。
4.  **モデル名**、**ハードウェア Id**、および**エクスペリエンス ID**を確認します。
5.  [**エクスペリエンス名**] の横に、エクスペリエンスの名前を入力します。
    **メモ**   この手順は、すべてのパッケージの送信に必要です。

     

6.  [**修飾**] の横で、一覧から次のいずれかのオプションを選択します。
    -   **このデバイスには、関連付けられているロゴまたは未分類の送信があります**
        -   **ロゴの送信 id**を入力します。
    -   **このデバイスは、受信トレイのドライバーのみを使用し、関連付けられたロゴの送信はありません**

7.  パッケージが前に送信されている場合は、[**更新エクスペリエンス**] を選択します。
8.  **[次へ]** をクリックします。
9.  パッケージに署名していない場合は、署名ウィザードで次の手順を実行して署名します。

    1.  証明書ファイルを探し、ダブルクリックしてインストールします。
    2.  証明書ファイルは、コンピューターストアではなく、ユーザーストアにインストールしてください。
    3.  [**署名ウィザードの起動**] をクリックします。
    4.  [**ストアの選択] を**クリックします。
    5.  ダイアログボックスから証明書を選択します。
        **メモ**   署名ウィザードのファイル名は、メタデータの送信ウィザードの完了後に表示されます。 そのため、特定の理由がない限り、ファイル名またはパスを変更しないでください。

         

    6.  署名プロセスを完了します。

10. パッケージを送信する準備ができたら、[ **Windows デベロッパーセンターの起動-ハードウェアダッシュボード**] をクリックします。

パッケージを送信する方法の詳細については、「[デバイスメタデータパッケージを送信](hhttps://docs.microsoft.com/windows-hardware/drivers/dashboard/submit-a-device-metadata-package--dashboard-help-)する」を参照してください。

Bulkmetadata ファイルの詳細については、「[一括メタデータパッケージの送信](https://docs.microsoft.com/windows-hardware/drivers/dashboard/submit-a-bulk-metadata-package)」を参照してください。

 

 





