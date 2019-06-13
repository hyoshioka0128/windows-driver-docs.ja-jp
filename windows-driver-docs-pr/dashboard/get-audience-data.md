---
title: 対象ユーザー データの取得
description: Microsoft ハードウェア APIの以下のメソッドは、配送先住所ラベルで使用される、組織の対象ユーザーを取得します。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 08/21/2018
ms.openlocfilehash: 2fc033ca64fded4d2cc8a3fe00082d1e3a635d92
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63335031"
---
# <a name="get-audience-data"></a>対象ユーザー データの取得

組織の対象ユーザーを取得するには、*Microsoft ハードウェア API* の次のメソッドを使用します。 対象ユーザーを使用すると、公開を特定の構成のコンピューターに限定できます。 たとえば、テスト環境を、特定のレジストリ キーがインストールされているクライアントにのみ提供することもできます。

```cpp
https://manage.devcenter.microsoft.com/v1.0/my/hardware/audiences
```

これらのメソッドを使用するには、製品および申請をお客様自身のデベロッパー センター アカウントに用意しておく必要があります。 製品の申請を作成または管理する方法については、「[製品申請の管理](manage-product-submissions.md)」のメソッドを参照してください。

|説明|メソッド|URI|
|-|-|-|
|組織の対象ユーザーの一覧を取得します。|GET|`https://manage.devcenter.microsoft.com/v1.0/my/hardware/audiences`|

## <a name="prerequisites"></a>前提条件

Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。

## <a name="data-resources"></a>データ リソース

配送先住所ラベル データを取得するための Microsoft ハードウェア API のメソッドでは、次の JSON データ リソースが使われます。

### <a name="audience-resource"></a>対象ユーザー

このリソースは、お客様の組織に適用可能な対象ユーザーを表します。

```json
{
  "id": "9f4f44d8-bfec-48c6-a02c-2d9ea220f6e2",
  "name": "My Custom Audience",
  "description": "Matches machines that have the following registry key: HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\FOO-BAR",
  "audienceName": "Sample_Audience_Key"
}
```

このリソースには、次の値があります。

| Value | 種類 | 説明 |
|:--|:--|:--|
|id|string|対象ユーザーの ID。 これは、配送先住所ラベルで送受信される値です。|
|name|string|対象ユーザーのフレンドリ名|
|説明|string|対象ユーザーの説明|
|audienceName|string|対象ユーザーの名前|

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。

|メソッド|要求 URI|
|--|--|
|GET|`https://manage.devcenter.microsoft.com/v1.0/my/hardware/audience`|

### <a name="request-header"></a>要求ヘッダー

|Header|種類|説明|
|--|--|--|
|Authorization|string|必須。 **Bearer** *\<トークン\>* という形式の Azure AD アクセス トークン。|
|accept|string|(省略可能)。 コンテンツの種類を指定します。 許容値は “application/json” です|

### <a name="request-parameters"></a>要求パラメーター

このメソッドでは要求パラメーターを指定しないでください。

### <a name="request-body"></a>要求本文

このメソッドでは要求本文を指定しないでください。

### <a name="request-examples"></a>要求の例

次の例は、組織の対象ユーザーに関する情報を取得する方法を示しています。

```cpp
GET https://manage.devcenter.microsoft.com/v1.0/my/hardware/audience HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>応答

次の例は、組織のすべての対象ユーザーに対する要求が成功した場合に返される JSON 応答本文を示しています。 応答本文の値について詳しくは、次の表をご覧ください。

```json
{
  "value": [
    {
      "id": "9f4f44d8-bfec-48c6-a02c-2d9ea220f6e2",
      "name": "Test Registry Key",
      "description": "Matches machines that have the following registry key: HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\Test Drivers - use at own risk",
      "audienceName": "Test_Registry_Key"
    },
    {
      "id": "10415bba-3572-421b-a3de-d0d347bace5f",
      "name": "Test Audience 2",
      "description": "Additional Audeince",
      "audienceName": "Test_Audeince_2"
    }
  ],
  "links": [
    {
      "href": "https://manage.devcenter..microsoft.com/api/v1/hardware/audiences",
      "rel": "self",
      "method": "GET"
    }
  ]
}
```

このリソースには、次の値があります。

| Value | 種類 | 説明 |
|:--|:--|:--|
| value | array | 各対象ユーザーに関する情報を含むオブジェクトの配列です。 各オブジェクトのデータについて詳しくは、「[対象ユーザー](#audience-resource)」をご覧ください。 |
| links | array | コンテナー エンティティに関する役立つリンクが含まれるオブジェクトの配列です。 詳しくは、「[リンク オブジェクト](get-product-data.md#link-object)」をご覧ください。|

## <a name="see-also"></a>関連項目

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
