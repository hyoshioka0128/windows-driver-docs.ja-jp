---
Description: Device Installation
title: デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6c45211f6367ee1eb74c40863f29441dc9a36ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580437"
---
# <a name="device-installation"></a>デバイスのインストール


WPD ドライバーは、UMDF (Windows Driver Frameworks (WDF) - ユーザー モード ドライバー フレームワーク) 準拠のドライバーです。 そのため、Windows のプラグ アンド プレイ (PnP) インフラストラクチャのインストールを使用します。

エクスペリエンスを作成する、PnP 従来 PnP れないバス上のさまざまな方法はまた、PNP-X 対応のネットワーク デバイスの使用など。 これは、任意のバス経由でデバイスの探索を有効にでき、PnP コンポーネントとしてインストールする前に実行します。

デバイスのドライバーがシステムにインストールされると、クライアントがすべてインストールされ、現在アクティブな WPD デバイスを列挙するのに WPD Api を使用します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**WPD ドライバーの概要**](wpd-drivers-overview.md)

 

 





