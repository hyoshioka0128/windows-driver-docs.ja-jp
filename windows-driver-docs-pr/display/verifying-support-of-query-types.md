---
title: クエリの種類のサポートを確認しています
description: クエリの種類のサポートを確認しています
ms.assetid: 0f925796-d827-42ba-9232-8f221919e6d4
keywords:
- 非同期クエリ操作 WDK DirectX 9.0、クエリの種類のサポートを確認しています
- クエリ操作 WDK DirectX 9.0、クエリの種類のサポートを確認しています
- WDK DirectX 9.0 のクエリの種類
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6ae69298ebf203a16f2edbb9f431947309b6dbd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537394"
---
# <a name="verifying-support-of-query-types"></a>クエリの種類のサポートを確認しています


## <span id="ddk_verifying_support_of_query_types_gg"></span><span id="DDK_VERIFYING_SUPPORT_OF_QUERY_TYPES_GG"></span>


DirectX 9.0 ランタイムでは、すべて非同期クエリ操作の前に、ドライバーをサポートするどのクエリの種類を実行することができますを確認してください。 ドライバーがサポートするクエリの種類の数を確認するランタイムの送信、 **GetDriverInfo2** 、D3DGDI2 を使用して要求\_型\_GETD3DQUERYCOUNT 値。 ドライバーが任意のクエリの種類をサポートしていない場合に 0 を返します、 **dwNumQueries**のメンバー、 [ **DD\_GETD3DQUERYCOUNTDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551539)この構造体要求。

各に関する情報を受信するサポートされているクエリの種類、ランタイムが送信を**GetDriverInfo2** 、D3DGDI2 を使用して要求\_型\_GETD3DQUERY 値の種類ごと。 ドライバーが後でクエリの種類に関する情報を返します、 [ **DD\_GETD3DQUERYDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551541)構造体。 詳細については**GetDriverInfo2**を参照してください[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。

 

 





