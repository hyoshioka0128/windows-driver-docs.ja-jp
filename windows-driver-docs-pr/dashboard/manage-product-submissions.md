---
title: 製品申請の管理
description: 製品のハードウェア ダッシュボード申請を管理し、Microsoft による署名を得ます
ms.topic: article
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d6438ed3d56dceea65e90d42753aa4954d90f3b2
ms.sourcegitcommit: 102deacad36c96892cbbc39c02f41fe68e60470b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2019
ms.locfileid: "66400870"
---
# <a name="manage-product-submissions"></a>製品申請の管理

*Microsoft ハードウェア API* の以下のメソッドを使用して製品の申請を管理し、製品が Microsoft によって署名されるようにします。 API を使用するための前提条件など、Microsoft Hardware API の概要については、「[Hardware dashboard API (ハードウェア ダッシュボード API)](dashboard-api.md)」をご覧ください。

```cpp
https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/
```

製品の申請を管理するためのメソッド

| メソッド | URI | 説明 |
|:--|:--|:--|
| GET | `https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productID}` | [特定の製品の状態/データの取得](get-a-product.md)  |
| GET | `https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productID}/submissions/{submissionId}` |[製品の特定の申請の状態/データの取得](get-a-submission.md)   |
| POST | `https://manage.devcenter.microsoft.com/v1.0/my/hardware/products` | [新しい製品の作成](create-a-new-product.md)   |
| POST | `https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productID}/submissions/` | [製品の新しい申請の作成](create-a-new-submission-for-a-product.md)  |
| POST | `https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productID}/submissions/{submissionId}/commit` |[製品申請のコミット](commit-a-product-submission.md)  |

## <a name="create-and-submit-a-product-for-signing"></a>製品を作成し、署名のために提出

1. Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)を満たします (前提条件がまだ満たされていない場合)。

2. [Azure AD のアクセス トークンを取得します](dashboard-api.md#obtain-an-azure-ad-access-token)。 このアクセス トークンを Microsoft Store 申請 API のメソッドに渡す必要があります。 アクセス トークンを取得した後、アクセス トークンを使用できるのは、その有効期限が切れるまでの 60 分間です。 トークンの有効期限が切れたら新しいトークンを取得できます。

3. Microsoft ハードウェア API の次のメソッドを実行して、[新しい製品を作成します](create-a-new-product.md)。 これにより、進行中の新しい製品が作成され、この製品のパッケージを提出することができます。

    ```cpp
    https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/
    ```

    応答本文には、この製品の ID を含む[製品リソース](get-product-data.md#product-resource)が含まれます。

4. Microsoft ハードウェア API の次のメソッドを実行して、この製品の[申請を作成します](create-a-new-submission-for-a-product.md)。  上記の手順で作成した ProductID を使用します。

    ```cpp
    https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productID}/submissions/
    ```

    応答本文に含まれる[申請のリソース](get-product-data.md#submission-resource)には、申請の ID、申請の製品 (ドライバー) パッケージを Azure Blob Storage にアップロードするための共有アクセス署名 (SAS) URI が含まれます。 [!NOTE] > SAS URI では、アカウント キーを必要とせずに、Azure Storage 内のセキュリティで保護されたリソースにアクセスできます。 SAS URI の背景情報と Azure Blob Storage での SAS URI の使用については、[Shared Access Signature 第 1 部: SAS モデルにの概要](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1)に関する記事と、「[Shared Access Signature、第 2 部: BLOB ストレージでの SAS の作成と使用](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-2/)」をご覧ください。

5. 前の手順の SAS URI で指定された場所にある Azure Blob Storage に**パッケージをアップロードします**。
次の C# コード例は、.NET 用 Azure Storage クライアント ライブラリの [CloudBlockBlob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.aspx) クラスを使用して Azure Blob Storage にパッケージをアップロードする方法を示しています。 この例では、パッケージが既にストリーム オブジェクトに書き込まれていることを前提としています。

    ```json
    string sasUrl = "https://productingestionbin1.blob.core.windows.net/ingestion/26920f66-b592-4439-9a9d-fb0f014902ec?sv=2014-02-14&sr=b&sig=usAN0kNFNnYE2tGQBI%2BARQWejX1Guiz7hdFtRhyK%2Bog%3D&se=2016-06-17T20:45:51Z&sp=rwl";
    Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob blockBob =
        new Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob(new System.Uri(sasUrl));
    await blockBob.UploadFromStreamAsync(stream);
    ```

6. 次のメソッドを実行して、[製品の申請をコミット](commit-a-product-submission.md)します。 これで、製品の申請を完了したことがハードウェア デベロッパー センターに通知され、申請の検証が開始されます。

    ```cpp
    https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productID}/submissions/{submissionId}/commit
    ```

7. 次のメソッドを実行して[製品申請の状態を取得](get-a-submission.md)して、コミット状態を確認します。

    ```cpp
    https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productID}/submissions/{submissionId}
    ```

    申請の状態を確認するには、応答本文の *commitStatus* の値を確認します。 この値が *commitReceived* から *commitCompleted* (要求が成功した場合) または *commitFailed* (要求でエラーが発生した場合) に変わっています。 エラーがある場合は、*error* フィールドにエラーについての詳細情報が含まれています。

   >[!NOTE]
   >メインの検索ページでは、約 10 分ごとに更新します。 表示するには、結果をすべて作成するには、次のようにクリックします。 **(すべて) ドライバーの一覧ページ**、上部にある、**ドライバー**パートナー センターのページ。 ページの処理し、送信の多くがある場合にロードするまでに時間がかかりますが読み込むことは成功と失敗の両方の送信が表示されます。 詳細については、次を参照してください。[ハードウェアの提出を見つける](https://docs.microsoft.com/windows-hardware/drivers/dashboard/find-hardware-submission)します。

## <a name="code-examples"></a>コード例

次のコード例は、Microsoft ハードウェア API を呼び出す方法を示しています。

* [C# のサンプル](http://download.microsoft.com/download/C/F/4/CF404E53-87A0-4204-BA13-A64B09A237C1/HardwareApiCSharpSample.zip)

## <a name="data-resources"></a>データ リソース

製品データを作成して管理するための Microsoft ハードウェア API メソッドは、次の JSON データ リソースを使用します。

* [製品リソース](get-product-data.md#product-resource)

* [申請のリソース](get-product-data.md#submission-resource)

## <a name="see-also"></a>関連項目

[ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
