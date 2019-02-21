---
title: Windows の Bluetooth ホスト コント ローラー インターフェイス (HCI) アーキテクチャの概要
description: このトピックでは、コント ローラー インターフェイス (HCI) Bluetooth ホストをバイパスするオーディオ データを再ルーティングの Windows 8.1 のサポートのアーキテクチャの概要を示します。
ms.assetid: FC9E5254-B543-4890-811C-1DA5F28E61B9
ms.date: 10/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 60697fee2589d9b2d55f25b26f387e3b424cf404
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559058"
---
# <a name="windows-bluetooth-host-controller-interface-hci-architectural-overview"></a>Windows の Bluetooth ホスト コント ローラー インターフェイス (HCI) アーキテクチャの概要


このトピックでは、コント ローラー インターフェイス (HCI) Bluetooth ホストをバイパスするオーディオ データを再ルーティングの Windows 8.1 のサポートのアーキテクチャの概要を示します。

Windows 8.1 以降、Microsoft のオペレーティング システムが更新されました低電力チップでのシステム (SoC) 設計のソリューションと互換性があります。 新しい Windows のサポートは、Intel ベースまたは ARM ベースのいずれかの SoC 設計と互換性が。 これらの新しい低電力デバイスは、バッテリ消費が成功の鍵になるように「常時オン」のシナリオで最適化されます。

SoC アーキテクチャでは、ユニバーサル非同期 Receiver/transmitter (UART) トランスポート モードを使用して、Bluetooth ホスト コント ローラーとの間のデータを送信します。

Uart には、時間の機密データの転送を提供できません、ため、UART、オーディオ コーデックと Bluetooth 無線間 I2S またはその他のいくつかの接続を使用してオーディオ データを転送するだけでなく、同期接続指向 (SCO) バイパス チャネルを実装しなければなりません。 これは、Bluetooth HCI をバイパスするオーディオ データを再ルーティングする必要があることを意味します。 オーディオ データを送信する Pc で通常使用される Bluetooth HCI します。

この機能がユーザーの観点からは、Bluetooth ハンズフリー プロファイル (HFP) SoC の間で異なるユース ケースがないために、Windows 8.1 では、前に Windows のバージョンに存在する同じ機能をオフロードが単純に注意することが重要とWindows PC やラップトップで Bluetooth HFP します。

次の図は、Windows 8.1 のこの新しいサポートを提供するソフトウェアとハードウェア コンポーネントを示しています。

![windows で bluetooth のサポートを提供するソフトウェアとハードウェアのコンポーネントを示す図では、オーディオ ストリーミングをバイパスします。](images/btth-bypass-arch.png)

この Windows 機能をサポートしませんので注意では、高度なオーディオ配布プロファイル (A2DP) を使用して、オーディオのストリーミングをバイパスします。 Windows 8 では、その他のオーディオ ドライバーを必要とせず、Bluetooth HCI の標準的なオーディオ機能を完全にサポートする個別の A2DP プロファイル ドライバーを提供します。

 

 




