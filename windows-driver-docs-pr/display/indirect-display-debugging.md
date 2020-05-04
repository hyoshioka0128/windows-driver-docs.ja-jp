---
title: デバッグ (間接ディスプレイドライバーを)
description: 間接的な表示のデバッグ手法について説明します
ms.assetid: a343812d-03d0-4a95-9c36-7e6b5a404088
ms.date: 04/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1cb1feb250ae96882d5d77bc2327707c837296e2
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82107411"
---
# <a name="debugging-indirect-displays"></a>デバッグ (間接表示を)

間接的に表示されるドライバーは、umdf ドライバーであるため、UMDF デバッグドキュメントが適切な開始点となります。このセクションのページの例を[次](https://docs.microsoft.com/windows-hardware/drivers/wdf/determining-why-the-umdf-driver-fails-to-load-or-the-umdf-device-fails)に示します。  このページには、間接的に表示される特定のデバッグ情報が表示されます。

## <a name="span-idregistry_controlspanspan-idregistry_controlspanspan-idregistry_controlspanregistry-control"></a><span id="Registry_Control"></span><span id="registry_control"></span><span id="REGISTRY_CONTROL"></span>レジストリコントロール

IddCx には、間接ディスプレイドライバーのデバッグを支援するために使用できるレジストリ設定がいくつかあります。  すべてのレジストリ値は、 **HKLM\System\CurrentControlSet\Control\GraphicsDrivers**レジストリキーの下にあります。


| 値の名前               | 詳細 |
|--------------------------|---------|
| TerminateIndirectOnStall | 0を指定すると、フレームが使用可能になってから10秒以内にフレームが処理されない場合に、ドライバーを終了するウォッチドッグが無効になります。  それ以外の値を指定すると、ウォッチドッグは有効のままになります。 |
| IddCxDebugCtrl           | IddCx のさまざまなデバッグ側面を有効にしたビットフィールド、次の表を参照してください。 |

**メモ**TerminateIndirectOnStall レジストリ値を使用してウォッチドッグ HLK を無効にすると、テストは失敗します。

### <a name="iddcxdebugctrl-values"></a>IddCxDebugCtrl の値

| IddCxDebugCtrl のビット | 意味  |
|:---------------------:|----------|
| 0x0001 | IddCx がエラーを検出したときにデバッガーを中断する |
| 0x0002 | IddCx が読み込まれたときにデバッガーを中断する |
| 0x0004 | IddCx がアンロードされたときにデバッガーを中断する |
| 0x0008 | IddCx DriverEntry が呼び出されたときにデバッガーを中断する |
| 0x0010 | ドライバーのバインドが呼び出されたときにデバッガーを中断する |
| 0x0020 | ドライバーの開始が呼び出されたときにデバッガーを中断する |
| 0x0040 | ドライバーのバインド解除が呼び出されたときにデバッガーを中断する |
| 0x0080 | Ddi コールでドライバーを終了するときに時間がかかりすぎる DDI ウォッチドッグを無効にします |
| 0x0100 | 未使用 |
| 0x0200 | デバッグオーバーレイを有効にします。以下を参照してください |
| 0x0400 | フレーム内のダーティ rect に色の付いたアルファボックスを重ねて、0x0200 を設定する必要があります |
| 0x0800 | Pref stats を frame にオーバーレイし、0x0200 を設定する必要があります |

**メモ**どのオーバーレイ関数も、ドライバーによって作成され、IddCxSwapChainSetDevice () に渡された Direct3D デバイスを動作させるために、D3D11_CREATE_DEVICE_BGRA_SUPPORT フラグを使用して作成する必要があります。
