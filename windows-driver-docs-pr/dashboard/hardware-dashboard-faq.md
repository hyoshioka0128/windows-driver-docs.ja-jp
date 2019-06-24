---
title: パートナー センターに関する FAQ
description: この記事では、パートナー センターについてよく寄せられる質問に対してお答えします。
ms.assetid: AA3D1147-7015-4D21-84A6-D127F57DDC97
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 911a3dc086bb07f691ca1fd9bc41548952d22bbb
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "65106397"
---
# <a name="hardware-dashboard-faq"></a>ハードウェア ダッシュボードに関する FAQ

この記事では、パートナー センターについてよく寄せられる質問に対してお答えします。

## <a name="how-do-i-contact-partner-center-support"></a>パートナー センターのサポートに問い合わせるにはどうすればよいですか。

ダッシュボードにアクセスできない場合や、ダッシュボード サポートが必要な場合は、こちらからサポート チケットを開いてください: https://developer.microsoft.com/windows/support 。  **[お問い合わせ先]** を選択し、ドロップダウン リストから **[ダッシュボードの問題]** と **[ハードウェアの申請と署名 (すべての OS バージョン)]** をそれぞれ選択してください。  ライブ チャットと電子メール サポートの受付時間は、月曜日から金曜日の午前 8 時から午後 8 時 (CST) です。  電子メール サポートの初回応答の SLA は、24 時間から 48 時間です。

## <a name="can-i-associate-multiple-certificates-with-a-dashboard-account"></a>ダッシュボード アカウントに複数の証明書を関連付けることができますか。

組織は、ダッシュボード アカウントに複数の証明書を関連付けることができます。 これらの証明書のいずれかで提出が署名されている必要があります。

組織に関連付けられる証明書 (EV と標準の両方) の数に制限はありません。

## <a name="what-agreements-need-to-be-signed"></a>どのような契約に署名する必要がありますか。

次の契約には、登録プロセスの一環として署名できます。

> [!NOTE]
> Windows ハードウェア互換性プログラムのテスト契約への署名は、すべての登録における要件です。 その他のすべての契約は、関連するその他の契約の機能またはアセットを使用している場合を除き、省略できます。 

* Windows ハードウェア互換性プログラムのテスト契約 (バージョン 2.0)

* ハードウェア用のロゴ使用許諾契約書 (バージョン 2017)

* UEFI 補遺

* Windows エラー報告 (WER) 契約 (バージョン 1.3)

## <a name="how-do-i-add-additional-users-or-grant-additional-roles-to-users-in-my-company"></a>ユーザーを追加する方法と社内のユーザーに他の役割を付与する方法を教えてください。

詳しくは、「[ユーザー ロールの管理](managing-user-roles.md)」をご覧ください。

## <a name="managing-submissions"></a>申請の管理

### <a name="what-is-the-hardware-certification-submission-processing-time"></a>ハードウェア認定の申請の処理時間はどれぐらいですか。

ダッシュボードへのすべてのハードウェア申請は、申請に手動レビューが必要かどうかに応じて 5 営業日以内に処理されます。 申請のテストが失敗した場合、申請に有効なフィルターが適用されていない場合、または社内のビジネス ポリシーによって要求されている場合は、手動によるレビューが必要になることがあります。

### <a name="why-do-i-see-a-difference-in-download-signed-files"></a>ダウンロードした署名済みのファイルに違いがあるのはなぜですか。

Windows 10 では、パフォーマンスに影響を与えずに安全性を高めるために、すべてのバイナリが埋め込み署名を受信するようになりました。 これは、Windows 10 の申請だけではなく、認定を目的としたすべての申請に適用されます。

### <a name="how-to-get-a-single-cat-file-if-drivers-are-uniform-for-all-operating-systems"></a>すべてのオペレーティング システムのドライバーが統一されている場合に cat ファイルを 1 つにする方法

**[パッケージ]** タブで、最終的なパッケージにドライバー フォルダーが 1 つ設定され、ドライバーのプロパティにテスト済みのすべてのオペレーティング システムが含まれるようにします。 詳しくは、「[複数のバージョンの Windows で Microsoft によって署名されたドライバーを取得する方法](get-drivers-signed-by-microsoft-for-multiple-windows-versions.md)」をご覧ください。

### <a name="im-unable-to-add-new-marketing-names-to-the-approved-submission"></a>新しいマーケティング名を承認済みの申請に追加できません

設定されている発表日を確認します。 発表日が過ぎている場合は、新しい名前を追加することはできません。

### <a name="how-can-i-share-a-link-to-a-windows-certification-verification-report"></a>Windows 認定検証レポートへのリンクを共有するにはどうすればよいですか。

* 共有可能な URL には、以下に示すようにスラッシュで区切られた 3 つの ID 番号が含まれています。`https://developer.microsoft.com/dashboard/hardware/driver/DownloadCertificationReport/SellerID/PrivateProductID/SubmissionID`

* URL で使用される ID 番号とそれらの ID を確認できる場所は次のとおりです。

| Component | 説明 |
| ---       | ---         |
|SellerID   | パートナー アカウントの ID 番号。 アカウント管理ページの **[アカウント設定]** の下に表示されます。 |
|PrivateProductID | 各製品の作成に伴って生成される ID 番号。 製品のドライバーの詳細ページで確認できます。 詳しくは、「[ダッシュボード ID 定義](https://docs.microsoft.com/windows-hardware/drivers/dashboard/id-definitions)」をご覧ください。 |
|SubmissionID | 各申請と申請の各更新に対して割り当てられる ID 番号。 製品のドライバーの詳細ページで確認できます。 詳しくは、「[ダッシュボード ID 定義](https://docs.microsoft.com/windows-hardware/drivers/dashboard/id-definitions)」をご覧ください。 |

* 共有可能なリンクを作成するには、上の URL の例に含まれている **SellerID**、**PrivateProductID**、**SubmissionID** を適切な ID 番号と置き換えます。
* この URL があれば、事前の承認やパートナー センターへのアクセス許可がなくても、レポートにアクセスしてダウンロードできます。

## <a name="troubleshooting-submission-upload-errors"></a>提出のアップロード エラーのトラブルシューティング

### <a name="my-driver-signing-submission-fails-with-the-error-there-are-files-at-the-root-of-the-cabinet-or-no-inf-files-found-in-driver-directorydirectories-xyz"></a>ドライバーの署名の提出が、"There are files at the root of the cabinet (キャビネットのルートにファイルがあります)"、または "\#No .inf files found in driver directory/directories: XYZ (ドライバー ディレクトリ:XYZ" で .inf ファイルが見つかりません)" というエラーで失敗します。

失敗の原因は .cab ファイルの構造が正しくないためです。 .cab の構造は、.cab ファイルのサブフォルダーではなく、ルート フォルダーにドライバー ファイルを配置して作成されています。 ドライバー署名の提出のために適切な .cab ファイルを作成する方法については、「[一般リリースのためのカーネル ドライバーへの構成証明署名](attestation-signing-a-kernel-driver-for-public-release.md)」をご覧ください。

### <a name="it-looks-like-your-package-is-corrupt-or-missing-important-information-ensure-you-are-using-the-latest-version-of-the-kit-regenerate-your-package-and-try-again-if-you-continue-to-experience-the-issue-contact-support"></a>"パッケージは、破損しているか、重要な情報が不足していると考えられます。 キットの最新バージョンを使用していることを確認し、パッケージを再生成してもう一度やり直してください。 問題が解決しない場合は、サポートにお問い合わせください。" という内容のエラーが表示されます。

パッケージの提出についての問題が継続して発生する場合、ダッシュボード ヘッダーでサポートにお問い合わせください。

### <a name="file-is-using-zip644gbfile-size"></a>"ファイルは Zip64 (4 gb + ファイル サイズ) を使用します"

このエラーは、アップロードされたアーカイブのファイルの種類が .zip ではなく .zip64 である場合に発生します。 この原因はファイル サイズが大きいためです。 このエラーを解決するには、次の手順を使って提出をもう一度パッケージ化します。

1. ファイルの名前を現在の .hckx/hlkx から .zip に変更します。
2. フォルダーを展開します。
3. フォルダーを開きます。
4. すべての項目を選択し、右クリックして、 **[Send to Compressed zip folder]** (圧縮された zip フォルダーへ送信) を選択します。
5. 新しい .zip フォルダーの名前を .hckx/.hlkx に変更します。
6. 新しい .hckx/.hlkx ファイルをアップロードします。

### <a name="the-dua-package-error-shows-failed-to-open-package-with-the-error-not-compatible-with-a-version-3200-with-this-instance-package-manager"></a>DUA パッケージのエラーで、"Failed to open package (このファイルを開けません)" と共にエラー "Not compatible with a version (3.2.0.0) with this instance package manager (このインスタンスのパッケージ マネージャーはバージョン (3.2.0.0) と互換性がありません)" が表示されます

* [HLK Studio](https://msdn.microsoft.com/library/windows/hardware/dn939927) のページを使用して、ダウンロード済みの DUA シェル パッケージを開き、DUA 申請を作成します。
