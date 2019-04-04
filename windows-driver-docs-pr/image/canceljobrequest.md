---
title: CancelJobRequest 要素
description: 必要な CancelJobRequest 操作では、クライアントがスキャン ジョブをキャンセルすることができるようにします。
ms.assetid: 781fae32-2827-48d8-8aed-7f437326919d
keywords:
- CancelJobRequest 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn CancelJobRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3028dc3472eb3cd74a87e6c9e2812a9a77b57297
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528339"
---
# <a name="canceljobrequest-element"></a>CancelJobRequest 要素


必要な**CancelJobRequest**操作には、クライアントがスキャン ジョブの取り消しができるようにします。

<a name="usage"></a>使用方法
-----

```xml
<wscn:CancelJobRequest>
  child elements
</wscn:CancelJobRequest>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

なし

## <a name="child-elements"></a>子要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="jobid.md" data-raw-source="[&lt;strong&gt;JobId&lt;/strong&gt;](jobid.md)"><strong>JobId</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

[**JobId**](jobid.md)

クライアントは、完了、キャンセル、または中止の時刻まで、ジョブが作成された時刻からスキャン ジョブをキャンセルできます。 [ **JobId** ](jobid.md)要素は、ジョブをキャンセルしようとして、クライアントを識別します。

WSD スキャン サービスに指定されたジョブを移動する必要があります、**終端**状態に、ジョブがあったかどうか、**保留中**または**Active**状態。 完了した、または取り消されたジョブを取り消すまたはをクライアントが権限を持たないすべてのジョブをキャンセルすると、エラーになります。

[**WSD スキャン サービス操作の一般的なエラー コード**](common-wsd-scan-service-operation-error-codes.md)[WSD スキャン サービス操作エラーの報告](wsd-scan-service-operation-error-reporting.md)

この操作は、のすべてを返すことができます、 [ **WSD スキャン サービス操作の一般的なエラー コード**](common-wsd-scan-service-operation-error-codes.md)します。 エラーを報告する方法の詳細については、[WSD スキャン サービス操作エラー報告](wsd-scan-service-operation-error-reporting.md)を参照してください。

**CancelJobRequest**次のエラー コードを返すことがもできます。

-   **ClientErrorJobIdNotFound**

## <a name="see-also"></a>関連項目


[**CancelJobResponse**](canceljobresponse.md)

[**JobId**](jobid.md)

 

 






