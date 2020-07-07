---
title: JobHistory 要素 (省略可能)
description: オプションの JobHistory 要素には、最近処理を完了したスキャンジョブに関する情報が含まれています。
ms.assetid: 7f46044e-ac34-4181-9a35-62dea5ec8c82
keywords:
- JobHistory 要素イメージングデバイス
topic_type:
- apiref
api_name:
- wscn JobHistory
api_type:
- Schema
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: 118664d5e1d033084dcbcc65531b0b4a755f6daf
ms.sourcegitcommit: 40d7d538756767d26bbda636589f614f85a6fab3
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86020047"
---
# <a name="jobhistory-element-optional"></a>JobHistory 要素 (省略可能)

オプションの**Jobhistory**要素には、最近処理を完了したスキャンジョブに関する情報が含まれています。

## <a name="usage"></a>使用

```xml
<wscn:JobHistory>
  child elements
</wscn:JobHistory>
```

## <a name="attributes"></a>属性

属性はありません。

## <a name="child-elements"></a>子要素

| 要素 |
|--|
| [**ジョブ**](job.md) |
| [**JobSummary**](jobsummary.md) |

## <a name="parent-elements"></a>親要素

| 要素 |
|--|
| [**GetJobHistoryResponse**](getjobhistoryresponse.md) |
| [**JobTable**](jobtable.md) |

## <a name="remarks"></a>注釈

**Jobhistory**要素には、処理が完了した最新のジョブのサブセットが含まれています。 これらのジョブは、スキャンされた、中止された、または他の理由で失敗した可能性があります。 この一覧に表示されるジョブの最大数は、デバイスによって異なります。

クライアントは、 [**Getjobhistory request**](getjobhistoryrequest.md) operation 要素を使用してジョブ履歴を要求できます。 WSD Scan サービスは、この履歴を[**Getjobhistory response**](getjobhistoryresponse.md) operation 要素に返します。

## <a name="see-also"></a>こちらもご覧ください

[**GetJobHistoryRequest**](getjobhistoryrequest.md)

[**GetJobHistoryResponse**](getjobhistoryresponse.md)

[**ジョブ**](job.md)

[**JobSummary**](jobsummary.md)

[**JobTable**](jobtable.md)
