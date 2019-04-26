---
title: フィルター モジュール同期 OID 要求
description: このトピックでは、フィルター モジュールの同期 OID 要求を説明します。
ms.assetid: 14C6555D-D8E6-4DEB-96C8-D4F18F06CE6B
keywords: モジュール同期 OID 要求インターフェイスを呼び出し、WDK フィルター モジュール同期 Oid、フィルター モジュールの同期 OID 要求のフィルター モジュールの同期の OID をフィルター処理します。
ms.date: 04/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ad38bda86c3cd938ae7bececf60dd5dd631e04d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350009"
---
# <a name="filter-module-synchronous-oid-requests"></a>フィルター モジュール同期 OID 要求

フィルター ドライバーを提供する同期の OID の要求パスをサポートするために、 [ *FilterSynchronousOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-filter_synchronous_oid_request)関数内のエントリ ポイント、 [ **NDIS\_フィルター\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_driver_characteristics)の呼び出し時に構造体、 [ **NdisFRegisterFilterDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfregisterfilterdriver)関数。

> [!NOTE]
> NDIS 6.81 には、同期の OID 要求インターフェイスで使用するための特定の Oid がサポートされています。 NDIS 6.80 といくつかの NDIS 6.80 Oid がサポートされていません前に存在する Oid。 同期の OID 要求インターフェイスの OID を使用できるかどうかを確認するには、OID のリファレンス ページを参照してください。

同期 OID 要求インターフェイスをサポートするには、標準の OID 要求インターフェイスのドキュメントを使用します。 次の表では、同期の OID 要求インターフェイスでの機能と標準の OID 要求インターフェイス間のリレーションシップを示します。

| 同期の OID 関数 | 標準の OID 関数 |
| --- | --- |
| [*FilterSynchronousOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-filter_synchronous_oid_request) | [*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request) |
| [*FilterSynchronousOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-filter_synchronous_oid_request_complete) | [*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request_complete) | 
