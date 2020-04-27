---
title: 生体認証デバイス設計ガイド
description: 生体認証デバイス設計ガイド
ms.assetid: 78270890-4ea2-403e-bbd7-84a22581bbb7
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
author: EliotSeattle
ms.openlocfilehash: 32b3fefefc3c90ae1269fc0e20fb29f83db9c81d
ms.sourcegitcommit: 988d100e4d3b218a59fdac034d39a1816d145c85
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "68473445"
---
# <a name="biometric-devices-design-guide"></a>生体認証デバイス設計ガイド


## <span id="ddk_biometric_design_guide_kg"></span><span id="DDK_BIOMETRIC_DESIGN_GUIDE_KG"></span>


このセクションでは、Windows 生体認証ドライバー インターフェイス (WBDI) と連携するユーザー モード ドライバーを作成する方法について説明します。 WBDI は、Windows 生体認証フレームワーク (WBF) のドライバー インターフェイスです。 WBF は、Windows 7 以降のバージョンの Windows オペレーティング システムに付属しています。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


-   [生体認証ドライバーの概要](getting-started-with-biometric-drivers.md)
-   [生体認証ドライバーの開発のロードマップ](roadmap-for-developing-biometric-drivers.md)
-   [生体認証ドライバーのサンプル](sample-biometric-driver.md)
-   [生体認証 IOCTL 呼び出しシーケンスのサポート](supporting-biometric-ioctl-calling-sequence.md)
-   [WBDI ドライバーでの WinUSB の使用](using-winusb-in-a-wbdi-driver.md)
-   [生体認証ドライバーのインストール](installing-a-biometric-driver.md)
-   [WBDI ドライバーでのキューの管理](managing-queues-in-a-wbdi-driver.md)
-   [WBDI ドライバー用のデバイス インターフェイスの作成](creating-a-device-interface-for-a-wbdi-driver.md)
-   [WBDI ドライバーでのセキュリティで保護されたチャネルのサポート](supporting-secure-channels-in-wbdi-drivers.md)
-   [非 PnP デバイスまたは専用スタックでの WBDI の使用](using-wbdi-with-non-pnp-devices-or-proprietary-stacks.md)
-   [生体認証ドライバーのハードウェアに関する考慮事項](hardware-considerations-for-biometric-drivers.md)
-   [Windows Update における生体認証ドライバーのランク付け](ranking-a-biometric-driver-on-windows-update.md)
-   [生体認証ドライバーのテスト](testing-biometric-drivers.md)
-   [WBDI ドライバーへの署名](signing-wbdi-drivers.md)
-   [Windows Hello:フィンガープリント ドライバーを送信する手順](windows-hello-driver-signing.md)
-   [カスタム コントロールのコード](custom-control-codes.md)

 

 





