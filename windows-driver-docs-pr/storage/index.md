---
title: 概要
description: 概要
ms.assetid: 0AEFA19D-C270-4777-8C08-E6056FBB6BC5
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# <a name="storage-driver-design-guide"></a>記憶装置ドライバー設計ガイド


記憶装置ドライバーには、[クラス](storage-class-drivers.md)、[ポート](storage-port-drivers.md)、[ミニポート](storage-miniport-drivers.md)、および[フィルター](storage-filter-drivers.md)の各ドライバーが含まれています。 通常、デバイス ベンダーでは、特定のアダプターまたはアダプターの種類に対応したミニポート ドライバーを実装します。 一般的ではありませんが、新しい記憶域クラスを定義できます。そのクラス用に新しいクラス ドライバーが開発されます。 Windows の記憶域クラスには、ディスク、CD-ROM、USB 記憶装置、および暗号化されたドライブの各クラスが含まれます。 通常、記憶装置ドライバーの開発は、[StorPort](storport-driver.md) ポート ドライバーと連携するミニポート ドライバーの作成に制限されます。

他の種類の記憶装置ドライバーは、マルチパス I/O 用のセキュリティで保護された[サイロ](storage-silo-drivers.md) ドライバーおよびデバイス固有モジュール (DSM) です。 記憶域の管理のために、ドライバーに対する制御インターフェイスとして [WMI](https://msdn.microsoft.com/library/windows/hardware/ff567016) プロバイダーが開発されます。

## <a name="span-idstoragedriverwdkresourcesspanspan-idstoragedriverwdkresourcesspanspan-idstoragedriverwdkresourcesspanoverview"></a><span id="Storage_Driver_WDK_Resources"></span><span id="storage_driver_wdk_resources"></span><span id="STORAGE_DRIVER_WDK_RESOURCES"></span>概要
この設計ガイドには次のセクションが含まれます。
* [Windows 記憶装置ドライバーの開発のロードマップ](roadmap-for-developing-storage-drivers.md)  
* [Storport ミニポート ドライバーの開発のロードマップ](roadmap-for-developing-storport-miniport-drivers.md)  
* [記憶装置ドライバー](storage-drivers.md)  
* [記憶域クラス ドライバー](storage-class-drivers.md)  
* [記憶域ポート ドライバー](storage-port-drivers.md)  
* [記憶域ミニポート ドライバー](storage-miniport-drivers.md)  
* [記憶域仮想ミニポート ドライバー](storage-virtual-miniport-drivers.md)  
* [記憶域フィルター ドライバー](storage-filter-drivers.md)  
* [クラッシュ ダンプ フィルター ドライバー](crash-dump-filter-drivers.md)  
* [記憶域サイロ ドライバー](storage-silo-drivers.md)  
* [CD-ROM ドライバー](cd-rom-drivers.md)  
* [テープ ドライバー](tape-drivers.md)  
* [チェンジャー ドライバー](changer-drivers.md)  
* [記憶域のシナリオ](storage-scenarios.md)  

## <a name="samples"></a>サンプル
サンプルの学習は、機能する記憶装置ドライバーの開発方法を確認するための実用的な方法です。 [記憶装置ドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples)は GitHub で入手できます。

## <a name="span-iddriververificationforstorportspanspan-iddriververificationforstorportspanspan-iddriververificationforstorportspandriver-verification-for-storport"></a><span id="Driver_Verification_for_StorPort"></span><span id="driver_verification_for_storport"></span><span id="DRIVER_VERIFICATION_FOR_STORPORT"></span>StorPort 用のドライバーの検証


ドライバーの開発およびテストの際にコード分析ツールを使用すると、記憶装置ドライバーにおけるパフォーマンスの問題や欠陥を把握するのに役立ちます。 [静的ドライバー検証ツール (SDV)](https://msdn.microsoft.com/library/windows/hardware/ff552808) を使用すると、記憶装置ドライバーのコードの欠陥を検出できます。 SDV には、StorPort のルーチンがミニポート ドライバーによって適切に使用されているかどうかを検証するためのコンプライアンス [ルール](https://msdn.microsoft.com/library/windows/hardware/hh454238)が付属しています。

記憶域ハードウェア認定のテストは、[Windows ハードウェア認定キット (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613) に含まれています。 記憶装置のテストは、HCK の [Devices.Storage](https://msdn.microsoft.com/library/windows/hardware/jj125097) カテゴリに含まれています。

 

 




