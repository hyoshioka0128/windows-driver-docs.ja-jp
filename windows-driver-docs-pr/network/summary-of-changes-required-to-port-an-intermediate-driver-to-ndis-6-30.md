---
title: NDIS 6.30 に中間のドライバーのポートへの変更の概要
description: ドライバーを更新するには、NDIS 6.x 中間 (IM) NDIS 6.30 をサポートするために、次のセクションで説明したよう変更する必要があります。
ms.assetid: 02FAC8B2-16B1-49C2-8B3A-29535A698CEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 006c3baf552407484f36085a8b9c8f53044e61e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376916"
---
# <a name="summary-of-changes-required-to-port-an-intermediate-driver-to-ndis-630"></a>中間ドライバーを NDIS 6.30 に移植するために必要な変更の概要


ドライバーを更新するには、NDIS 6.x 中間 (IM) NDIS 6.30 をサポートするために、次のセクションで説明したよう変更する必要があります。

## <a name="build-environment"></a>環境を構築します。


-   NDIS630 で存在する場合、NDIS60 または NDIS61 NDIS620、プリプロセッサの定義を置き換えます。
-   メジャーおよびマイナーの NDIS バージョン番号、NDIS で更新\_*Xxx*\_ドライバー\_特性構造」の説明に従って[NDIS 6.30 ドライバーを実装する](implementing-an-ndis-6-30-driver.md).

## <a name="general-porting-requirements"></a>移植の一般的な要件


-   プロトコル ドライバーおよびミニポート ドライバーの変更はない限りそれ以外の場合も中間ドライバーに適用されます。 これらのドライバーの移植の詳細については、次を参照してください、[概要の変更に必要なポート、プロトコルまたはフィルター ドライバーには、NDIS 6.30](summary-of-changes-required-to-port-a-protocol-or-filter-driver-to-ndis-6-30.md)と[概要の変更に必要なポートの NDIS 6.30に、ミニポートドライバー](summary-of-changes-required-to-port-a-miniport-driver-to-ndis-6-30.md).

 

 





