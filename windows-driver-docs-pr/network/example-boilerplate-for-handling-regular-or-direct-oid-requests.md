---
title: 標準または Direct OID 要求の処理の定型コード例
description: このトピックでは、定期的なバックアップまたは直接 OID の要求を処理するための定型コードの例を説明します。
ms.assetid: 4C8297DD-C237-4437-A0B1-8CE0F3A6225B
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5e5ccc8bfaf684c6b1c765749926094b17d94e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368289"
---
# <a name="example-boilerplate-for-handling-regular-or-direct-oid-requests"></a>標準または Direct OID 要求の処理の定型コード例

このトピックでは、例では、に対して目立つように、定期的なバックアップまたは直接 OID の要求を処理する定型コードの例は[同期 OID 要求インターフェイスで NDIS 6.80](synchronous-oid-request-interface-in-ndis-6-80.md)します。 同期 OID 要求インターフェイスは、Windows 10 バージョン 1709 以降で使用できます。

```cpp
NDIS_STATUS
FilterOidRequest(
  NDIS_HANDLE     FilterModuleContext,
  PNDIS_OID_REQUEST  Request)
{
  PMS_FILTER       pFilter = (PMS_FILTER)FilterModuleContext;

  Status = NdisAllocateCloneOidRequest(pFilter->FilterHandle,
                     Request,
                     FILTER_TAG,
                    &ClonedRequest);
  if (Status != NDIS_STATUS_SUCCESS)
    return Status;

  Context = (PFILTER_REQUEST_CONTEXT)(&ClonedRequest->SourceReserved[0]);
  *Context = Request;

  ClonedRequest->RequestId = Request->RequestId;

  Status = NdisFOidRequest(pFilter->FilterHandle, ClonedRequest);

  if (Status != NDIS_STATUS_PENDING)
  {
    FilterOidRequestComplete(pFilter, ClonedRequest, Status);
    Status = NDIS_STATUS_PENDING;
  }
  return Status;
}

VOID
FilterOidRequestComplete(
  NDIS_HANDLE     FilterModuleContext,
  PNDIS_OID_REQUEST  Request,
  NDIS_STATUS     Status)
{
  PMS_FILTER             pFilter = (PMS_FILTER)FilterModuleContext;
  PNDIS_OID_REQUEST          OriginalRequest;

  Context = (PFILTER_REQUEST_CONTEXT)(&Request->SourceReserved[0]);
  OriginalRequest = (*Context);

  //
  // Copy the information from the returned request to the original request
  //
  switch(Request->RequestType)
  {
    case NdisRequestMethod:
      OriginalRequest->DATA.METHOD_INFORMATION.OutputBufferLength = Request->DATA.METHOD_INFORMATION.OutputBufferLength;
      OriginalRequest->DATA.METHOD_INFORMATION.BytesRead = Request->DATA.METHOD_INFORMATION.BytesRead;
      OriginalRequest->DATA.METHOD_INFORMATION.BytesNeeded = Request->DATA.METHOD_INFORMATION.BytesNeeded;
      OriginalRequest->DATA.METHOD_INFORMATION.BytesWritten = Request->DATA.METHOD_INFORMATION.BytesWritten;
      break;

    case NdisRequestSetInformation:
      OriginalRequest->DATA.SET_INFORMATION.BytesRead = Request->DATA.SET_INFORMATION.BytesRead;
      OriginalRequest->DATA.SET_INFORMATION.BytesNeeded = Request->DATA.SET_INFORMATION.BytesNeeded;
      break;

    case NdisRequestQueryInformation:
    case NdisRequestQueryStatistics:
    default:
      OriginalRequest->DATA.QUERY_INFORMATION.BytesWritten = Request->DATA.QUERY_INFORMATION.BytesWritten;
      OriginalRequest->DATA.QUERY_INFORMATION.BytesNeeded = Request->DATA.QUERY_INFORMATION.BytesNeeded;
      break;
  }

  NdisFreeCloneOidRequest(pFilter->FilterHandle, Request);

  NdisFOidRequestComplete(pFilter->FilterHandle, OriginalRequest, Status);
}
```

