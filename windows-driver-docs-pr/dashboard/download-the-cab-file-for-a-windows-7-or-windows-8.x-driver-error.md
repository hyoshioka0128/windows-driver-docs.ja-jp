---
ms.assetid: 48D891CD-706C-4759-AB33-B0663774A829
description: Windows 7 や Windows 8.x のドライバー エラーに関する CAB ファイルをダウンロードするには、Microsoft Store 分析 API の以下のメソッドを使います。 このメソッドは、IHV のみを対象としています。
title: Windows 7 や Windows 8.x のドライバー エラーに関する CAB ファイルをダウンロードする
ms.date: 08/28/2018
ms.topic: article
keywords: Windows 10, UWP, Microsoft Store 分析 API, CAB のダウンロード
ms.localizationpriority: medium
ms.openlocfilehash: 672b085f6f02f096a01994d9fe598e21afba68d1
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63337253"
---
# <a name="download-the-cab-file-for-a-windows-7-or-windows-8x-driver-error"></a>Windows 7 や Windows 8.x のドライバー エラーに関する CAB ファイルをダウンロードする

> [!IMPORTANT]
> このトピックには、サポートが終了した機能に関する内容が含まれています。 この記事では、ドライバー申請エラーに関するデータを収集するための、古いメソッドについて説明しています。 これはレガシー サポートのみを目的に提供されているものです。
>
> 代わりに、次の新しいトピックを使用してください。
>
> - [ドライバー エラー詳細のカスタム レポートをスケジュールする](schedule-custom-reports-for-driver-failure-details.md)
> - [レポート テンプレートの新規作成](create-a-new-report-template.md)
> - [新しいレポートをスケジュールする](schedule-a-new-report.md)
> - [レポート データの取得](get-report-data.md)
> - [エラー CAB のダウンロード](download-failure-cabs.md)

Windows 7 や Windows 8.x の特定のドライバー エラーに関連付けられている CAB ファイルをダウンロードするには、Microsoft Store 分析 API の以下のメソッドを使います。 このメソッドを使うには、事前に [Windows 7 や Windows 8.x のドライバー エラーに関する詳細を取得する](get-details-for-a-windows-7-or-windows-8.x-driver-error.md)メソッドを使用し、ダウンロードする CAB ファイルの ID を取得しておく必要があります。

Microsoft Store 分析 API に含まれる、[Windows 7 や Windows 8.x のドライバーに関するエラー報告データを取得する](get-error-reporting-data-for-windows-7-and-windows-8.x-drivers.md)メソッドおよび [Windows 7 や Windows 8.x のドライバー エラーに関する詳細を取得する](get-details-for-a-windows-7-or-windows-8.x-driver-error.md)メソッドを使うと、Windows 7 や Windows 8.x のドライバー エラーに関する他の情報を取得できます。

> [!NOTE]
> このメソッドは、[パートナー センター プログラム](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/get-started-with-the-hardware-dashboard)に参加している開発者アカウントでのみ使用できます。

## <a name="prerequisites"></a>前提条件

このメソッドを使うには、最初に次の作業を行う必要があります。

- Microsoft Store 分析 API に関するすべての[前提条件](https://docs.microsoft.com/windows/uwp/monetize/access-analytics-data-using-windows-store-services)を満たします (前提条件がまだ満たされていない場合)。

- このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](https://docs.microsoft.com/windows/uwp/monetize/access-analytics-data-using-windows-store-services#obtain-an-azure-ad-access-token)します。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。

- ダウンロードする CAB ファイルの ID を取得します。 この ID を取得するには、[Windows 7 や Windows 8.x のドライバー エラーに関する詳細を取得する](get-details-for-a-windows-7-or-windows-8.x-driver-error.md)メソッドを使用して、特定のドライバー エラーに関する詳細情報を取得し、そのメソッドの応答本文にある **cabIdHash** の値を使います。

## <a name="request"></a>要求

### <a name="request-syntax"></a>要求の構文

| メソッド | 要求 URI                                                          |
|--------|----------------------------------------------------------------------|
| GET    | `https://manage.devcenter.microsoft.com/v1.0/my/analytics/ihvdriver/cabdownload` |

### <a name="request-header"></a>要求ヘッダー

| Header        | 種類   | 説明                                                                 |
|---------------|--------|-----------------------------------------------------------------------------|
| Authorization | string | 必須。 **Bearer** &lt;*トークン*&gt; という形式の Azure AD アクセス トークン。 |

### <a name="request-parameters"></a>要求パラメーター

| パラメーター        | 種類   |  説明      |  必須  |
|---------------|--------|---------------|------|
| cabIdHash | string | ダウンロードする CAB ファイルの一意の ID です。 この ID を取得するには、[Windows 7 や Windows 8.x のドライバー エラーに関する詳細を取得する](get-details-for-a-windows-7-or-windows-8.x-driver-error.md)メソッドを使用して、アプリの特定のエラーに関する詳細情報を取得し、そのメソッドの応答本文にある **cabIdHash** の値を使います。 |  〇  |

### <a name="request-example"></a>要求の例

次の例は、このメソッドを使って CAB ファイルをダウンロードする方法を示しています。

```syntax
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/ihvdriver/cabdownload?cabIdHash=c1a51104-d682-4230-be14-7278b18e3555 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>応答

このメソッドは 302 (リダイレクト) 応答コードを返します。また、応答に含まれる **Location** ヘッダーは、CAB ファイルの Shared Access Signature (SAS) URI に割り当てられます。 呼び出し元はこの URI にリダイレクトされ、CAB ファイルが自動的にダウンロードされます。

## <a name="related-topics"></a>関連トピック

- [Windows 7 や Windows 8.x のドライバーに関するエラー報告データを取得する](get-error-reporting-data-for-windows-7-and-windows-8.x-drivers.md)
- [Windows 7 や Windows 8.x のドライバー エラーに関する詳細を取得する](get-details-for-a-windows-7-or-windows-8.x-driver-error.md)
