---
title: フィルターモジュールの同期 OID 要求
description: このトピックでは、フィルターモジュールの同期 OID 要求について説明します。
ms.assetid: 14C6555D-D8E6-4DEB-96C8-D4F18F06CE6B
keywords: フィルターモジュール同期 OID 要求インターフェイス、フィルターモジュール同期 OID 呼び出し、WDK フィルターモジュール同期 oid、フィルターモジュール同期 OID 要求
ms.date: 04/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8900b4bbed1cf2935f939dda3281499ac73c0a43
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834668"
---
# <a name="filter-module-synchronous-oid-requests"></a>フィルターモジュールの同期 OID 要求

同期 OID 要求パスをサポートするために、フィルタードライバーは、 [*FilterSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-filter_synchronous_oid_request)関数のエントリポイントを[**NDIS\_フィルター\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_driver_characteristics)の構造を呼び出します[ **。NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)関数。

> [!NOTE]
> NDIS 6.81 では、同期 OID 要求インターフェイスで使用する特定の Oid がサポートされています。 NDIS 6.80 および一部の NDIS 6.80 Oid より前に存在していた Oid はサポートされていません。 同期 OID 要求インターフェイスで OID を使用できるかどうかを判断するには、「OID リファレンス」ページを参照してください。

同期 OID 要求インターフェイスをサポートするには、標準の OID 要求インターフェイスのドキュメントを使用します。 次の表は、同期 OID 要求インターフェイスの関数と標準 OID 要求インターフェイスの間の関係を示しています。

| 同期 OID 関数 | 標準 OID 関数 |
| --- | --- |
| [*FilterSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-filter_synchronous_oid_request) | [*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request) |
| [*FilterSynchronousOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-filter_synchronous_oid_request_complete) | [*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete) | 
