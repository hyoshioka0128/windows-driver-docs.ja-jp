---
title: ドライバー エラー詳細のカスタム レポートをスケジュールする
description: Microsoft ハードウェア デベロッパー センター向けのエラー レポートを作成してスケジュール設定するプロセスの概要です。
ms.topic: article
ms.author: shganesh
ms.date: 09/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: e9c6eb348b8213a2b17617ecf413afca9c57aaf6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518629"
---
# <a name="schedule-custom-reports-for-your-driver-failure-details"></a>ドライバー エラー詳細のカスタム レポートをスケジュールする

Win10/Win 8.x ドライバーのエラーおよび OEM ハードウェアのエラーに関するレポート データにアクセスするには、これらの非同期メソッドを使います。 ニーズに基づいてレポート テンプレートを定義して、スケジュールを設定することができ、そうすれば定期的にデータが送られてきます。

>[!NOTE]
>
> - これらのメソッドは、[Windows ハードウェア デベロッパー センター プログラム](https://msdn.microsoft.com/windows/hardware/drivers/dashboard/get-started-with-the-hardware-dashboard)に参加している開発者アカウントでのみ使用できます。
> - 既存のメソッドの代わりにこれらのメソッドを使って、[Windows 10 のドライバー エラー](https://docs.microsoft.com/windows/uwp/monetize/get-error-reporting-data-for-windows-10-drivers)、[Windows 7 および Windows 8.x のドライバー エラー](https://docs.microsoft.com/windows/uwp/monetize/get-error-reporting-data-for-windows-7-and-windows-8.x-drivers) (IHV の場合)、および[ハードウェア エラー](https://docs.microsoft.com/windows/uwp/monetize/get-oem-hardware-error-reporting-data) (OEM の場合) を特定できます。
> - これらのメソッドでは、新しいディメンションの豊富なセットが公開されており、最大過去 90 日まで遡ることができます。
> - API のドキュメントは、[Swagger](https://apidocs.microsoft.com/services/analyticsreportingapis) でも入手できます

## <a name="prerequisites"></a>前提条件

> [!IMPORTANT]
> 「[Enable secure data sharing (セキュリティ保護されたデータ共有を有効にする)](enable-secure-data-sharing.md)」で概説が説明されている要件を完了しておく必要があります。

このメソッドを使うには、最初に次の作業を行う必要があります。

- まだ行っていない場合は、このメソッドの要求ヘッダーで使うための Azure AD アクセス トークンの取得など、Microsoft Store 分析 API に関するすべての[前提条件](https://docs.microsoft.com/windows-hardware/drivers/dashboard/dashboard-api#complete-prerequisites-for-using-the-microsoft-hardware-api)を完了します。 アクセス トークンを取得した後、それを使用できるのは有効期限が切れるまでの 60 分間であることに注意してください。 トークンの有効期限が切れたら新しいトークンを取得できます。

詳しくは、「[Access analytics data using Microsoft Store services (Microsoft Store サービスを使用して分析データにアクセスする)](https://docs.microsoft.com/windows/uwp/monetize/access-analytics-data-using-windows-store-services)」をご覧ください

> [!IMPORTANT]
> 念のため、「[Windows Analytics Agreement (Windows Analytics 契約)](https://go.microsoft.com/fwlink/?linkid=866941)」には次のように記載されています。"個人情報を 30 日より長く格納しておくことはできません。 30 日が経過すると、個人情報は直ちに破棄されます。"

## <a name="workflow-to-schedule-custom-reports-for-driver-failure"></a>ドライバー エラーのカスタム レポートをスケジュールするワークフロー

次の図では、新しいレポート テンプレートを作成し、カスタム レポートのスケジュールを設定して、エラー データを取得するための、API 呼び出しパターンについて説明します。

![カスタム レポート テンプレートの作成、カスタム レポート テンプレートのスケジュール設定、レポート データの取得、CAB のダウンロードのワークフローを上から下の順に示した図。](./images/async-api-flow.png)

1. クライアント アプリケーションで JSON 形式を使用してレポートのスキーマを定義し、[Create Report Template API](create-a-new-report-template.md) を呼び出します。

2. 成功すると、Create New Report Template API から TemplateId が返されます。

3. クライアント アプリケーションで、TemplateId と共にレポートの開始日、繰り返し間隔、繰り返し回数を使用して、[Schedule Custom Report API](schedule-a-new-report.md) を呼び出します。

4. クライアント アプリケーションでは、スケジュール設定したレポートのデータが準備できたことの通知を受け取るためのコールバック URL を送信することもできます。

5. 成功すると、Schedule Custom Report API から ReportID が返されます。

6. データの定期的なダウンロードの準備ができると、コールバック URL で通知を受け取ります。

7. その後、クライアント アプリケーションで [Get Report Data API](get-report-data.md) と ReportID を使用し、レポート ID と日付範囲を指定してレポートの状態のクエリを実行します。

8. 成功すると、レポートのダウンロード リンクが返され、アプリケーションでデータのダウンロードを開始できます。

9. レポート データに含まれる CabIdHash を Cab Download API への入力として使用して、CAB ファイルをダウンロードできます。

10. [Cab Download API](download-failure-cabs.md) から返される CAB ダウンロード リンクを使用して、CAB ファイルをダウンロードすることができます。

## <a name="see-also"></a>関連項目

- [新しいレポート テンプレートを作成する](create-a-new-report-template.md)

- [サンプル レポート テンプレート](sample-report-templates.md)

- [分析レポート API (Swagger)](https://apidocs.microsoft.com/services/analyticsreportingapis)

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
