---
title: WDM 下端のフラグをコンパイルします。
description: WDM 下端のフラグをコンパイルします。
ms.assetid: 60fbee2a-b8f3-4d1a-95c2-b4962a406065
keywords:
- NDIS WDM ミニポート ドライバー WDK ネットワー キング、コンパイル フラグ
- NDIS WDM ミニポート ドライバー WDK ネットワークを構築
- 下端の NDIS ミニポート ドライバー WDK ネットワー キング、コンパイル フラグ
- WDM 低い edge WDK ネットワー キング、コンパイル フラグ
- コンパイル フラグ WDK の NDIS WDM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b7fcf5c7f29e17abdb009b6e1b120b9f40bd6a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539135"
---
# <a name="compile-flags-for-wdm-lower-edge"></a>WDM 下端のフラグをコンパイルします。





NDIS WDM ミニポート ドライバーをビルドする NDIS WDM、ミニポート ドライバーのソース ファイルで、次のコンパイル フラグを含める必要があります。

-   -DNDIS\_WDM=1

    適切な WDM ヘッダー ファイルをインクルードする NDIS に指示します。

または、Ndis.h ヘッダー ファイルが含まれる前に、ミニポート ドライバーのソース コードの開始時のコンパイル フラグを埋め込むことができます。

 

 





