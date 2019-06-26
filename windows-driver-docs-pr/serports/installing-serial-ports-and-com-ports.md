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
ms.openlocfilehash: d0e5324bcde130ab16d6228bdb3fa0e53e3e0532
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384185"
---
# <a name="installing-serial-ports-and-com-ports"></a>シリアル ポートと COM ポートをインストールする

ほとんどのデバイスでは、ポートの[デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)シリアル関数ドライバーは、シリアル ポートや COM ポートを操作するために必要な機能を提供します。 シリアル ポートとこれらのシステム提供のコンポーネントを使用して COM ポートをインストールするには、次の操作を行います。

- ポートのサービスとしてのポートのデバイス セットアップ クラスとシリアル機能ドライバーを指定する INF ファイルを提供します。

- COM ポートとしては、シリアル ポートを構成するで定義されている要件を満たす[COM ポートの構成](configuration-of-com-ports.md)します。

シリアル ポートとポートのデバイス セットアップ クラスと、シリアル機能ドライバーを使用して COM ポートをインストールする方法の詳細については、次のトピックを参照してください。

[プラグ アンド プレイ シリアル ポートおよび COM ポートをインストールします。](installing-plug-and-play-serial-ports-and-com-ports.md)

[従来の COM ポートをインストールします。](installing-legacy-com-ports.md)

COM ポートのカスタム インストールを実行する場合に定義されている COM ポートの要件を遵守しなければなりません[COM ポートの構成](configuration-of-com-ports.md)します。
