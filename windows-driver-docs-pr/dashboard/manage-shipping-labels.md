---
title: 配送先住所ラベルを管理する
description: このドキュメントには、ハードウェア ダッシュボードでのドライバーの送信の配送先住所ラベルを更新または作成する方法に関する情報が含まれています
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 08/23/2018
ms.openlocfilehash: 8a8681daed14aafba673a74e93795ad60b3372fb
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63337177"
---
# <a name="manage-shipping-labels"></a>配送先住所ラベルを管理する

Windows ハードウェア ダッシュ ボード申請の配送先住所ラベルを管理するには、次のメソッドを使用します。 API を使用するための前提条件など、Microsoft ハードウェア ダッシュボード API の概要については、「[API を使用したハードウェア提出の管理](dashboard-api.md)」を参照してください。

```cpp
https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productid}/submissions/{submissionid}/shippingLabels
```

配送先住所ラベルを管理するためのメソッド

|説明|メソッド |URI|
|:--|:--|:--|
|[新しい配送先住所ラベルを作成する](create-a-new-shipping-label.md)|POST|`https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productid}/submissions/{submissionid}/shippingLabels`|
|[配送先住所ラベルを更新する](update-a-shipping-label.md)|PATCH|`https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productid}/submissions/{submissionid}/shippingLabels/{shippingLabelId}`|

## <a name="create-a-new-shipping-label"></a>新しい配送先住所ラベルを作成する

1. Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)を満たします (前提条件がまだ満たされていない場合)。

2. [Azure AD のアクセス トークンを取得します](dashboard-api.md#obtain-an-azure-ad-access-token)。 このアクセス トークンを Microsoft Store 申請 API のメソッドに渡す必要があります。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。

3. 配送先住所ラベルを作成するには、製品と申請を作成しておく必要があります。 製品と申請の作成について詳しくは、「[製品申請の管理](manage-product-submissions.md)」をご覧ください。

4. 次のメソッドを実行して、この申請に対する[新しい配送先住所ラベルを作成](create-a-new-shipping-label.md)します。  前の手順の「[製品申請の管理](manage-product-submissions.md)」で作成した ProductID と SubmissionID を使用します。

    ```cpp
    https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productid}/submissions/{submissionid}/shippingLabels
    ```
    応答本文には、新しく作成された配送先住所ラベルやその他の詳細情報を含んだ、[配送先住所ラベル リソース](get-shipping-labels.md#shippinglabel-resource)が含まれます。

## <a name="code-examples"></a>コード例

次のコード例は、Microsoft ハードウェア API を呼び出す方法を示しています。

* [C# のサンプル](http://download.microsoft.com/download/C/F/4/CF404E53-87A0-4204-BA13-A64B09A237C1/HardwareApiCSharpSample.zip)

## <a name="data-resources"></a>データ リソース

製品データを作成して管理するための Microsoft ハードウェア API メソッドは、次の JSON データ リソースを使用します。

* [配送先住所ラベルのリソース](get-shipping-labels.md#shippinglabel-resource)

## <a name="error-codes"></a>エラー コード

エラー コードについて詳しくは、「[Error codes (エラー コード)](get-product-data.md#error-codes)」をご覧ください。

## <a name="see-also"></a>関連項目

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
