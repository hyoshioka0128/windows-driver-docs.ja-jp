---
title: ハードウェアの機能のスキャンを実行します。
description: ハードウェアの機能のスキャンを実行します。
ms.assetid: 966b30b7-2f08-4611-9f4d-f85b301de414
keywords:
- OPM WDK の表示、HFS
- OPM WDK の表示、ハードウェアの機能のスキャン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f4118d3b34858c9e4f86c8c2e5e2003e665faab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530273"
---
# <a name="performing-a-hardware-functionality-scan"></a>ハードウェアの機能のスキャンを実行します。


ディスプレイ ミニポート ドライバーのハードウェア機能スキャン (HFS) によりミニポート ドライバーが必要なハードウェアと通信するようになります。 HFS の詳細については、出力コンテンツの保護ドキュメントのダウンロード、[出力 Content Protection と Windows Vista](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/output_protect.doc) web サイト。

ディスプレイのミニポート ドライバーは、HFS の実行を開始する必要がありますたびに Microsoft DirectX グラフィックスのカーネル サブシステム (*Dxgkrnl.sys*) ドライバーの次の関数を呼び出します。

-   [**DxgkDdiStartDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_start_device)

-   [**DxgkDdiSetPowerState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_set_power_state)グラフィックス アダプターの電源の状態が D0 に設定します。

HFS が非同期にすることができ、前に完了する必要はありません[ **DxgkDdiStartDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_start_device)または[ **DxgkDdiSetPowerState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_set_power_state)を返します。 ただし、ありません[OPM DDI](supporting-output-protection-manager.md) HFS が完了するまで関数が返すことができます。
