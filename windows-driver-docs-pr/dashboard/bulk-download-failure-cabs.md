---
title: エラー CAB の一括ダウンロード
description: CabURL を取得し、エラー CAB をダウンロードするには、Get Report Data API の一部として提供されるレポートを使います。
ms.author: shganesh
ms.date: 09/01/2018
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 5afb3cf56642ec6a28827ee3d6df0afcd2b10874
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "63337282"
---
# <a name="bulk-download-failure-cabs"></a>エラー CAB の一括ダウンロード

このメソッドを使用すると、[Get Report Data](get-report-data.md) API の一部としてレポートから取得された failureHash と applicationId を使用して、特定のエラー ハッシュに使用できるすべてのエラー CAB をダウンロードできます。

## <a name="request"></a>要求

### <a name="request-syntax"></a>要求の構文

|認証方法|要求 URI|
|----|----|
|取得|`https://manage.devcenter.microsoft.com/v1.0/my/analytics/driver/cabdownloadbatch`|

## <a name="request-header"></a>要求ヘッダー

|Header|種類|説明|
|----|----|----|
|Authorization|string|必須。 **Bearer** *\<トークン\>* という形式の Azure AD アクセス トークン。|

### <a name="request-parameters"></a>要求パラメーター

|パラメーター|種類|説明|必須|
|----|----|----|----|
|applicationId|string|エラー データを取得するドライバーの製品 ID です。|はい|
|failureHash|string|取得する詳細情報の対象となるエラーの一意の ID です。|はい|
|startDate|日付|取得するエラー報告データの日付範囲の開始日です。 既定値は、現在の日付の 30 日前です。|いいえ|
|endDate|日付|取得するエラー報告データの日付範囲の終了日です。 既定値は現在の日付です。|いいえ|
|top|int|要求で返すデータの行数です。 最大値および指定しない場合の既定値は 100 です。 クエリにこれを上回る行がある場合は、応答本文に次リンクが含まれ、そのリンクを使ってデータの次のページを要求できます。|いいえ|
|skip|int|クエリでスキップする行数です。 大きなデータ セットを操作するには、このパラメーターを使用します。 たとえば、top=100 と skip=0 を指定すると、データの最初の 100 行が取得され、top=100 と skip=100 を指定すると、データの次の 100 行が取得されます。|いいえ|

### <a name="request-example"></a>要求の例

次の例は、このメソッドを使って cabURIs を取得する方法を示しています。

```json
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/driver/cabdownloadbatch?
applicationId=13984104677400476&failureHash=1fd83f6d-9fe0-96ec-2c47-ef08b65ccbed
HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>応答

この要求の JSON 返信の本文の例を次に示します。

```json
{
  "Value": [
      {
      "applicationId": "13984104677400476",
      "submissionId": "29989690_13984104677400476_1152921504626153337",
      "failureHash": "1fd83f6d-9fe0-96ec-2c47-ef08b65ccbed",
      "cabIdHash": "fb57b37b-d364-4caf-995b-d99ae651ee18",
      "cabUrl": "https://uswewatcab09.blob.core.windows.net/kernel-20170407/fb57b37b-d364-4caf-995b-d99ae651ee18.ext.zip?sv=2015-07-08&sr=b&sig=lRVFxW%2F7GlumJHas0QxX5%2Bnvkrdi5lqijKQaGeB%2BUQA%3D&se=2017-04-28T02%3A37%3A28Z&sp=r",
      "date": "2017-04-07 13:53:43",
      "cabExpirationTime": "2017-05-07 13:53:43"
    },
    {
      "applicationId": "13984104677400476",
      "submissionId": "29989690_13984104677400476_1152921504626153337",
      "failureHash": "1fd83f6d-9fe0-96ec-2c47-ef08b65ccbed",
      "cabIdHash": "e261603b-1e86-4094-bca5-7ac4f8bf1aab",
      "cabUrl": "https://uswewatcab12.blob.core.windows.net/kernel-20170406/e261603b-1e86-4094-bca5-7ac4f8bf1aab.ext.zip?sv=2015-07-08&sr=b&sig=WCM3yNXJsIb1ME4hQICNGHBxSCWU%2FPq7ykCGNrd3lNo%3D&se=2017-04-28T02%3A37%3A28Z&sp=r",
      "date": "2017-04-07 06:17:01",
      "cabExpirationTime": "2017-05-07 06:17:01"
    }]
}
```

## <a name="see-also"></a>関連項目

- [分析レポート API (Swagger)](https://apidocs.microsoft.com/services/analyticsreportingapis)

- [エラー CAB をダウンロードする](download-failure-cabs.md)
