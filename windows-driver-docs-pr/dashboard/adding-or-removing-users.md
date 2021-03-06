---
title: ユーザーの追加または削除
description: ハードウェア ダッシュボードでは、ユーザーの管理に Azure Active Directory を使います。 このトピックでは、グローバル管理者の資格情報を使ってユーザーを追加または削除するプロセスについて説明します。
ms.assetid: 1922C767-CD34-43CD-AF90-F1FCA297EF5E
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb5dcefa805a8577e7fcbf2a008ef500d218296d
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63337335"
---
# <a name="adding-or-removing-users"></a>ユーザーの追加または削除

パートナー センターでは、ユーザーの管理に Azure Active Directory を使います。 つまり、ユーザーを追加または削除するには、デベロッパー ポータルのグローバル管理者アカウントの資格情報を使う必要があります。 グローバル管理者の資格情報を紛失したり、資格情報がわからない場合は、サポートにお問い合わせください。 なお、デベロッパー ポータル グローバル管理者アカウントの資格情報は、Azure AD グローバル管理者アカウントの資格情報と同じではないことに注意してください。

グローバル管理者は、ハードウェア プログラムの登録に使ったアカウントです。 アカウントを Sysdev から移行した場合、グローバル管理者は電子メールで通知されています。 グローバル管理者の資格情報を紛失したり、資格情報がわからない場合は、サポートにお問い合わせください。

最初に、[アカウントの設定](https://go.microsoft.com/fwlink/?linkid=833506)ページに移動し、グローバル管理者としてログインします。左側で、 **[ユーザーの管理]** を選びます。

## <a name="adding-users"></a>ユーザーの追加

ユーザーを追加するには、 **[ユーザーの追加]** を選びます。

![パートナー センターの [ユーザーの管理] メニューを示す画像](images/manage-users.png)

これにより、Azure Active Directory テナントに関連付けられたすべてのユーザーが読み込まれます。 既存のユーザーの名前の横にあるチェック チェックボックスをオンにすると、パートナー センターにそのユーザーを追加できます。 新しいユーザーをテナントに関連付けるには、 **[新しいユーザー]** を選びます。

![パートナー センターの [ユーザーの追加] メニューを示す画像](images/add-users.png)

**[新しいユーザー]** 画面で、新しいユーザーの詳細を指定します。 姓と名のほか、ログインに使うカスタム ユーザー名が必要です。 新しいユーザーは、既にディレクトリに作成済みのグループに追加することもできます。 最後に、ハードウェア プログラムに必要な役割を付与できます。

![[新しいユーザー] 画面と、新しいユーザーの登録に必要な詳細を示す画像](images/new-user-screen.png)

すべての詳細を入力し終えたら、 **[保存]** を選んで新しいユーザーの登録を完了します。 これで、選んだアクセス許可を持つユーザーがアカウントに追加され、ワンタイム パスワードが生成されます。

**注**  必ず新しいユーザー用にこのページを印刷または保存してください。 このページから移動した後、このパスワードを取得し直すことはできません。

## <a name="removing-users"></a>ユーザーの削除

ユーザーは簡単に削除できます。 **[ユーザーの管理]** ページに、現在パートナー センター アカウントにアクセスできるすべてのユーザーの一覧が表示されます。 ユーザーを削除するには、右端にある **[削除]** を選びます。

![[ユーザーの管理] 画面の [削除] ボタンを示す画像](images/remove-users.png)
