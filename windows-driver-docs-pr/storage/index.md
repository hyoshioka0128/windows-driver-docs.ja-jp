---
title: 概要
description: 概要
ms.assetid: 0AEFA19D-C270-4777-8C08-E6056FBB6BC5
ms.date: 12/15/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: c1ab472469eb0ecc8eb66fb6fc42561f19ea4823
ms.sourcegitcommit: 988d100e4d3b218a59fdac034d39a1816d145c85
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "75606428"
---
# <a name="storage-driver-design-guide"></a>記憶装置ドライバー設計ガイド

記憶装置ドライバーには、[クラス](introduction-to-storage-class-drivers.md)、[ポート](storage-port-drivers.md)、[ミニポート](storage-miniport-drivers.md)、および[フィルター](storage-filter-drivers.md)の各ドライバーが含まれています。 通常、デバイス ベンダーでは、特定のアダプターまたはアダプターの種類に対応したミニポート ドライバーを実装します。 一般的ではありませんが、新しい記憶域クラスを定義できます。そのクラス用に新しいクラス ドライバーが開発されます。 Windows の記憶域クラスには、ディスク、CD-ROM、USB 記憶装置、および暗号化されたドライブの各クラスが含まれます。 通常、記憶装置ドライバーの開発は、[StorPort](storport-driver-overview.md) ポート ドライバーと連携するミニポート ドライバーの作成に制限されます。

他の種類の記憶装置ドライバーは、マルチパス I/O 用のセキュリティで保護された[サイロ](overview.md) ドライバーおよびデバイス固有モジュール (_DSM) です。 記憶域の管理のために、ドライバーに対する制御インターフェイスとして [WMI](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-wmi-classes) プロバイダーが開発されます。

この記憶装置ドライバーの設計ガイドには次のセクションが含まれます。

* [Windows 記憶装置ドライバーの開発のロードマップ](roadmap-for-developing-storage-drivers.md)
* [Storport ミニポート ドライバーの開発のロードマップ](roadmap-for-developing-storport-miniport-drivers.md)  
* [記憶装置ドライバー](storage-drivers.md)  
* [記憶域クラス ドライバー](introduction-to-storage-class-drivers.md)  
* [記憶域ポート ドライバー](storage-port-drivers.md)  
* [記憶域ミニポート ドライバー](storage-miniport-drivers.md)  
* [記憶域仮想ミニポート ドライバー](overview-of-storage-virtual-miniport-drivers.md)  
* [記憶域フィルター ドライバー](storage-filter-drivers.md)  
* [クラッシュ ダンプ フィルター ドライバー](crash-dump-filter-drivers.md)  
* [記憶域サイロ ドライバー](overview.md)  
* [CD-ROM ドライバー](cd-rom-drivers.md)  
* [テープ ドライバー](tape-drivers-overview.md)  
* [チェンジャー ドライバー](changer-drivers.md)  
* [記憶域のシナリオ](offloaded-data-transfer.md)  

## <a name="samples"></a>サンプル

サンプルの学習は、機能する記憶装置ドライバーの開発方法を確認するための実用的な方法です。 [記憶装置ドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples)は GitHub で入手できます。

## <a name="driver-verification-for-storport"></a>StorPort 用のドライバーの検証

ドライバーの開発およびテストの際にコード分析ツールを使用すると、記憶装置ドライバーにおけるパフォーマンスの問題や欠陥を把握するのに役立ちます。 [静的ドライバー検証ツール (SDV)](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier) を使用すると、記憶装置ドライバーのコードの欠陥を検出できます。 SDV には、StorPort のルーチンがミニポート ドライバーによって適切に使用されているかどうかを検証するためのコンプライアンス [ルール](https://docs.microsoft.com/windows-hardware/drivers/devtest/declaring-functions-by-using-function-role-types-for-storport-drivers)が付属しています。
