---
title: NDIS バージョン情報を指定します。
description: NDIS バージョン情報を指定します。
ms.assetid: 9d007046-01c5-4bf8-adda-b88b596945d6
keywords:
- WDK の NDIS バージョン情報
- バージョン管理の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d94e438ff72f56e4eecbeaa809bffb4b9c74867e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528363"
---
# <a name="specifying-ndis-version-information"></a>NDIS バージョン情報を指定します。





このセクションでは、サポートの概要その NDIS および NDIS ドライバーは、NDIS バージョン情報を提供します。

多くの NDIS 構造体の構造のバージョン情報は含ま、**ヘッダー**メンバー。 NDIS または NDIS ドライバーは、このような構造でバージョン情報を設定します。 NDIS ドライバーは、構造体のメンバーにアクセスする前に、構造体のバージョン情報を確認する必要があります。

また、NDIS ドライバーは、ドライバーの初期化中にサポートする NDIS バージョンを指定します。

ここでは、次のトピックについて説明します。

-   [ヘッダーのバージョンの NDIS サポートの概要](overview-of-ndis-support-for-header-versions.md)
-   [NDIS ドライバーのバージョン情報の要件](version-information-requirements-for-ndis-drivers.md)
-   [NDIS のバージョン情報の要件](version-information-requirements-for-ndis.md)
-   [NDIS 版を入手します。](obtaining-the-ndis-version.md)
-   [WMI の NDIS オブジェクト バージョンの問題](ndis-object-version-issues-for-wmi.md)

## <a name="related-topics"></a>関連トピック


[NDIS のバージョンの概要](overview-of-ndis-versions.md)

 

 






