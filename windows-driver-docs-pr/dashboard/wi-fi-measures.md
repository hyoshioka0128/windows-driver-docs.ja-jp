---
title: Wi-Fi の測定値
description: カメラの測定値では、Bluetooth ドライバーのフライティング時に、良性の初期化エラーがフィルターで除外されます
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: c2db79496dc7ffb4355efa9d0eb9e73481b244e0
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016988"
---
# <a name="wi-fi-measures"></a>Wi-Fi の測定値

## <a name="description"></a>説明

Microsoft は、WLAN デバイスの製造元に WLAN デバイス ドライバー インターフェイス (WDI) を提供します。 製造元は WDI 対応ドライバーとして、デバイス プラットフォーム上で機能的で、WLAN ドライバーの品質が高く、ドライバー パッケージが複雑でないユニバーサル ドライバーを開発できます。 WDI 対応ドライバーをマシンに使用することで、その Wi-Fi コンポーネントおよび Windows OS が通信可能になり、エンド ユーザーがワイヤレス ネットワークを利用できるようになります。 WDI ドライバー開発の情報について詳しくは、「[WLAN ユニバーサル Windows ドライバー モデル](https://docs.microsoft.com/windows-hardware/drivers/network/wifi-universal-driver-model)」を参照してください。

Wi-Fi の測定値では、マシンの信号品質に基づいてイベントをフィルターで除外します。Wi-Fi 接続のうち最も品質の低い 5% をフィルターで除外する場合もあります。 これにより、品質を評価する際のノイズが減少します。 さらに、Wi-Fi と Bluetooth のコンポーネントは相互に作用することが多く、同じデバイスに統合できるので、Wi-Fi ドライバーは [Bluetooth の測定値](bluetooth-measures.md)でも評価されます。
