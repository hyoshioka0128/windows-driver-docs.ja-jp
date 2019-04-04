---
title: NDIS フィルター ドライバーの概要
description: NDIS フィルター ドライバーの概要
ms.assetid: dcf9b992-4812-43d7-9170-1a565d8db8fb
keywords:
- フィルター ドライバーについてのフィルター ドライバー WDK ネットワーク
- フィルター ドライバーの詳細については、NDIS フィルター ドライバー WDK、
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d883cdbfb42d31392cb651e440b872d15faaa10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581009"
---
# <a name="introduction-to-ndis-filter-drivers"></a>NDIS フィルター ドライバーの概要





フィルター ドライバーは、ミニポート ドライバーのフィルター処理のサービスを提供します。 NDIS ドライバー スタックは、ミニポート ドライバーとプロトコル ドライバーが含まれます、必要に応じてフィルター ドライバーを含める必要があります。 NDIS ドライバーとドライバー スタックの詳細については、[ドライバー スタック管理](driver-stack-management.md)を参照してください。

次のアプリケーションには、フィルター ドライバーが必要です。

-   データのセキュリティまたはその他の目的でアプリケーションをフィルター処理します。

-   監視し、ネットワーク データの統計情報を収集するアプリケーション。

次のトピックでは、フィルター ドライバーの特性とサービスの概要を説明します。

[フィルター ドライバーの特性](filter-driver-characteristics.md)

[ドライバー サービスのフィルター処理](filter-driver-services.md)

[フィルター ドライバーの種類](types-of-filter-drivers.md)

[必須フィルター ドライバー](mandatory-filter-drivers.md)

 

 





