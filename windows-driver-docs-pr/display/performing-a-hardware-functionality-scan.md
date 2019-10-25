---
title: ハードウェア機能スキャンの実行
description: ハードウェア機能スキャンの実行
ms.assetid: 966b30b7-2f08-4611-9f4d-f85b301de414
keywords:
- OPM WDK ディスプレイ、HFS
- OPM WDK ディスプレイ、ハードウェア機能スキャン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c27888c5663a0e0de5cc6558396aefcaf861a8ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829802"
---
# <a name="performing-a-hardware-functionality-scan"></a>ハードウェア機能スキャンの実行


ミニポートドライバーのハードウェア機能スキャン (HFS) を使用すると、ミニポートドライバーが必要なハードウェアと通信できるようになります。 HFS の詳細については、出力 Content Protection ドキュメントを、[出力 Content Protection と Windows Vista](https://download.microsoft.com/download/5/D/6/5D6EAF2B-7DDF-476B-93DC-7CF0072878E6/output_protect.doc)の web サイトからダウンロードしてください。

Microsoft DirectX グラフィックカーネルサブシステム (*Dxgkrnl*) が次のドライバー関数を呼び出すたびに、ディスプレイミニポートドライバーが HFS の実行を開始する必要があります。

-   [**DxgkDdiStartDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)

-   グラフィックスアダプターの電源状態が D0 に設定された[**DxgkDdiSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_set_power_state) 。

HFS は非同期にすることができ、 [**DxgkDdiStartDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)または[**DxgkDdiSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_set_power_state)が戻る前に完了する必要はありません。 ただし、 [OPM DDI](supporting-output-protection-manager.md)関数は、HFS が完了するまで返すことはできません。
