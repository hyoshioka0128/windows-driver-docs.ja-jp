---
title: カスタム オーディオ ドライバー
description: カスタム オーディオ ドライバー
ms.assetid: d5f19a72-0b43-4fe1-b0e1-0198344b4d19
keywords:
- WDM オーディオドライバー WDK、カスタム
- オーディオドライバー WDK、カスタム
- カスタムオーディオドライバー WDK
- ベンダー提供のドライバー WDK オーディオ
- PortCls WDK audio, カスタムオーディオドライバー
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: f8eceead615c1e7fdf9f1b0e9b95e285b03ec34b
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925603"
---
# <a name="custom-audio-drivers"></a>カスタム オーディオ ドライバー


UAA 互換でないオーディオデバイスでは、ベンダーが提供するカスタムドライバーが必要です。 また、UAA 互換オーディオアダプターには、UAA class ドライバーでサポートされていない独自の機能を組み込むことができます。これらの機能は、ベンダーがカスタムオーディオドライバーを提供している場合にのみ、アプリケーションにアクセスできます。 システム提供の UAA ドライバーを介してアクセスできるのは、標準の UAA 機能のみです。 UAA でサポートされる機能の詳細については、「[ユニバーサルオーディオアーキテクチャ](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn640534(v=vs.85))」ホワイトペーパーを参照してください。

カスタムオーディオドライバーの作成には、ハードウェアベンダーが、PortCls システムドライバー (Portcls) で使用するカスタムオーディオアダプタードライバーを開発する方法と、AVStream クラスシステムドライバー (Ks) で使用するカスタムミニドライバーを開発するオプションの2つがあります。

オーディオアダプター用のほとんどのカスタムドライバーは、オペレーティングシステムの一部として提供される PortCls を使用します。 PortCls システムドライバー (Portcls) には、カスタムオーディオドライバーを簡単に作成するタスクを行う組み込みのオーディオドライバーインフラストラクチャが含まれています。 PortCls はいくつかのポートドライバーを実装しており、それぞれが特定の種類の wave、MIDI、またはミキサーデバイスの汎用機能を管理するために特殊化されています。 オーディオアダプターのオーディオ機能を管理するための適切なポートドライバーのセットを選択すると、ベンダーは、選択されたポートドライバーと連携して動作するミニポートドライバーの補完的なセットを開発し、オーディオデバイスのハードウェアに依存する機能を制御します。

ベンダは、カスタム AVStream クラスミニドライバーを開発することによって、オーディオデバイスをサポートすることもできます。 ミニドライバーは AVStream クラスのシステムドライバーと共に動作し、オペレーティングシステムの一部として提供されます。 AVStream ドライバーの実装は PortCls を使用するよりも難しくなりますが、オーディオとビデオを統合するデバイスに適している場合もあります。 システムが提供する USBAudio または AVCAudio クラスのシステムドライバーの要件に準拠していない既存の USB または IEEE 1394 オーディオデバイスに対して AVStream ドライバーが必要になる場合もあります。

ベンダーが提供するカスタムドライバーを必要とするほとんどすべての PCI オーディオアダプターの場合、ベンダーは PortCls を選択する必要があります。

AVStream クラスシステムドライバー (Ks) では、PortCls に存在するオーディオ固有のサポート機能のほとんどが不足しています。

PortCls の詳細については、「 [Port クラスの概要](introduction-to-port-class.md)」を参照してください。 AVStream の詳細については、「 [Avstream の概要](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-overview)」を参照してください。

 

 




