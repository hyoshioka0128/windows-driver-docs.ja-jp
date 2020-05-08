---
title: ユニバーサル オーディオ アーキテクチャ
description: Microsoft Universal Audio Architecture (UAA) を使用すると、アーキテクチャに準拠するオーディオデバイスは、ドライバーをサポートするためにオペレーティングシステム全体を利用できます。
ms.assetid: a42eff33-7952-4004-903d-9b202d1864b9
keywords:
- UAA WDK
- ユニバーサルオーディオアーキテクチャ (WDK)
- オーディオデバイス WDK UAA
- PCI オーディオアダプター WDK
- USB WDK オーディオ
- IEEE 1394 WDK オーディオ
- Intel High Definition Audio 仕様
- WDM オーディオドライバー WDK、ユニバーサルオーディオアーキテクチャ
- オーディオドライバー WDK、ユニバーサルオーディオアーキテクチャ
- 1394 WDK オーディオ
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3acb8aac43f916d8f691880b924cb1a9189c694d
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925511"
---
# <a name="universal-audio-architecture"></a>ユニバーサル オーディオ アーキテクチャ

Microsoft Universal Audio Architecture (UAA) を使用すると、アーキテクチャに準拠するオーディオデバイスは、ドライバーをサポートするためにオペレーティングシステム全体を利用できます。

UAA 互換にするには、PCI オーディオアダプターが Intel Audio Codec ' 97 (AC ' 97) 仕様の後継となる Intel High Definition Audio 仕様に準拠している必要があります。 AC ' 97 とは異なり、Intel High Definition Audio (Intel HD Audio) は、コーデックデバイスとシリアルインターフェイスリンク (コントローラーをコーデックに接続するリンク) に加えて、バスコントローラーを標準化します。 Intel HD Audio デバイスの UAA design ガイドラインには、Intel High Definition Audio 仕様に含まれていない追加の要件が含まれています。 Windows Vista では、UAA 準拠の PCI オーディオアダプターのドライバーを完全にサポートしています。

UAA 互換にするには、usb オーディオデバイスが usb オーディオ仕様と USB オーディオデバイスの UAA 設計ガイドラインの両方に準拠している必要があります。 USB オーディオデバイスは、Windows の一部として提供される[usbaudio クラスシステムドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver) (usbaudio .sys) を利用できます。 定義上、Windows の USBAudio クラスシステムドライバーと互換性がある USB オーディオデバイスは、UAA に準拠しています。

UAA 互換にするために、IEEE 1394 AV/C オーディオデバイスは、関連する IEEE 1394 仕様と、IEEE 1394 AV/C オーディオデバイス用の UAA 設計ガイドラインの両方に準拠している必要があります。 IEEE 1394 オーディオデバイスは[avcaudio クラスシステムドライバー](kernel-mode-wdm-audio-components.md#avcaudio_class_system_driver) (avcaudio .sys) を利用できます。このドライバーは、Windows の一部として提供されます。

Microsoft UAA イニシアチブの詳細については、「[ユニバーサルオーディオアーキテクチャ](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn640534(v=vs.85))」ホワイトペーパーを参照してください。

Intel HD audio の詳細については、 [INTEL Hd audio](https://www.intel.com/content/www/us/en/standards/intel-standards-and-initiatives.html) web サイトを参照してください。

USB および IEEE 1394 オーディオデバイスの関連仕様の一覧については、「 [Usbaudio クラスシステムドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver) 」および「 [Avcaudio クラスシステムドライバー](kernel-mode-wdm-audio-components.md#avcaudio_class_system_driver)」を参照してください。
