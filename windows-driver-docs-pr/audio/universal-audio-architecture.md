---
title: ユニバーサルのオーディオのアーキテクチャ
description: Microsoft Universal オーディオ アーキテクチャ (UAA) は、ドライバーのサポート用のオペレーティング システムに完全に依存するアーキテクチャに準拠しているオーディオ デバイスを使用できます。
ms.assetid: a42eff33-7952-4004-903d-9b202d1864b9
keywords:
- UAA WDK
- ユニバーサル オーディオ アーキテクチャ WDK
- オーディオ デバイス WDK UAA
- WDK の PCI オーディオ アダプター
- WDK の USB オーディオ
- IEEE 1394 WDK オーディオ
- Intel の高解像度オーディオ仕様
- WDM オーディオ ドライバー WDK、ユニバーサル オーディオのアーキテクチャ
- オーディオ ドライバー WDK、ユニバーサル オーディオのアーキテクチャ
- 1394 WDK オーディオ
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 18ac085175fe4928f6772e27b094f0f4e08927b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530010"
---
# <a name="universal-audio-architecture"></a>ユニバーサルのオーディオのアーキテクチャ


Microsoft Universal オーディオ アーキテクチャ (UAA) は、ドライバーのサポート用のオペレーティング システムに完全に依存するアーキテクチャに準拠しているオーディオ デバイスを使用できます。

UAA 互換にするには、PCI オーディオ アダプターは、Intel オーディオ コーデック ' 97 (AC'97) 仕様の後継である Intel 高オーディオの仕様に従う必要があります。 AC'97 とは異なり (Intel HD オーディオ) Intel 高品位オーディオ コーデックのデバイスと、シリアル インターフェイス リンク (コーデックをコント ローラーを接続するリンク) に加え、バス コント ローラーで標準化されます。 Intel HD オーディオ デバイスの UAA デザイン ガイドラインには、Intel の高解像度オーディオ仕様の一部ではないその他の要件が含まれています。 Windows Vista では、オーディオの UAA 準拠 PCI アダプターの完全なドライバーのサポートを提供します。

UAA 互換にするには、USB オーディオ デバイスが USB オーディオ仕様と USB オーディオ デバイスの UAA デザイン ガイドラインに従う必要があります。 USB オーディオ デバイスを使用することができますの使用、 [USBAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver) (Usbaudio.sys)、Windows の一部として指定されます。 定義上、Windows で USBAudio クラス システム ドライバーと互換性のある USB オーディオ デバイスが UAA に準拠していません。

UAA 互換にするには、IEEE 1394 AV/C のオーディオ デバイスは、関連の IEEE 1394 仕様と IEEE 1394 AV/C オーディオ デバイスの UAA デザイン ガイドラインに従う必要があります。 オーディオ デバイスを使用することができます、IEEE 1394 を使用して、 [AVCAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#avcaudio_class_system_driver) (Avcaudio.sys)、Windows の一部として指定されます。

Microsoft UAA イニシアチブの詳細については、次を参照してください。、[ユニバーサル オーディオ アーキテクチャ](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/UAA_Guidelines.doc)ホワイト ペーパー。 Intel HD オーディオの詳細については、次を参照してください。、 [Intel HD オーディオ](https://go.microsoft.com/fwlink/p/?linkid=42508)web サイト。 USB と IEEE 1394 のオーディオ デバイスに関連する仕様の一覧は、[USBAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)と[AVCAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#avcaudio_class_system_driver)を参照してください。

 

 




