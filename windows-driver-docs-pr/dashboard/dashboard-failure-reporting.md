---
title: Dashboard API を使用したハードウェア障害のレポート
description: Win10/Win 8.x ドライバーのエラーおよび OEM ハードウェアのエラーに関するレポート データにアクセスするには、これらの非同期メソッドを使います。
ms.topic: article
ms.localizationpriority: medium
ms.date: 04/05/2018
ms.openlocfilehash: 28bb769ea30b7a8f14e0f68a506f128671d21b24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518781"
---
# <a name="hardware-failure-reporting"></a>ハードウェア障害レポート

Windows 8 と Windows 10 のドライバーおよび OEM ハードウェアのエラーに関するレポート データにアクセスするには、これらの非同期メソッドを使います。 

ニーズに基づいてレポート テンプレートを定義して、スケジュールを設定することができ、そうすれば定期的にデータが送られてきます。 

## <a name="prerequisites"></a>前提条件 

このメソッドを使うには、最初に次の作業を行う必要があります。 
* Microsoft Store 分析 API に関するすべての [前提条件](https://docs.microsoft.com/windows/uwp/monetize/access-analytics-data-using-windows-store-services)を満たします (前提条件がまだ満たされていない場合)。 

* このメソッドの要求ヘッダーで使う [Azure AD アクセス トークンを取得](https://docs.microsoft.com/windows/uwp/monetize/access-analytics-data-using-windows-store-services)します。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。 

詳しくは、「Microsoft Store サービスを使った分析データへのアクセス」をご覧ください  

> [!IMPORTANT]
> 念のため、「[Windows Analytics Agreement (Windows Analytics 契約)](https://go.microsoft.com/fwlink/?linkid=866941)」には次のように記載されています。"個人情報を 30 日より長く格納しておくことはできません。 30 日が経過すると、個人情報は直ちに破棄されます。" 

