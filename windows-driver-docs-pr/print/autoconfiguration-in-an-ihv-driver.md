---
title: IHV、ドライバーの自動構成
description: IHV、ドライバーの自動構成
ms.assetid: 81febae0-6fab-4226-9e98-7705d606caf4
keywords:
- IHV ドライバーの自動構成の WDK プリンター
- 自動構成の WDK プリンター、IHV ドライバー
- プリンターの自動構成の WDK プリンター、IHV ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb13bbf726003ee037c4cf392f4fc90826e2539d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549166"
---
# <a name="autoconfiguration-in-an-ihv-driver"></a>IHV、ドライバーの自動構成


自動構成をサポートしているスタンドアロン IHV ドライバーでは、次の要件を満たす必要があります。

1.  次の Microsoft[双方向通信スキーマ](https://msdn.microsoft.com/library/windows/hardware/ff545175)と[双方向の通信インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff545163)Windows SDK のドキュメントで説明されています。

2.  プリンターのサポート\_イベント\_構成\_で更新プリンター イベント、 [ **DrvPrinterEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff548564)関数。

3.  受信した通知を理解する bidi 通知スキーマの機能を把握します。 参照してください[双方向通信スキーマ](bidirectional-communication-schema.md)します。

**注**  自動構成サポートを提供するために、スタンドアロンのドライバーを作成する必要はありません。 代わりに、GPD または PPD ファイルを利用する Microsoft のプリンターのいずれかのクラス ドライバーを記述することができます。 詳細については、[自動構成のインボックス サポート](in-box-support-for-autoconfiguration.md)を参照してください。

 

 

 




