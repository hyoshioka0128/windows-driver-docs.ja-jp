---
title: クライアント側レンダリング
description: クライアント側レンダリング
ms.assetid: 7b67de2a-b5aa-4d8c-9b2c-9caeffdb71c3
keywords:
- 印刷ジョブの WDK では、クライアント側のレンダリング
- WDK の印刷ジョブの表示
- クライアント側のレンダリング WDK を印刷します。
- 印刷スプーラの印刷ジョブのレンダリング WDK
- 印刷ジョブの表示のスプーラー WDK を印刷します。
- ジョブ WDK の印刷、クライアント側のレンダリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bef7c62d7324045175bedc008f44046a682f3d60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351950"
---
# <a name="client-side-rendering"></a>クライアント側レンダリング


印刷ジョブの表示は、Windows Vista を実行しているクライアント コンピューターで、既定の場所を受け取る。

Windows 2000 では、前に Windows クライアント コンピューター上の印刷ジョブを表示して、表示されたデータは、印刷のプリント サーバーに送信されました。 Windows 2000 以降と Windows Vista より前に、印刷ジョブの表示は、プリント サーバー上の場所にかかりました。 プリント サーバー、クライアント コンピューターよりも処理能力を提供するために、Windows 2000 以降のサーバーを印刷する印刷ジョブの表示が移動されました。 強力なプリント サーバーは、印刷ジョブのレンダリングのプロセッサを要するタスクを完了し、でした。

最近では、ただし、クライアント コンピューター多くの場合、リソースがある使用可能なプロセッサのプリント サーバーよりもします。 さらに、多くのプリント サーバーでは、複数の印刷キューを処理し、ファイル、Web、およびメール サーバーとしても機能します。

以降 Windows Vista では、印刷スプーラをレンダリングの印刷ジョブ ローカルに既定でします。 この種類のレンダリングを有効にする、印刷スプーラーが変更されたが、プリンター ドライバーと、エンドユーザーは何らかの変更を確認できません。 ほとんどのプリンター ドライバーを変更したり、クライアント側のレンダリングを正常に使用して、必要としません。ただし、記載されているいくつかの例外がある[クライアント側のレンダリングに関する既知の問題](known-issues-with-client-side-rendering.md)します。

このセクションの内容:

[クライアント側のレンダリングの概要](client-side-rendering-overview.md)

[クライアント側のレンダリングに関する既知の問題](known-issues-with-client-side-rendering.md)

[クライアント側のレンダリングのためのベスト プラクティス](best-practices-for-client-side-rendering.md)

 

 




