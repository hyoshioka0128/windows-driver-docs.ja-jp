---
title: IHV ドライバーの自動構成
description: IHV ドライバーの自動構成
ms.assetid: 81febae0-6fab-4226-9e98-7705d606caf4
keywords:
- IHV ドライバー自動構成の WDK プリンター
- 自動構成 WDK プリンター、IHV ドライバー
- プリンター自動構成 WDK プリンター、IHV ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0503b4b823536212b94a0814ad78e07ca0944948
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842836"
---
# <a name="autoconfiguration-in-an-ihv-driver"></a>IHV ドライバーの自動構成


自動構成をサポートするスタンドアロン IHV ドライバーは、次の要件を満たしている必要があります。

1.  Microsoft [bidi 通信スキーマ](https://docs.microsoft.com/windows-hardware/drivers/print/bidi-communications-schema-reference)と、Windows SDK のドキュメントで説明されている[bidi 通信インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)に従います。

2.  [**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)関数でプリンタ\_イベント\_構成\_プリンタイベントをサポートします。

3.  受信した通知を理解するための bidi 通知スキーマの機能に注意してください。 「 [Bidi 通信スキーマ](bidirectional-communication-schema.md)」を参照してください。

**  、** 自動構成のサポートを提供するためにスタンドアロンドライバーを作成する必要はありません。 代わりに、Microsoft printer class ドライバーのいずれかを利用する GPD または PPD ファイルを作成できます。 詳細については、「[自動構成のインボックスサポート](in-box-support-for-autoconfiguration.md)」を参照してください。

 

 

 




