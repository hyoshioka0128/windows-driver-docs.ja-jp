---
title: NDIS 6.1 ドライバーの実装
description: NDIS 6.1 ドライバーの実装
ms.assetid: a2b5d722-88b3-4321-9d0d-451f465194d1
keywords:
- NDIS WDK、ネットワーク ドライバーのバージョン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da47aad532bd43516fd5c1eaaed3a69946638720
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574749"
---
# <a name="implementing-an-ndis-61-driver"></a>NDIS 6.1 ドライバーの実装





NDIS 6.1 ドライバーは、NDIS に登録する際に、正しい NDIS バージョンを報告する必要があります。

NDIS のメジャーおよびマイナー NDIS バージョン番号を更新する必要があります\_*Xxx*\_ドライバー\_NDIS 6.1 をサポートする特性構造体。 **MajorNdisVersion**メンバー 0x06 を含める必要があります、 **MinorNdisVersion**メンバー 0x01 を含める必要があります。 この要件は、ミニポート、プロトコル、およびフィルター ドライバーに適用されます。

 

 





