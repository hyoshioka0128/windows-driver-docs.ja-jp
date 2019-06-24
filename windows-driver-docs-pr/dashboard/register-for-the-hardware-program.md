---
title: ハードウェア プログラムの登録
description: ハードウェア プログラムの登録
ms.assetid: 8E947636-7F0E-4C31-9149-D6BF60D84226
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8236e67db1829e08b493197ccce4c5fed0265463
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "65106396"
---
# <a name="register-for-the-hardware-program"></a>ハードウェア プログラムの登録

組織の管理者は、Windows ハードウェア デベロッパー センター プログラムに[登録](https://go.microsoft.com/fwlink/?LinkID=828002)する必要があります。

> [!Note]
> このプロセスでサポートが必要な場合は、 https://developer.microsoft.com/windows/support でサポート チケットを開いてください。  
>- **[お問い合わせ先]** を選択し、ドロップダウン リストから **[ダッシュボードの問題]** と **[ハードウェアの申請と署名 (すべての OS バージョン)]** をそれぞれ選択してください。  
>- ライブ チャットと電子メール サポートの受付時間は、月曜日から金曜日の午前 8 時から午後 8 時 (CST) です。  電子メール サポートの初回応答の SLA は、24 時間から 48 時間です。

## <a name="before-you-sign-up"></a>サインアップする前に

登録プロセスを開始する前に、次の要件を確認します。

- 既にある組織のデベロッパー センター アカウントをハードウェア プログラムで使用する場合は、登録を開始する前にそのアカウントでサインインします。

- 拡張検証 (EV) コード署名証明書が必要です。 組織にコード署名証明書が既にあるかどうかを確認してください。 組織に証明書が既にある場合、ファイルの署名を求められたときに証明書を利用できるようにしておきます。 組織に証明書がない場合は、登録プロセスを行っているときに証明書を購入する必要があります。

    コード署名証明書と証明書を取得する方法については、「[コード署名証明書の取得](get-a-code-signing-certificate.md)」をご覧ください。

- 組織の Azure Active Directory (Azure AD) の[全体管理者](https://go.microsoft.com/fwlink/?LinkId=746654)アカウントでサインインする必要があります。 組織で Azure AD ディレクトリを使用しているかどうかがわからない場合は、組織内の IT 部門にお問い合わせください。 組織に Azure AD ディレクトリがない場合は、Azure AD ディレクトリを作成できることが必要です。

- 組織を代表して契約書に署名する権限が必要です。

## <a name="registration-steps"></a>登録手順

ハードウェアのプログラムの登録には、5 つの主な手順があります。

1. コード署名証明書の取得

    - コード署名証明書があることを確認する

    - 証明書がない場合は、証明書を購入して利用可能にしておく必要があります。

2. signtool.exe のダウンロード
    - signtool.exe は [Windows SDK のダウンロード](https://developer.microsoft.com/windows/downloads/windows-10-sdk)の一部として取得できます。

3. 登録プロセスの**署名とアップロード**の部分で提供されたファイルに署名しアップロードします。
    > [!NOTE]
    > 以下の 3 つの手順を、同じブラウザー セッションで完了する必要がなくなりました。

    1. 提供されている署名できるファイルをダウンロードします。
    2. signtool.exe とコード署名証明書を使ってファイルに署名します。
    3. 署名されたファイルをアップロードします。 組織の名前と ID 番号が、署名されたファイルから抽出されます。

4. Azure AD グローバル管理者アカウントでのサインイン

    - 組織で既に Azure AD ディレクトリを使用している場合は、[全体管理者](https://go.microsoft.com/fwlink/?LinkId=746654)アカウントでサインインします。

    - 組織で Azure AD ディレクトリを使用していない場合は、Azure AD ディレクトリを作成し、サインインする必要があります。

5. アカウントの詳細

    - 組織の表示名と個人の連絡先情報など、アカウントの詳細を入力します。

    - 必要なハードウェア開発者の法的契約に署名します。この契約は、次に示すようにアカウント設定のタブにあります。

        !["契約" のボタンを示す画像。](images/legal-agreements-location.png)

## <a name="after-registration"></a>登録後

登録が完了すると、追加の管理タスクを利用できます。

- [ユーザーとアクセス許可の管理](managing-user-roles.md)

管理タスクを終了したら、最初のハードウェア提出を作成することができます。 詳細と操作手順については、[ハードウェア提出に関するページ](hardware-certification-submissions.md)をご覧ください。
