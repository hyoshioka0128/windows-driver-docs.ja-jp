---
title: クエリの種類のサポートの確認
description: クエリの種類のサポートの確認
ms.assetid: 0f925796-d827-42ba-9232-8f221919e6d4
keywords:
- 非同期クエリ操作 WDK DirectX 9.0、クエリの種類のサポートの確認
- クエリ操作 WDK DirectX 9.0、クエリの種類のサポートの確認
- クエリの種類 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 579724169f8b5e77d31efbadf682e2b646e923c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825320"
---
# <a name="verifying-support-of-query-types"></a>クエリの種類のサポートの確認


## <span id="ddk_verifying_support_of_query_types_gg"></span><span id="DDK_VERIFYING_SUPPORT_OF_QUERY_TYPES_GG"></span>


DirectX 9.0 ランタイムは、非同期クエリ操作を実行する前に、ドライバーがサポートしているクエリの種類を確認する必要があります。 ドライバーがサポートしているクエリの種類の数を確認するために、ランタイムは D3DGDI2\_TYPE\_GETD3DQUERYCOUNT value を使用して**GetDriverInfo2**要求を送信します。 ドライバーでクエリの種類がサポートされていない場合は、この要求の[**DD\_GETD3DQUERYCOUNTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getd3dquerycountdata)構造体の**dwnumqueries**メンバーで0が返されます。

サポートされている各クエリの種類に関する情報を受信するために、ランタイムは D3DGDI2\_TYPE\_GETD3DQUERY value を使用して、各型の**GetDriverInfo2**要求を送信します。 次に、ドライバーは、クエリの種類に関する情報を[**DD\_GETD3DQUERYDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getd3dquerydata)構造体に返します。 **GetDriverInfo2**の詳細については、「 [GetDriverInfo2 のサポート](supporting-getdriverinfo2.md)」を参照してください。

 

 





