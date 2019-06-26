---
title: クエリの種類のサポートの確認
description: クエリの種類のサポートの確認
ms.assetid: 0f925796-d827-42ba-9232-8f221919e6d4
keywords:
- 非同期クエリ操作 WDK DirectX 9.0、クエリの種類のサポートを確認しています
- クエリ操作 WDK DirectX 9.0、クエリの種類のサポートを確認しています
- WDK DirectX 9.0 のクエリの種類
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 018eaaa9984b4ac9ada2877afe3a46af50fa7251
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374358"
---
# <a name="verifying-support-of-query-types"></a>クエリの種類のサポートの確認


## <span id="ddk_verifying_support_of_query_types_gg"></span><span id="DDK_VERIFYING_SUPPORT_OF_QUERY_TYPES_GG"></span>


DirectX 9.0 ランタイムでは、すべて非同期クエリ操作の前に、ドライバーをサポートするどのクエリの種類を実行することができますを確認してください。 ドライバーがサポートするクエリの種類の数を確認するランタイムの送信、 **GetDriverInfo2** 、D3DGDI2 を使用して要求\_型\_GETD3DQUERYCOUNT 値。 ドライバーが任意のクエリの種類をサポートしていない場合に 0 を返します、 **dwNumQueries**のメンバー、 [ **DD\_GETD3DQUERYCOUNTDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_getd3dquerycountdata)この構造体要求。

各に関する情報を受信するサポートされているクエリの種類、ランタイムが送信を**GetDriverInfo2** 、D3DGDI2 を使用して要求\_型\_GETD3DQUERY 値の種類ごと。 ドライバーが後でクエリの種類に関する情報を返します、 [ **DD\_GETD3DQUERYDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_getd3dquerydata)構造体。 詳細については**GetDriverInfo2**を参照してください[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。

 

 





