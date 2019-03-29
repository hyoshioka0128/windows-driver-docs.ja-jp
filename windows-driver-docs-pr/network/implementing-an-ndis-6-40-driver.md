---
title: NDIS 6.40 ドライバーの実装
description: NDIS 6.40、ドライバーは、NDIS 6.30 ドライバーの実装で定義されている要件に従う必要があります。
ms.assetid: 860DFD3E-F324-417A-A625-3C2935752DA2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43e4a15b40c941613d53090aabc508838100e3ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570710"
---
# <a name="implementing-an-ndis-640-driver"></a>NDIS 6.40 ドライバーの実装


NDIS 6.40、ドライバーがで定義されている要件に従う必要があります[NDIS 6.30 ドライバーを実装する](implementing-an-ndis-6-30-driver.md)します。

さらに、NDIS 6.40 ドライバーは、次の要件に準拠する必要があります。

-   NDIS 6.40 ドライバーは、NDIS に登録する際に、正しい NDIS バージョンを報告する必要があります。

    NDIS のメジャーおよびマイナー NDIS バージョン番号を更新する必要があります\_*Xxx*\_ドライバー\_NDIS 6.40 サポートの特性構造体。 **MajorNdisVersion**メンバーを含める必要があります**6**と**MinorNdisVersion**メンバーを含める必要があります**40**します。 この要件は、ミニポート、プロトコル、およびフィルター ドライバーに適用されます。 バージョン情報を更新することも必要があります。 コンパイラは、次を参照してください。 [NDIS 6.40 ドライバーをコンパイルする](compiling-an-ndis-6-40-driver.md)します。

-   Windows 8.1 および Windows Server 2012 R2 オペレーティング システムの NDIS 6.40 ミニポート ドライバーでは、データ構造の NDIS 6.40 バージョンを使用する必要があります。 詳細については、次を参照してください。 [NDIS 6.40 データ構造体を使用して](using-ndis-6-40-data-structures.md)します。

 

 





