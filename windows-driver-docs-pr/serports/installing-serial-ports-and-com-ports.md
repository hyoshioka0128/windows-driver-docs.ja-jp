---
title: シリアル ポートと COM ポートをインストールする
description: シリアル ポートと COM ポートをインストールする
ms.assetid: 9c755dfa-65e5-4ecb-8544-dd63c6b69c8e
keywords:
- WDK のシリアル ポート
- COM ポートの WDK シリアル デバイス
- シリアル ドライバー WDK では、COM ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00f3d00b7b73fa129886fcaca98a9bace1873ba7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331138"
---
# <a name="installing-serial-ports-and-com-ports"></a>シリアル ポートと COM ポートをインストールする





ほとんどのデバイスでは、ポートの[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)シリアル関数ドライバーは、シリアル ポートや COM ポートを操作するために必要な機能を提供します。 シリアル ポートとこれらのシステム提供のコンポーネントを使用して COM ポートをインストールするには、次の操作を行います。

-   ポートのサービスとしてのポートのデバイス セットアップ クラスとシリアル機能ドライバーを指定する INF ファイルを提供します。

-   COM ポートとしては、シリアル ポートを構成するで定義されている要件を満たす[COM ポートの構成](configuration-of-com-ports.md)します。

シリアル ポートとポートのデバイス セットアップ クラスと、シリアル機能ドライバーを使用して COM ポートをインストールする方法の詳細については、次のトピックを参照してください。

[プラグ アンド プレイ シリアル ポートおよび COM ポートをインストールします。](installing-plug-and-play-serial-ports-and-com-ports.md)

[従来の COM ポートをインストールします。](installing-legacy-com-ports.md)

COM ポートのカスタム インストールを実行する場合に定義されている COM ポートの要件を遵守しなければなりません[COM ポートの構成](configuration-of-com-ports.md)します。

 

 




