---
title: IHV ドライバーの自動構成
description: IHV ドライバーの自動構成
ms.assetid: 81febae0-6fab-4226-9e98-7705d606caf4
keywords:
- IHV ドライバーの自動構成の WDK プリンター
- 自動構成の WDK プリンター、IHV ドライバー
- プリンターの自動構成の WDK プリンター、IHV ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 718f7f1a1857e7e59f4cc219498e2debc993c79a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370472"
---
# <a name="autoconfiguration-in-an-ihv-driver"></a>IHV ドライバーの自動構成


自動構成をサポートしているスタンドアロン IHV ドライバーでは、次の要件を満たす必要があります。

1.  次の Microsoft[双方向通信スキーマ](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-communications-schema-reference)と[双方向の通信インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index)Windows SDK のドキュメントで説明されています。

2.  プリンターのサポート\_イベント\_構成\_で更新プリンター イベント、 [ **DrvPrinterEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvprinterevent)関数。

3.  受信した通知を理解する bidi 通知スキーマの機能を把握します。 参照してください[双方向通信スキーマ](bidirectional-communication-schema.md)します。

**注**  自動構成サポートを提供するために、スタンドアロンのドライバーを作成する必要はありません。 代わりに、GPD または PPD ファイルを利用する Microsoft のプリンターのいずれかのクラス ドライバーを記述することができます。 詳細については、次を参照してください。[自動構成のインボックス サポート](in-box-support-for-autoconfiguration.md)します。

 

 

 




