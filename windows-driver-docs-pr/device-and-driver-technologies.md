---
title: デバイス テクノロジとドライバー テクノロジ
description: このセクションには、サポートされている各 Windows ドライバー テクノロジに関する情報が含まれています。
ms.assetid: 1ef3e216-1322-42c3-b070-94cddfb2133c
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8be95023093318da17e9f84a643d181696b879c8
ms.sourcegitcommit: 132f0c2d827982b808053ecd3b4d137a2883cca1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "56519010"
---
# <a name="device-and-driver-technologies"></a>デバイス テクノロジとドライバー テクノロジ

このセクションには、サポートされている各 Windows ドライバー テクノロジに関する情報が含まれています。 ドライバー技術情報の大部分は、Windows 10 のすべてのエディションに関するものと同じです。 Windows の特定のエディション (Windows 10 Mobileなど) について特別な考慮事項がある場合は、それらの技術領域に明示的な説明を添えています。 ドライバーの開発に関する一般的な情報については、「[初めてのドライバーの作成](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/writing-your-first-driver)」をご覧ください。

## <a name="universal-windows-drivers"></a>ユニバーサル Windows ドライバー

ユニバーサル Windows ドライバー (Windows ドライバーで利用できるインターフェイスのサブセットを使用したドライバー) を作成すると、Windows 10 のすべてのエディションでそのドライバーを実行できます。 可能であれば、ユニバーサル Windows ドライバーを使用して、ドライバーを複数のデバイスで展開できるようにしてください。 Windows 10 のユニバーサル Windows ドライバーをビルド、インストール、展開、デバッグする方法については、「[Getting Started with Universal Windows drivers (ユニバーサル Windows ドライバーの概要)](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)」と「[テスト コンピューターへのドライバーの展開](https://docs.microsoft.com/windows-hardware/drivers/develop/deploying-a-driver-to-a-test-computer)」をご覧ください。

## <a name="device-drivers-and-windows10-for-desktop-computers"></a>デバイス ドライバーとデスクトップ コンピューター向け Windows 10

デスクトップ ドライバーの開発に使用されるツールについては、[ドライバー開発ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/
)と[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-verifying-drivers)に関する記事をご覧ください。 デスクトップの Windows 10 にドライバーを展開する方法について詳しくは、「[ドライバー パッケージの配布](https://docs.microsoft.com/windows-hardware/drivers/develop/distributing-a-driver-package-win8)」をご覧ください。 ドライバー構成のトラブルシューティングについて詳しくは、[ドライバー構成のトラブルシューティング](https://docs.microsoft.com/windows-hardware/drivers/develop/troubleshooting-configuration-of-driver-deployment--testing-and-debugging)に関する記事をご覧ください。

## <a name="device-drivers-and-windows10-mobile"></a>デバイス ドライバーと Windows 10 Mobile

Windows 10 Mobile は、モバイル デバイス特有のニーズに合わせて最適化されています。 デスクトップにドライバーをコピーしたり、デバイス マネージャーを使用してドライバーをインストールするのではなく、パッケージを使用してモバイル デバイスの OS にドライバーを追加できます。 パッケージの操作について詳しくは、「[モバイル パッケージの作成](https://docs.microsoft.com/previous-versions/windows/hardware/packaging/dn756642(v=vs.85))」をご覧ください。 なお、モバイル デバイス上のドライバーは、OS の整合性を維持するため、特定のプロセスを使用して署名する必要があります ([モバイル コード署名](https://docs.microsoft.com/previous-versions/windows/hardware/code-signing/dn756634(v=vs.85))に関する記事で説明しています)。 携帯電話などのモバイル デバイスにデバイス ドライバーを追加する方法のチュートリアルについては、「[テスト イメージへのドライバーの追加](https://docs.microsoft.com/previous-versions//mt131832(v=vs.85))」をご覧ください。

## <a name="in-this-section"></a>このセクションの内容

- [3D 印刷デバイス](3dprint/index.md)
- [Advanced Configuration and Power Interface (ACPI)](acpi/index.md)
- [オーディオ デバイス](audio/index.md)
- [バッテリー デバイス](battery/index.md)
- [生体認証デバイス](biometric/index.md)
- [Bluetooth デバイス](bluetooth/index.md)
- [ディスプレイ デバイス (アダプターとモニター)](display/index.md)
- [GNSS デバイス (位置情報)](gnss/index.md)
- [ハードウェア通知](gpiobtn/index.md)
- [ヒューマン入力デバイス (HID)](hid/index.md)
- [イメージング デバイス (スキャナー)](image/index.md)
- [インストール可能ファイル システム ドライバー](ifs/index.md)
- [カーネル モード ドライバー テクノロジ](kernel/index.md)
- [モバイル ブロードバンド](mobilebroadband/index.md)
- [多機能デバイス ドライバー](multifunction/index.md)
- [NetAdapterCx ドライバー](netcx/index.md)
- [ネットワーク ドライバー](network/index.md)
- [NFC デバイス ドライバー](nfc/index.md)
- [パラレル ポート ドライバー](parports/index.md)
- [パートナー アプリケーションの開発](partnerapps/index.md)
- [PCI ドライバー](pci/index.md)
- [PCMCIA ドライバー](pcmcia/index.md)
- [Point of Service (POS) ドライバー](pos/index.md)
- [電源管理テクノロジ](powermeter/index.md)
- [印刷デバイス](print/index.md)
- [SD カード バス ドライバー](sd/index.md)
- [センサー ドライバー](sensors/index.md)
- [シリアル ポート ドライバー](serports/index.md)
- [スマート カード リーダー デバイス ドライバー](smartcard/index.md)
- [SPB (Simple Peripheral Bus) ドライバー](spb/index.md)
- [記憶装置ドライバー](storage/index.md)
- [ストリーミング メディア デバイス ドライバー](stream/index.md)
- [Test Authoring and Execution Framework (TAEF)](taef/index.md)
- [ユニバーサル シリアル バス (USB)](usbcon/index.md)
- [Windows Device Testing Framework (WDTF)](wdtf/index.md)
- [Windows Hardware Error Architecture (WHEA)](whea/index.md)
