---
title: セキュリティ保護されたデータ共有を有効にする
description: Hardware Dashboard API を使用して安全な方法でドライバー申請エラー データをダウンロードするために必要な手順です。
ms.author: shganesh
ms.topic: article
ms.date: 09/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: 37aadceb87ad2d3aaf183ce23efe848590df1894
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63335110"
---
# <a name="enable-secure-data-sharing"></a>セキュリティ保護されたデータ共有を有効にする

API を使用して安全な方法でドライバー申請エラー データをダウンロードするには、レポート API へのアクセスに使用した Azure AD アプリに関する次の情報を、Microsoft Store パートナー運用部門 [partnerops@microsoft.com](mailto:partnerops@microsoft.com) に送信する必要があります。

|Azure AD アプリの情報|表記|
|----|----|
|ApplicationId|*\<アプリの GUID>*|
|DisplayName|*\<アプリの名前>*|
|ホーム ページ URL|*\<URL>*|
|アプリケーションの種類|**Web アプリ**(Web アプリを想定)|
|マルチ テナント|**はい** (マルチ テナントでない場合、マルチ テナントにできますか)|

* アプリに次のアクセス許可があることを確認してください。

  * Windows AAD - **サインイン**と**ユーザー プロファイルの読み取り**

  * Azure Storage - **Azure ストレージへのアクセス**

この情報は、Azure AD アプリのダッシュボード ビューの、[登録済みのアプリ] ウィンドウ、[プロパティ] ウィンドウ、および [必要なアクセス許可] と [アクセスの有効化] のウィンドウで、見つけることができます。 次のスクリーンショットでは、データの場所を示します。

![[登録済みのアプリ]、[設定]、[プロパティ] ウィンドウのスクリーンショット](./images/app-settings.png)

![[必要なアクセス許可] と [アクセスの有効化] のウィンドウのスクリーンショット](./images/permissions-access.png)

セキュリティ保護されたデータ共有についてのヘルプおよび質問に対する回答については、Microsoft Store パートナー運用部門 [partnerops@microsoft.com](mailto:partnerops@microsoft.com) にメールでご連絡ください。
