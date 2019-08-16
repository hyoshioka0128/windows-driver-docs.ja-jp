---
title: What's new in driver development
description: このセクションでは、Windows 10 でのドライバー開発に関する新機能について説明します。
ms.assetid: 5502AAF9-2400-4338-A646-C746B29F9A44
ms.date: 06/04/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 4c8f9325984b275a24087811991074b7212ea6a8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368030"
---
# <a name="top"></a>ドライバー開発に関する最新情報

このセクションでは、Windows 10 での Windows ドライバー開発に関する新機能と更新された機能について説明します。

以下は、Windows 10 でのドライバー開発に関する主な新機能の一覧です。

* [Windows 10 Version 1903 WDK による Visual Studio 2019 のサポート](#wdk-supports-visual-studio-2019)
* [Windows ハードウェア デベロッパー センター ダッシュボード](#windows-hardware-dev-center-dashboard)
* [オープンな発行](#open-publishing)
* [Windows 用デバッグ ツール](#debugging-tools-for-windows)
* [デバイスとドライバーのインストール](#device-and-driver-installation)
* [ドライバーの検証ツール](#driver-verifier)
* [Windows Driver Framework](#windows-driver-frameworks-wdf)
* [ユニバーサル Windows ドライバー](#universal-windows-drivers)
* [Windows 互換ハードウェア開発ボード](#windows-compatible-hardware-development-boards)
* [電源管理フレームワーク](#power-management-framework)
* [システム提供のドライバー インターフェイス](#system-supplied-driver-interfaces)
* [WPP ソフトウェア トレース](#wpp-software-tracing)

次の表は、Windows 10 で更新された機能をドライバー テクノロジとバージョン別に示しています。

| Driver (ドライバー)  |[1903](#whats-new-in-windows-10-version-1903-latest)| [1809](#whats-new-in-windows-10-version-1809) |   [1803](#whats-new-in-windows-10-version-1803)    | [1709](#whats-new-in-windows-10-version-1709) |  [1703](#whats-new-in-windows-10-version-1703)  | [1607](#whats-new-in-windows-10-version-1607) |  [1507](#whats-new-in-windows-10-version-1507)  |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| オーディオ  |  [![詳細](checkmark.png)](#audio-1903) |      [![詳細](checkmark.png)](#audio-1809)       |      [![詳細](checkmark.png)](#audio-1803)      |         [![詳細](checkmark.png)](#audio-1709)          |      [![詳細](checkmark.png)](#audio-1703)      |      [![詳細](checkmark.png)](#audio-1607)      |                   ![利用不可](minus.png)                   |
|               ACPI         |   ![利用不可](minus.png)    |             ![利用不可](minus.png)              |      [![詳細](checkmark.png)](#acpi-1803)       |          [![詳細](checkmark.png)](#acpi-1709)          |            ![利用不可](minus.png)             |          ![利用不可](minus.png)          |                   ![利用不可](minus.png)                   |
|             生体認証    |     ![利用不可](minus.png)   |             ![利用不可](minus.png)              |            ![利用不可](minus.png)             |       [![詳細](checkmark.png)](#biometric-1709)        |            ![利用不可](minus.png)             |          ![利用不可](minus.png)          |                   ![利用不可](minus.png)                   |
|             Bluetooth     |   ![利用不可](minus.png)     |     [![詳細](checkmark.png)](#bluetooth-1809)     |    [![詳細](checkmark.png)](#bluetooth-1803)    |                ![利用不可](minus.png)                |    [![詳細](checkmark.png)](#bluetooth-1703)    |          ![利用不可](minus.png)          |             [![詳細](checkmark.png)](#bluetooth-1507)             |
|          バスとポート          |   ![利用不可](minus.png)   |       ![利用不可](minus.png)              |            ![利用不可](minus.png)             |                ![利用不可](minus.png)                |            ![利用不可](minus.png)             |          ![利用不可](minus.png)          |          [![詳細](checkmark.png)](#buses-and-ports)          |
|              Camera       |    [![詳細](checkmark.png)](#camera-1903)    |             ![利用不可](minus.png)              |     [![詳細](checkmark.png)](#camera-1803)      |                ![利用不可](minus.png)                |     [![詳細](checkmark.png)](#camera-1703)      |   [![詳細](checkmark.png)](#camera-1607)   |            [![詳細](checkmark.png)](#camera-1507)            |
|             Cellular              |   ![利用不可](minus.png)   |       ![利用不可](minus.png)              |            ![利用不可](minus.png)             |                ![利用不可](minus.png)                |            ![利用不可](minus.png)             |          ![利用不可](minus.png)          |             [![詳細](checkmark.png)](#cellular)              |
|              ディスプレイ          |  [![詳細](checkmark.png)](#display-1903) |      [![詳細](checkmark.png)](#display-1809)      |     [![詳細](checkmark.png)](#display-1803)     |        [![詳細](checkmark.png)](#display-1709)         |            ![利用不可](minus.png)             |          ![利用不可](minus.png)          |              [![詳細](checkmark.png)](#display-1507)              |
|          ドライバーのセキュリティ      |  ![利用不可](minus.png)  |             ![利用不可](minus.png)              |    [![詳細](checkmark.png)](#security-1803)     |                ![利用不可](minus.png)                |            ![利用不可](minus.png)             |          ![利用不可](minus.png)          |              ![利用不可](minus.png)              |
|      ハードウェア通知    | ![利用不可](minus.png)  |             ![利用不可](minus.png)              |            ![利用不可](minus.png)             | [![詳細](checkmark.png)](#hardware-notifications-1709) |            ![利用不可](minus.png)             |          ![利用不可](minus.png)          |                   ![利用不可](minus.png)                   |
|   ヒューマン インターフェイス デバイス (HID)    |    ![利用不可](minus.png)    |     ![利用不可](minus.png)              |            ![利用不可](minus.png)             |                ![利用不可](minus.png)                |            ![利用不可](minus.png)             |          ![利用不可](minus.png)          |      [![詳細](checkmark.png)](#human-interface-device)       |
|              カーネル          |   ![利用不可](minus.png)  |      [![詳細](checkmark.png)](#kernel-1809)       |     [![詳細](checkmark.png)](#kernel-1803)      |         [![詳細](checkmark.png)](#kernel-1709)         |     [![詳細](checkmark.png)](#kernel-1703)      |          ![利用不可](minus.png)          |                   ![利用不可](minus.png)                   |
|             Location       |   ![利用不可](minus.png)    |             ![利用不可](minus.png)              |            ![利用不可](minus.png)             |                ![利用不可](minus.png)                |            ![利用不可](minus.png)             |  [![詳細](checkmark.png)](#location-1607)  |           [![詳細](checkmark.png)](#location-1507)           |
|         モバイル ブロードバンド    |    [![詳細](checkmark.png)](#mobilebroadband-1903)  |  [![詳細](checkmark.png)](#mobilebroadband-1809)  | [![詳細](checkmark.png)](#mobilebroadband-1803) |    [![詳細](checkmark.png)](#mobilebroadband-1709)     | [![詳細](checkmark.png)](#mobilebroadband-1703) |          ![利用不可](minus.png)          |                   ![利用不可](minus.png)                   |
|     近距離無線通信      |    ![利用不可](minus.png)     |    ![利用不可](minus.png)              |            ![利用不可](minus.png)             |                ![利用不可](minus.png)                |            ![利用不可](minus.png)             |          ![利用不可](minus.png)          |     [![詳細](checkmark.png)](#near-field-communication)      |
|            ネットワーク     |    [![詳細](checkmark.png)](#networking-1903)    |    [![詳細](checkmark.png)](#networking-1809)     |   [![詳細](checkmark.png)](#networking-1803)    |       [![詳細](checkmark.png)](#networking-1709)       |   [![詳細](checkmark.png)](#networking-1703)    |          ![利用不可](minus.png)          |          [![詳細](checkmark.png)](#networking-1507)          |
|                POS          |   ![利用不可](minus.png)   |             ![利用不可](minus.png)              |            ![利用不可](minus.png)             |                ![利用不可](minus.png)                |       [![詳細](checkmark.png)](#pos-1703)       |          ![利用不可](minus.png)          |                   ![利用不可](minus.png)                   |
|                PCI        |    ![利用不可](minus.png)    |             ![利用不可](minus.png)              |       [![詳細](checkmark.png)](#pci-1803)       |          [![詳細](checkmark.png)](#pci-1709)           |            ![利用不可](minus.png)             |          ![利用不可](minus.png)          |                   ![利用不可](minus.png)                   |
|               印刷     |      [![詳細](checkmark.png)](#print-1903)    |             ![利用不可](minus.png)              |            ![利用不可](minus.png)             |                ![利用不可](minus.png)                |            ![利用不可](minus.png)             |   [![詳細](checkmark.png)](#print-1607)    |            [![詳細](checkmark.png)](#print-1507)             |
|      パルス幅変調       |   ![利用不可](minus.png)  |        ![利用不可](minus.png)              |            ![利用不可](minus.png)             |          [![詳細](checkmark.png)](#pwm-1709)           |            ![利用不可](minus.png)             |          ![利用不可](minus.png)          |                   ![利用不可](minus.png)                   |
|              センサー        |  [![詳細](checkmark.png)](#sensors-1903)    |      [![詳細](checkmark.png)](#sensors-1809)      |     [![詳細](checkmark.png)](#sensors-1803)     |                ![利用不可](minus.png)                |            ![利用不可](minus.png)             |          ![利用不可](minus.png)          |                   ![利用不可](minus.png)                   |
|            スマート カード     |    ![利用不可](minus.png)    |             ![利用不可](minus.png)              |            ![利用不可](minus.png)             |                ![利用不可](minus.png)                |            ![利用不可](minus.png)             |          ![利用不可](minus.png)          |            [![詳細](checkmark.png)](#smart-card)             |
|              ストレージ         |    [![詳細](checkmark.png)](#storage-1903)  |             ![利用不可](minus.png)              |            ![利用不可](minus.png)             |        [![詳細](checkmark.png)](#storage-1709)         |            ![利用不可](minus.png)             |          ![利用不可](minus.png)          |              [![詳細](checkmark.png)](#storage-1507)              |
| システム提供のドライバー インターフェイス |   ![利用不可](minus.png)   |      ![利用不可](minus.png)              |            ![利用不可](minus.png)             |                ![利用不可](minus.png)                |            ![利用不可](minus.png)             |          ![利用不可](minus.png)          | [![詳細](checkmark.png)](#system-supplied-driver-interfaces) |
|                USB                |  ![利用不可](minus.png) |     [![詳細](checkmark.png)](#usb-1809)        |       [![詳細](checkmark.png)](#usb-1803)       |          [![詳細](checkmark.png)](#usb-1709)           |       [![詳細](checkmark.png)](#usb-1703)       |          ![利用不可](minus.png)          |                [![詳細](checkmark.png)](#usb-1507)                |
|               Wi-Fi           |  [![詳細](checkmark.png)](#wifi-1903)  |       [![詳細](checkmark.png)](#wifi-1809)        |      [![詳細](checkmark.png)](#wifi-1803)       |                ![利用不可](minus.png)                |            ![利用不可](minus.png)             |          ![利用不可](minus.png)          |                   ![利用不可](minus.png)                   |
|               WLAN         |    ![利用不可](minus.png)   |             ![利用不可](minus.png)              |            ![利用不可](minus.png)             |                ![利用不可](minus.png)                |            ![利用不可](minus.png)             |    [![詳細](checkmark.png)](#wlan-1607)    |             [![詳細](checkmark.png)](#wlan-1507)             |

## <a name="whats-new-in-driver-development-for-windows-10"></a>Windows 10 でのドライバー開発に関する最新情報

[ページのトップへ](#top)

このセクションでは、Windows 10 でのドライバー開発に関する主な新機能について説明します。

### <a name="wdk-supports-visual-studio-2019"></a>WDK による Visual Studio 2019 のサポート

Windows 10 Version 1903 用の Windows Driver Kit (WDK) は、以前の[発表](https://social.msdn.microsoft.com/Forums/en-US/b116571d-d5b2-4c1c-a43e-4b57171c8c41/windows-driver-kit-wdk-to-support-visual-studio-2019?forum=wdk)のとおり、Visual Studio 2019 をサポートするように更新されました。 このリリースの WDK は Visual Studio 2017 とは互換性がありませんが、開発者は以前のリリースの WDK を使用して Visual Studio 2017 を引き続き使用できます (リリース 1709 から 1809 は[こちら](https://docs.microsoft.com/en-us/windows-hardware/drivers/other-wdk-downloads)にあります)。 Visual Studio 2019 の新機能については、[こちら](https://docs.microsoft.com/en-us/visualstudio/releases/2019/release-notes#whats-new-in-visual-studio-2019)の情報を参照してください。

Visual Studio 2019 の Windows ドライバー開発者向けの注目すべき変更点を次に示します。

#### <a name="wdk-gui-driver-menu-moved"></a>WDK GUI ドライバー メニューの移動

Visual Studio 2019 では、WDK ドライバー メニューは次のように [拡張機能] メニューに表示されるように移動されました。

![Visual Studio 2019 メニューのスクリーンショット](images/vs-2019-driver-menu.png)

Visual Studio 2017 の WDK ドライバー メニューは次のように上部のメニュー オプションにあります。

![Visual Studio 2017 メニューのスクリーンショット](images/vs-2017-menu.png)

#### <a name="driver-templates-discoverability"></a>ドライバー テンプレートの見つけやすさ

Visual Studio 2019 では、WDK ドライバー テンプレートは [プロジェクトの種類] の [ドライバー] に表示されます。 [Driver Project Type]\(ドライバー プロジェクトの種類\) は、Visual Studio 2019 の最初の公式更新プログラム リリースに表示されます。 それまでは、ドライバー テンプレートを見つけるには、検索メニューで検索します。

![Visual Studio 2019 ドライバー テンプレートのスクリーンショット](images/vs-2019-driver-template.png)

WDK ドライバー テンプレートは、以前は Visual Studio 2017 の [新規プロジェクト] > [Visual C++] > [Windows ドライバー] に表示されていました。

![Visual Studio 2017 ドライバー テンプレートのスクリーンショット](images/vs-2017-driver-template.png)

### <a name="windows-hardware-dev-center-dashboard"></a>Windows ハードウェア デベロッパー センター ダッシュボード

Windows 10 Version 1809 では、開発者、IHV、OEM 用の[ハードウェア API](https://docs.microsoft.com/windows-hardware/drivers/dashboard/dashboard-api) でドライバー パッケージを追跡して Windows ハードウェア ダッシュボードに送信できるように、新機能の追加と機能強化が行われました。

出荷ラベル REST API (ドライバーを配布するためのメソッド) を使って、出荷ラベルの作成と管理を行います。

* [Manage Shipping Labels (出荷ラベルを管理する)](https://docs.microsoft.com/windows-hardware/drivers/dashboard/manage-shipping-labels)
* [Get shipping label data (出荷ラベルのデータを取得する)](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-shipping-labels)

ドライバーのエラーや OEM ハードウェアのエラーに関するレポート データにアクセスするには、非同期のカスタム レポート メソッドを使います。 ニーズに基づいてレポート テンプレートを定義し、スケジュール設定すれば、データが定期的に届くようになります。

* [Schedule custom reports for your driver failure details (ドライバー エラー詳細のカスタム レポートをスケジュールする)](https://docs.microsoft.com/windows-hardware/drivers/dashboard/schedule-custom-reports-for-driver-failure-details)

### <a name="open-publishing"></a>オープンな発行

Microsoft では、コミュニティ主導によるドキュメント制作を推進しています。 Windows ドライバーのドキュメントの多くのページで、変更を直接提案できます。 ページの右上隅で **[投稿]** ボタンを探します。 次のようになります。

![[投稿] ボタンのスクリーンショット](contribute-button.png)

**[投稿]** をクリックすると、[GitHub リポジトリ](https://github.com/MicrosoftDocs/windows-driver-docs)にある該当トピックのマークダウン ソース ファイルが表示されます。 **[編集]** をクリックし、その場で変更を提案できます。

詳しくは、リポジトリの [CONTRIBUTING.md](https://github.com/MicrosoftDocs/windows-driver-docs/blob/staging/CONTRIBUTING.md) をご覧ください。 ドキュメントの改善にご協力いただき、ありがとうございます。

### <a name="debugging-tools-for-windows"></a>Debugging Tools for Windows

このセクションでは、Windows 用デバッグ ツールの変更点について説明します。

#### <a name="debugging-in-windows-10-version-1903"></a>Windows 10 Version 1903 でのデバッグ

* Windows オペレーティング システム固有のエラーの種類を追跡しやすいように、新しい停止コードが追加されました。 さらに、いくつかの既存のバグ チェックに関するトピックが拡張および更新されました。 詳細については、「[バグ チェック コード リファレンス](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-code-reference2)」を参照してください。

* 使いやすさを向上させるために KDNET トピックを更新しました。たとえば、新しい「[KDNET ネットワーク カーネル デバッグの自動設定](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-automatically)」です

* IP V6 KDNET のサポートが更新されました。

* 新しい [JavaScript のデバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/javascript-debugger-scripting)のトピック

#### <a name="debugging-in-windows-10-version-1809"></a>Windows 10 Version 1809 でのデバッグ

* **新しいデバッガー データ モデル API** – デバッガーの自動化をサポートするオブジェクト指向の新しいデバッガー データ モデル インターフェイスが、dbgmodel.h ヘッダーを通じて利用可能になりました。 このデバッガー データ モデルは、新しいデバッガー拡張機能 (JavaScript、NatVis、C++ で記述されたものを含む) でデバッガーからの情報を利用したり、デバッガーや他の拡張機能からアクセスできる情報を生成したりするしくみの中心となる、拡張可能なオブジェクト モデルです。 データ モデル API に書き込まれるコンストラクトは、デバッガーの dx 式エバリュエーターのほか、JavaScript 拡張機能や C++ 拡張機能から参照できます。 ドキュメントは、「[Overview of the Debugger Data Model C++ Interface (デバッガー データ モデル C++ インターフェイスの概要)](debugger/data-model-cpp-overview.md)」および [dbgmodel.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgmodel/) ヘッダーのリファレンス トピックでご覧いただけます。

* **IPv6** - Microsoft では、KDNET に IPv6 のサポートを追加しています。 IPv6 で必要とされる大きいサイズのヘッダーに対応するため、パケットのペイロード サイズを縮小しました。 その結果、KDNET プロトコルの新しいバージョンを発表して、最新バージョンのデバッガーを実行するホスト PC から IPv4 のみをサポートするターゲット PC をデバッグできるようにしています。 IPv6 をサポートするバージョンの WinDbg プレビューは、[https://aka.ms/windbgpreview](https://aka.ms/windbgpreview) でダウンロードできます。 KDNET での IPv6 のサポートに関する最新情報を入手するには、Debugging Tools for Windows ブログをフォローしてください。また、「[Setting Up KDNET Network Kernel Debugging Manually (KDNET ネットワーク カーネルのデバッグを手作業でセットアップする)](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection)」で詳細をご確認ください。

#### <a name="debugging-in-windows-10-version-1803"></a>Windows 10 Version 1803 でのデバッグ

[WinDbg プレビューのタイム トラベル デバッグ (TTD) ハンズオン ラボ](https://docs.microsoft.com/windows-hardware/drivers/debugger/time-travel-debugging-walkthrough) - このラボでは、コードにエラーのある短いサンプル プログラムを使ってタイム トラベル デバッグ (TTD) を紹介します。 TTD を使って問題をデバッグし、その根本原因を特定します。

#### <a name="debugging-in-windows-10-version-1709"></a>Windows 10 Version 1709 でのデバッグ

Windows 10 Version 1709 では、デバッガーに関する次のコンテンツ セットが新たに追加されています。

* [Debugging Using WinDbg Preview (WinDbg プレビューを使用したデバッグ)](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugging-using-windbg-preview) - 次世代のデバッガーをプレビューします。
* [Time Travel Debugging - Overview (タイム トラベル デバッグ - 概要)](https://docs.microsoft.com/windows-hardware/drivers/debugger/time-travel-debugging-overview) - プロセスの実行を記録して再生します。

#### <a name="debugging-in-windows-10-version-1703"></a>Windows 10 Version 1703 でのデバッグ

次の表は、Windows 10 Version 1703 でのデバッガーの変更点を示しています。

| 新しいトピック | 更新されたトピック |
| --- | --- |
| [JavaScript デバッガー スクリプト](https://docs.microsoft.com/windows-hardware/drivers/debugger/javascript-debugger-scripting) | [dtx (Display Type - Extended Debugger Object Model Information)](https://docs.microsoft.com/windows-hardware/drivers/debugger/dtx--display-type---extended-debugger-object-model-information-) コマンド |
| [バグ チェック コード リファレンス](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-code-reference2)に未掲載の 40 の停止コード | 「[Configuring tools.ini (tools.ini の構成)](https://docs.microsoft.com/windows-hardware/drivers/debugger/configuring-tools-ini)」トピックの更新 (コマンド ライン デバッガー用の tools.ini の追加オプション) |
| [!ioctldecode コマンド](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ioctldecode) | [dx (Display Debugger Object Model Extension)](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-) コマンドの新しいコマンド機能 |

#### <a name="debugging-in-windows-10-version-1607"></a>Windows 10 Version 1607 でのデバッグ

Windows 10 Version 1607 では、デバッガーに関して、[WinDbg を使用した UWP アプリのデバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugging-a-uwp-app-using-windbg)に関する新しいトピックの追加や、[バグ チェック コード リファレンス](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-code-reference2)で最も閲覧数の多い 30 件の開発者向けバグ チェック トピックの更新などが行われました。

#### <a name="debugging-in-windows-10-version-1507"></a>Windows 10 Version 1507 でのデバッグ

Windows 10 Version 1507 では、Windows デバッガーに次のコマンドが新たに追加されました。

* [**dx (Display NatVis Expression)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-) - NatVis 拡張モデルを使ってオブジェクトの情報を表示する新しいデバッガー コマンド。
* [ **.settings**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-settings--set-debug-settings-) - Debugger.Settings 名前空間の設定を設定、変更、表示、読み込み、保存する新しいコマンド。

### <a name="device-and-driver-installation"></a>デバイスとドライバーのインストール

Windows 10 Version 1809 では、次のコンテンツが追加されました。

* [INF AddEventProvider ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addeventprovider-directive)
* [INF DDInstall.Events セクション](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-events-section)

次のものが更新されました。

* [起動時マルウェア対策の要件](https://docs.microsoft.com/windows-hardware/drivers/install/elam-driver-requirements)
* [カーネル モードのコード署名の要件](https://docs.microsoft.com/windows-hardware/drivers/install/kernel-mode-code-signing-requirements--windows-vista-and-later-)

### <a name="driver-verifier"></a>ドライバーの検証ツール

ドライバーの検証ツールには、次のテクノロジ向けの新しいドライバー検証規則が含まれています。

* 新しい[オーディオ ドライバーの規則](https://docs.microsoft.com/windows-hardware/drivers/devtest/rules-for-audio-drivers)
* 新しい [AVStream ドライバーの規則](https://docs.microsoft.com/windows-hardware/drivers/devtest/rules-for-avstream-drivers)
* 4 つの新しい [KMDF ドライバーの規則](https://docs.microsoft.com/windows-hardware/drivers/devtest/sdv-rules-for-kmdf-drivers)
* 3 つの新しい [NDIS ドライバーの規則](https://docs.microsoft.com/windows-hardware/drivers/devtest/sdv-rules-for-ndis-drivers)
* 新しい [Nullcheck 規則](https://docs.microsoft.com/windows-hardware/drivers/devtest/nullcheck) ("*Version 1703 で追加*")

### <a name="windows-driver-frameworks-wdf"></a>Windows Driver Framework (WDF)

#### <a name="wdf-in-windows-10-version-1903"></a>Windows 10 Version 1903 の WDF

Windows 10 Version 1903 の Windows Driver Framework (WDF) には、Kernel-Mode Driver Framework (KMDF) バージョン 1.29 と User-Mode Driver Framework (UMDF) バージョン 2.29 が含まれます。

これらのフレームワーク バージョンに含まれる機能については、「[What's New for WDF Drivers in Windows 10 (Windows 10 の WDF ドライバーの新機能)](https://docs.microsoft.com/windows-hardware/drivers/wdf/)」をご覧ください。
WDF の以前のバージョンで追加された機能については、「[KMDF Version History (KMDF のバージョン履歴)](https://docs.microsoft.com/windows-hardware/drivers/wdf/kmdf-version-history)」と「[UMDF Version History (UMDF のバージョン履歴)](https://docs.microsoft.com/windows-hardware/drivers/wdf/umdf-version-history)」をご覧ください。

### <a name="universal-windows-drivers"></a>ユニバーサル Windows ドライバー

このセクションでは、Windows 10 のユニバーサル Windows ドライバーの新機能と更新された機能について説明します。

[ページのトップへ](#top)

#### <a name="universal-drivers-in-windows-10-version-1809"></a>Windows 10 Version 1809 のユニバーサル ドライバー

Windows 10 Version 1809 以降、Windows で柔軟なリンクがサポートされるようになりました。これにより、単一のバイナリを使って OneCore およびデスクトップの SKU をターゲットとすることができます。
柔軟なリンクを有効にするには、次の新しい SDK API を使用します。

* [IsApiSetImplemented](https://docs.microsoft.com/windows/desktop/api/apiquery2/nf-apiquery2-isapisetimplemented)

この既存のトピックが補強され、柔軟なリンクを使って [DCHU ドライバー設計の原則](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers#design-principles)に関する U の要件に準拠する方法についての説明が加わりました。

* [OneCore をターゲットとしたビルド](https://docs.microsoft.com/windows-hardware/drivers/develop/building-for-onecore)

#### <a name="universal-drivers-in-windows-10-version-1803"></a>Windows 10 Version 1803 のユニバーサル ドライバー

「[Getting started with universal drivers (ユニバーサル ドライバーの概要)](develop/getting-started-with-universal-drivers.md)」で、ユニバーサル ドライバーに関する最新の推奨事項をご確認ください。

#### <a name="universal-drivers-in-windows-10-version-1709"></a>Windows 10 Version 1709 のユニバーサル ドライバー

Windows 10 Version 1709 では、ユニバーサル ドライバーに次の新機能が追加されました。

* [Windows Update を使ったデバイス ファームウェアの更新](https://docs.microsoft.com/windows-hardware/drivers/install/updating-device-firmware-using-windows-update) - Windows Update (WU) サービスを使って、リムーバブルまたはシャーシ内のデバイスのファームウェアを更新する方法について説明しています。
* [Reg2inf](https://docs.microsoft.com/windows-hardware/drivers/devtest/reg2inf) - ドライバー パッケージ INF レジストリ変換ツール (reg2inf.exe) は、レジストリ キーとその値または DLL RegisterServer ルーチンを実装する COM .dll を、INF AddReg ディレクティブのセットに変換します。 これらのディレクティブは、ドライバー パッケージ INF ファイルに含まれます。

Windows 10 Version 1709 では、ユニバーサル ドライバーに関する次の更新が行われました。

* [ユニバーサル ドライバー シナリオ](https://docs.microsoft.com/windows-hardware/drivers/develop/universal-driver-scenarios)への新しい COM コンポーネント サンプルの追加
* [INF AddComponent ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addcomponent-directive)
* [拡張 INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)
* [コンポーネント INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-component-inf-file)

#### <a name="universal-drivers-in-windows-10"></a>Windows 10 のユニバーサル ドライバー

Windows 10 以降では、Windows 10 デスクトップ エディション (Home、Pro、Enterprise、Education)、Windows 10 Mobile、Windows 10 IoT Core (IoT Core) などの OneCoreUAP ベースの Windows エディションで動作する単一のドライバーを作成できます。 このようなドライバーは、ユニバーサル Windows ドライバーと呼ばれています。 ユニバーサル Windows ドライバーは、Windows ドライバーで利用可能なインターフェイスのサブセットを呼び出します。 Windows 10 のユニバーサル Windows ドライバーをビルド、インストール、展開、デバッグする方法については、「[Getting Started with Universal Windows drivers (ユニバーサル Windows ドライバーの概要)](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)」をご覧ください。

Microsoft Visual Studio 2015 を使ってユニバーサル Windows ドライバーをビルドするとき、ドライバーが呼び出す API がユニバーサル Windows ドライバーに対して有効かどうかが Visual Studio によって自動的にチェックされます。 ApiValidator.exe をスタンドアロン ツールとして使い、このタスクを実行することもできます。 ApiValidator.exe ツールは、Windows Driver Kit (WDK) for Windows 10 の一部です。 詳しくは、「[Validating Universal Windows drivers (ユニバーサル Windows ドライバーの検証)](https://docs.microsoft.com/windows-hardware/drivers/develop/validating-universal-drivers)」をご覧ください。

ユニバーサル Windows ドライバーには、"*ユニバーサル INF*" と呼ばれる特殊な INF ファイルも必要です。 ユニバーサル INF では、従来の INF ファイルで利用可能なディレクティブやセクションのサブセットを使用できます。 詳しくは、「[Using a Universal INF File (ユニバーサル INF ファイルの使用)](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-universal-inf-file)」をご覧ください。 該当するセクションとディレクティブを確認するには、「[INF File Sections and Directives (INF ファイルのセクションとディレクティブ)](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)」をご覧ください。

準備ができたら、[InfVerif](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif) ツールを使ってドライバーの INF ファイルをテストします。 このツールでは、INF 構文の問題だけでなく、その INF ファイルがユニバーサル Windows ドライバーに対応しているかどうかについても報告されます。

また、ユニバーサル Windows ドライバーから呼び出すことのできる API に関する情報も確認できます。 この情報は、ドライバーのリファレンス ページの下部にある要件ブロック内にあります。

たとえば、DDI が**ユニバーサル**であれば、次のように表示されます。

![要件ブロックでターゲット プラットフォームがユニバーサルに設定されている](targetplatform.png)

詳しくは、「[Target platform on driver reference pages (ドライバー リファレンス ページでのターゲット プラットフォーム)](https://docs.microsoft.com/windows-hardware/drivers/develop/windows-10-editions-for-universal-drivers)」をご覧ください。

### <a name="windows-compatible-hardware-development-boards"></a>Windows 互換ハードウェア開発ボード

Raspberry Pi 2 などの手頃な価格のボードで Windows がサポートされるようになりました。 早期導入者コミュニティに参加して、これらのボードで Windows を使ってみてください。 詳しくは、「[Windows 互換ハードウェア開発ボード](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/windows-compatible-hardware-development-boards)」をご覧ください。

### <a name="power-management-framework"></a>電源管理フレームワーク

電源管理フレームワーク (PoFx) により、ドライバーは、デバイス内の個々のコンポーネントに対して個別に調整可能なパフォーマンス状態のセットをいくつでも定義することができます。 このドライバーは、パフォーマンスの状態を使ってコンポーネントのワークロードを調整し、現在のニーズに最適なパフォーマンスを提供します。 詳しくは、「[Component-Level Performance State Management (コンポーネント レベルのパフォーマンス状態の管理)](https://docs.microsoft.com/windows-hardware/drivers/kernel/component-level-performance-management)」をご覧ください。

Windows 10 Version 1903 には [Directed Power Management Framework (DFx)](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-the-directed-power-management-framework) のサポートが含まれています。  以下の関連する参照ドキュメントがあります。

* [PO_FX_DEVICE_V3](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-po_fx_device_v3)
* [PO_FX_DIRECTED_POWER_DOWN_CALLBACK コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_down_callback)
* [PO_FX_DIRECTED_POWER_UP_CALLBACK コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_directed_power_up_callback)
* [PoFxCompleteDirectedPowerDown](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxcompletedirectedpowerdown) 関数

DFx のテストについては、以下のページを参照してください。

* [有向 FX 単一デバイス テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/34cfdfa6-7826-443c-9717-bc28c3166092)
* [有向 FX システムの検証テスト](https://docs.microsoft.com/windows-hardware/test/hlk/testref/def16163-9118-4d4a-b559-37873befa12e)
* [PwrTest DirectedFx シナリオ](devtest/pwrtest-directedfx-scenario.md)

### <a name="wpp-software-tracing"></a>WPP ソフトウェア トレース

[WPP ソフトウェア トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)に新機能"*インフライト トレース レコーダー*" が導入されました。 ドライバーで WPP トレースと WPP レコーダーを有効にすると、トレース ログが自動的にオンになるため、トレース セッションを開始または停止せずに簡単にメッセージを表示できます。 ログをよりきめ細かく制御できるように、WPP レコーダーでは KMDF ドライバーによるカスタム バッファーの作成と管理が許可されています。

* [ログ トレース用の WPP レコーダー](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-wpp-recorder)
* [WppRecorderLogGetDefault](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-imp_wpprecorderloggetdefault)
* [WppRecorderLogCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderlogcreate) (KMDF のみ)
* [WppRecorderDumpLiveDriverData](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderdumplivedriverdata)

## <a name="whats-new-in-windows-10-version-1903-latest"></a>Windows 10 Version 1903 (最新版) の最新情報

このセクションでは、Windows 10 Version 1903 (Windows 10 April 2019 Update) でのドライバー開発に関する新機能と更新された機能について説明します。

[ページのトップへ](#top)

### <a name="audio-1903"></a>オーディオ

Windows 10 Version 1903 の新機能と更新されたオーディオ機能の一覧を次に示します。

* 新しい [eventdetectoroemadapter.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/eventdetectoroemadapter/) ヘッダーの音声ライセンス認証に使用されるオーディオ OEM アダプターに関する新しい参照トピック。
* 新しい Far フィールド オーディオ情報: 
    * [PKEY_Devices_AudioDevice_Microphone_IsFarField](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-devices-audiodevice-microphone-isfarfield)
    * [KSPROPSETID_InterleavedAudio](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-interleavedaudio)
    * [KSPROPERTY_INTERLEAVEDAUDIO_FORMATINFORMATION](https://review.docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-interleavedaudio-formatinformation)
    
* [USB オーディオ 2.0 ドライバー](https://docs.microsoft.com/windows-hardware/drivers/audio/usb-2-0-audio-drivers)の新しいジャックの説明情報。

### <a name="camera-1903"></a>カメラ

Windows 10 Version 1903 で追加された新しいカメラ ドライバーのドキュメントと機能を次に示します。

* 新しい [IR Torch](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-irtorchmode) では、IR カメラの赤外線トーチの電力レベルとデューティ サイクルを設定するプロパティ コントロールを拡張しました。
* 新しい [KSCATEGORY_NETWORK_CAMERA](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-network-camera) デバイス。
* 次のコントロール セレクター用の新規および更新された [USB ビデオ クラス (UVC) 1.5 拡張機能](https://docs.microsoft.com/windows-hardware/drivers/stream/uvc-extensions-1-5)のドキュメント。
  * MSXU_CONTROL_FACE_AUTHENTICATION
  * MSXU_CONTROL_METADATA
  * MSUX_CONTROL_IR_TORCH

### <a name="display-1903"></a>ディスプレイ

Windows 10 Version 1903 では、ディスプレイ ドライバー開発に関する次の更新が行われました。

* **スーパーウェット インク** フロントバッファー レンダリングが可能になる新しい DDI が追加されました。 [D3DWDDM2_6DDI_SCANOUT_FLAGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ne-d3d10umddi-d3dwddm2_6ddi_scanout_flags) と [PFND3DWDDM2_6DDI_PREPARE_SCANOUT_TRANSFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3dwddm2_6ddi_prepare_scanout_transformation) を参照してください。

* **可変レート シェーディング** レンダリングされた画像全体にさまざまなレートのレンダリング パフォーマンス/電力の割り当てが可能になります。 [PFND3D12DDI_RS_SET_SHADING_RATE_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_rs_set_shading_rate_0062) と [D3D12DDI_SHADING_RATE_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/ne-d3d12umddi-d3d12ddi_shading_rate_0062) を参照してください。

* **診断情報の収集** OS で、レンダリング機能と表示機能の両方で構成されるグラフィックス アダプター用ドライバーからプライベート データを収集できるようになります。 [DXGKDDI_COLLECTDIAGNOSTICINFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_collectdiagnosticinfo) を参照してください。

* **バックグラウンド処理** ユーザー モード ドライバーで、目的のスレッド動作と、それを制御または監視するランタイムを表現できるようになります。 ユーザー モード ドライバーでは、バックグラウンド スレッドをスピンアップし、可能な限り低い優先度を割り当てます。また、これらのスレッドによってクリティカル パス スレッドが中断せず、全般的には成功するように NT スケジューラを利用します。 [PFND3D12DDI_QUEUEPROCESSINGWORK_CB_0062](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_queueprocessingwork_cb_0062) を参照してください。

* **ドライバーのホット更新** OS コンポーネントを更新する必要がある場合に、サーバーのダウンタイムを可能な限り短縮します。 [DXGKDDI_SAVEMEMORYFORHOTUPDATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_savememoryforhotupdate) と [DXGKDDI_RESTOREMEMORYFORHOTUPDATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_restorememoryforhotupdate) を参照してください。

### <a name="networking-1903"></a>ネットワーク

#### <a name="netadaptercx"></a>NetAdapterCx

NetAdapter WDF クラス拡張機能 (NetAdapterCx) では、ネット リング バッファーはネット リングに置き換えられました。これには、ネット リング反復子を使用してネットワーク データを送受信するための新しいインターフェイスがあります。 新しいトピックの一覧を次に示します。

* [ネット リングとネット リングの反復子](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-rings-and-net-ring-iterators)
* [ネット リングを使用したネットワーク データの送信](https://docs.microsoft.com/windows-hardware/drivers/netcx/sending-network-data-with-net-rings) (およびデータの送信方法を示す新しいアニメーション)
* [ネット リングを使用したネットワーク データの受信](https://docs.microsoft.com/windows-hardware/drivers/netcx/receiving-network-data-with-net-rings) (およびデータの受信方法を示す新しいアニメーション)
* [ネット リングを使用したネットワーク データの取り消し](https://docs.microsoft.com/windows-hardware/drivers/netcx/canceling-network-data-with-net-rings)

この機能をサポートする新しいヘッダーを次に示します。

* [Ring.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ring/index)
* [Ringcollection.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ringcollection/index)
* [Netringiterator.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/index)

NetAdapterCx コンテンツの更新の一覧を次に示します。

* 既定のアダプター オブジェクトは、1 つのアダプター オブジェクトの種類のために削除されました。 次のトピックが適宜更新されました。

  * [Summary of NetAdapterCx objects (NetAdapterCx オブジェクトの概要)](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-netadaptercx-objects)
  * [Device and adapter initialization (デバイスとアダプターの初期化)](https://docs.microsoft.com/windows-hardware/drivers/netcx/device-and-adapter-initialization)

* ハードウェア オフロードとパケット拡張 DDI は新しいヘッダーに再編成されました。

  * [Checksum.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/checksum/index)
  * [Checksumtypes.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/checksumtypes/index)
  * [Extension.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/extension/index)
  * [Lso.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lso/index)
  * [Lsotypes.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lsotypes/index)
  * [Rsc.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rsc/index)
  * [Rsctypes.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rsctypes/index)

* 基本的なネットワーク データ構造、パケット、およびフラグメントは更新され、新しいヘッダーに組み込まれました。

  * [Packet.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/packet/index)
  * [Fragment.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fragment/index)

* コールバックのサンプルとパケット キューの主な操作を含めるために、[キューの送信と受信](https://docs.microsoft.com/windows-hardware/drivers/netcx/transmit-and-receive-queues)に関するトピックを見直しました。

#### <a name="mobile-operator-scenarios"></a>通信事業者のシナリオ

通信事業者がモバイル プラン アプリを介して Windows 10 デバイス上で顧客にプランを直接販売するための新しいモバイル プラン コンテンツ。

* [モバイル プラン](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/mobile-plans)

### <a name="mobilebroadband-1903"></a>モバイル ブロードバンド

Windows 10 Version 1903 のモバイル ブロードバンドに次の機能が追加されました。

* 新しい [SIM カード (UICC) ファイル/アプリケーション システム アクセス](https://docs.microsoft.com/windows-hardware/drivers/network/mb-uicc-application-and-file-system-access)機能
* 新しい[移動体通信時間情報 (NITZ)](https://docs.microsoft.com/windows-hardware/drivers/network/mb-nitz-support) 機能。
* 新しい [DSS によるモデムのログ記録](https://docs.microsoft.com/windows-hardware/drivers/network/mb-modem-logging-with-dss)機能。
* 新しい [5G データ クラスのサポート](https://docs.microsoft.com/windows-hardware/drivers/network/mb-5g-data-class-support)機能。

### <a name="print-1903"></a>印刷

Windows 10 Version 1903 で追加された新しい印刷ドライバーのドキュメントと機能を次に示します。

* 新しい USB 印刷 IOCTL:

  * [IOCTL_USBPRINT_GET_INTERFACE_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_get_interface_type)
  * [IOCTL_USBPRINT_GET_PROTOCOL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_get_protocol)
  * [IOCTL_USBPRINT_SET_PROTOCOL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_set_protocol)

* 新しい **fpRegeneratePrintDeviceCapabilities** [PRINTPROVIDER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/ns-winsplp-_printprovidor) 構造体メンバーと更新されたドキュメント。

### <a name="sensors-1903"></a>センサー

Windows 10 Version 1903 のセンサー ドライバー開発の新機能には、画面の明るさをテストして調整するための [MALT (Microsoft Ambient Light Tool) ツール](https://docs.microsoft.com/windows-hardware/drivers/sensors/testing-malt-building-a-light-testing-tool)が含まれています。

Ambient Color OEM ホワイトペーパーも更新されました。

### <a name="storage-1903"></a>ストレージ

Windows 10 Version 1903 には次のストレージ機能が追加されました。

* ETW イベントでデバイスの障害とハードウェア プロトコル エラーをログに記録し、プラットフォーム D3 の望ましい動作を照会する新しい Storport API
* ストレージ デバイスまたはアダプターのプロパティを設定するための新しい API
* ファイル システムでは、作成の完了時に拡張属性 (EA) 情報の取得をサポートする新しい DDI が追加され、ミニフィルターで ECP ペイロードを変更して、より高いフィルターを変更できるようになりました

### <a name="windows-hardware-error-architecture-whea"></a>Windows Hardware Error Architecture (WHEA)

Windows 10 Version 1903 では、WHEA へのインターフェイスが簡単になりました。  詳細については、次のページを参照してください。

* [**WheaAddErrorSourceDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-wheaadderrorsourcedevicedriver)
* [**WheaReportHwErrorDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-wheareporthwerrordevicedriver)
* [**WheaRemoveErrorSourceDeviceDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-whearemoveerrorsourcedevicedriver)
* [**WHEA_ERROR_SOURCE_CONFIGURATION_DEVICE_DRIVER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-whea_error_source_configuration_device_driver)
* [*WHEA_ERROR_SOURCE_READY_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-_whea_error_source_ready_device_driver)
* [*WHEA_ERROR_SOURCE_UNINITIALIZE_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-_whea_error_source_uninitialize_device_driver)
* [*WHEA_ERROR_SOURCE_INITIALIZE_DEVICE_DRIVER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-_whea_error_source_initialize_device_driver)

### <a name="wifi-1903"></a>Wi-Fi

新しい Wi-Fi ドライバーの開発ドキュメントと機能を次に示します。

* 新しい Fine Timing Measurement (FTM) 機能
* 新しい [WPA3-SAE 認証](https://docs.microsoft.com/windows-hardware/drivers/network/wpa3-sae-authentication)機能
* エンタープライズ シナリオでローミング パフォーマンスを向上させるための新しい Multiband Operation (MBO) のサポート
* 新しいビーコン レポート オフロードのサポート
* これらの新機能に関する OID コマンド、NDIS の状態表示、および TLV については、「[WDI ドキュメントの変更履歴](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-doc-change-history)」を参照してください。

次のトピックは、Windows 10 Version 1903 に合わせて更新されました。

* [WDI_AUTH_ALGORITHM](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_auth_algorithm) - WPA3-SAE 認証のサポートが追加されました
* [OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-send-request-action-frame) と [OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-send-response-action-frame) - 送信ポイント ツー ポイント (P2P) アクション フレームの新しい検証が追加されました

## <a name="whats-new-in-windows-10-version-1809"></a>Windows 10 Version 1809 の最新情報

このセクションでは、Windows 10 Version 1809 (Windows 10 October 2018 Update) でのドライバー開発に関する新機能と更新された機能について説明します。

[ページのトップへ](#top)

### <a name="audio-1809"></a>オーディオ

新しい [sidebandaudio](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sidebandaudio/) ヘッダーと [usbsidebandaudio](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbsidebandaudio/) ヘッダーに関するドキュメントが公開されました。

### <a name="bluetooth-1809"></a>Bluetooth

* HCI_VS_MSFT_Read_Supported_Features が更新され、セキュリティで保護されたシンプルなペアリング プロセスのための新しいフラグが追加されました。 「[Microsoft-defined Bluetooth HCI commands and events (Microsoft が定義した Bluetooth HCI のコマンドとイベント)](https://docs.microsoft.com/windows-hardware/drivers/bluetooth/microsoft-defined-bluetooth-hci-commands-and-events#hcivsmsftreadsupportedfeatures)」をご覧ください。

* Windows 10 Version 1809 の新しい QDID はこちら([108589](https://launchstudio.bluetooth.com/ListingDetails/55701)) で確認できます。 すべてのリリースの全 QD ID の一覧については、「[Bluetooth](https://docs.microsoft.com/windows-hardware/design/component-guidelines/bluetooth)」をご覧ください。

### <a name="display-1809"></a>ディスプレイ

Windows 10 Version 1809 では、ディスプレイ ドライバー開発に関する次の更新が行われました。

* **レイトレーシング** ハードウェア アクセラレータによるレイトレーシングをサポートするために、Direct3D API と平行して新しい Direct3D DDI が作成されました。 次のような DDI があります。[PFND3D12DDI_BUILD_RAYTRACING_ACCELERATION_STRUCTURE_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_build_raytracing_acceleration_structure_0054)、[PFND3D12DDI_COPY_RAYTRACING_ACCELERATION_STRUCTURE_0054](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/nc-d3d12umddi-pfnd3d12ddi_copy_raytracing_acceleration_structure_0054)。 レイトレーシングについて詳しくは、[Microsoft DirectX レイトレーシングに関する発表](https://devblogs.microsoft.com/directx/announcing-microsoft-directx-raytracing/)をご覧ください。

* **ユニバーサル ドライバーの要件** WDDM 2.5 ドライバーでは、DirectX11 UMD、DirectX12 UMD、KMD、およびこれらのコンポーネントによって読み込まれるその他すべての DLL を、ユニバーサル API に確実に準拠させる必要があります。

* **SRV のみタイル リソース階層 3** Windows 10 Version 1809 では、GPU によって、タイル リソース階層 3 の機能が直交ではない方法でサポートされます。 Direct3D12 では、順序指定されていないアクセスやレンダー ターゲットの操作を必要とせずに、スパース ボリューム テクスチャがサポートされるようになりました。 SRV のみのタイル リソース階層 3 は、階層 2 と階層 3 の間に収まる概念上の階層です。 直交タイル リソース階層 3 のサポートが現在省略可能であるのと同様に、ハードウェアのサポートは省略可能です。 ただし、SRV のみのタイル リソース階層 3 はスーパーセットの階層なので、これをサポートするにはタイル リソース階層 2 のサポートが必要です。

   直交タイル リソース階層 3 のサポートが既にドライバーでアドバタイズされている場合、最新の "オプション キャプ" の DDI 構造バージョンをサポートするためにドライバーを更新する必要はありません。 直交タイル リソース階層 3 を既にサポートしているすべてのハードウェアについて、ランタイムで SRV のみのタイル リソース階層 3 のサポートがアプリケーションにアドバタイズされます。

* **レンダリング パス** レンダリング パス機能が追加され、次のことが可能になりました。

  * 新しい API が既存のドライバーで実行できるようにする。
  * ユーザー モードのドライバーが大量の CPU を消費することなく、最適なレンダリング パスを選択できるようにする。

* **メタコマンド** メタコマンドは、IHV 高速化アルゴリズムを表す Direct3D12 オブジェクトです。 ドライバーによって実装されるコマンド ジェネレーターを非透過的に参照します。 メタコマンドの更新には、記述子テーブルのバインドやテクスチャのバインドなどが含まれます。 「[D3D12DDI_META_COMMAND_PARAMETER_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/ne-d3d12umddi-d3d12ddi_meta_command_parameter_type)」および「[D3D12DDIARG_META_COMMAND_PARAMETER_DESC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d12umddi/ns-d3d12umddi-d3d12ddiarg_meta_command_parameter_desc)」を参照してください。

  計算アルゴリズムでのテクスチャ リソース (スウィズル メモリ) の使用を有効にする
  * グラフィックス パイプライン アルゴリズムを有効にする

* **HDR 明るさ補正** SDR コンテンツの基準白色をユーザーの望む値にするために、新しい SDR 明るさブーストが導入されました。これにより、ユーザーが SDR ディスプレイに期待する明るさと同等の、標準的な 200 から 240 ニットで SDR コンテンツが再現されます。 SDR 明るさブーストは、次の 2 点において Brightness3 の動作全般に影響します。

  1. このブーストは、SDR コンテンツの事前ブレンドだけに適用されます。 HDR コンテンツへの影響はありません。 一方、ほとんどのラップトップ/brightness3 のシナリオで、ユーザーはすべてのコンテンツ (SDR と HDR) が調整されることを期待します。
  2. OS の Brightness3 スタックで望ましいニット値が判断されるとき、既に適用されている SDR ブーストは認識されません。

     そこで、HDR 用の Brightness3 DDI からのニット値が望ましい値になるように、ドライバーが補正を適用する必要があります。 グラフィックス ドライバー (およびダウンストリームの TCON など) は、望ましいニット値を得るためにコンテンツのピクセル値を変更します。そのため、アプリケーション ([D3DDDI_HDR_METADATA_HDR10](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_hdr_metadata_hdr10) を通じて) または OS の既定値 ([DxgkDdiSetTargetAdjustedColorimetry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_settargetadjustedcolorimetry) を通じて) によって提供されたとおりに HDR コンテンツ メタデータに適用される補正もあります。 グラフィックス ドライバー (TCON) がピクセル データの変更を行うため、HDR コンテンツ メタデータの補正もドライバーが行います。

* **HDR ピクセル形式のサポート** このカーネル モードのデバイス ドライバー インターフェイス (DDI) の変更は、ドライバー/デバイスによって報告される新機能を公開する WDDM 2.5 の一部で、ドライバー/デバイスによってサポートされる HDR 機能に関する情報を提供します。

   現在、ドライバー/デバイスで HDR がサポートされているかどうかは、[DdiUpdateMonitorLinkInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_updatemonitorlinkinfo) から読み取られる [DXGK_MONITORLINKINFO_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgk_monitorlinkinfo_capabilities) 構造体の *HighColorSpace* ビットに基づいて、OS で判断されます。 *HighColorSpace* ビットでは、HDR モードで実行するためのドライバー/リンク/モニター機能の組み合わせが提供されます。

    ドライバーによって報告される HDR 機能にドライバー/デバイス レベルの機能が含まれるようになりました。これにより、ドライバー/デバイスで True HDR (FP16HDR) がサポートされているか、または制限付き HDR (ARGB10HDR) のみがサポートされているかを OS で判断することができます (下の定義を参照)。

  * FP16HDR:ドライバー/デバイスは、スキャンアウト パイプラインで出力信号が HDR10 に変換されている間に、scRGB/CCC 色空間と共に FP16 ピクセル形式のサーフェスを取得して、PQ/2084 エンコードと BT.2020 プライマリを適用することができます。
  * ARGB10HDR:ドライバー/デバイスは、既に PQ/2084 でエンコードされている ARGB10 ピクセル形式のサーフェスを取得して、HDR10 信号をスキャン アウトすることができます。 ドライバー/デバイスでは、上の定義どおり FP16HDR を処理できないか、または scRGB FP16 の拡張された数値範囲を処理できません。

    グラフィックス ドライバーは、FP16HDR か ARGB10HDR のいずれかをサポート対象として報告できます。グラフィックス ドライバーはスーパーセット/サブセットの構成ではなく、FP16HDR と ARGB10HDR の両方が同時にサポート対象として報告されると、OS によるアダプターの起動が失敗するためです。 「[DXGK_MONITORLINKINFO_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgk_monitorlinkinfo_capabilities)」および「[_DXGK_DISPLAY_DRIVERCAPS_EXTENSION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_display_drivercaps_extension)」を参照してください。

* **SDR ホワイト レベル** カーネル モードのデバイス ドライバー インターフェイスに既存の DDI への新しいパラメーターが追加されました。これにより、グラフィックス ドライバーは、HDR モードで実行しているディスプレイについて、OS のコンポジターがすべての SDR コンテンツに適用している "SDR ホワイト レベル" の値を知ることができます。 「_DXGK_COLORIMETRY」を参照してください。

### <a name="kernel-1809"></a>Windows カーネル

コア カーネルに新しい API がいくつか追加されています。

* [RtlQueryRegistryValueWithFallback 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlqueryregistryvaluewithfallback):プライマリ ハンドルが存在しないときにフォールバック ハンドルを使ってレジストリ値のエントリを照会します。
* [PsGetSiloContainerId 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetsilocontainerid)と [PsGetThreadServerSilo 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetthreadserversilo)
* 次の新しい情報クラスが [_FILE_INFORMATION_CLASS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_file_information_class) に追加されました。
  * FileLinkInformationExBypassAccessCheck
  * FileCaseSensitiveInformationForceAccessCheck
  * FileStorageReserveIdInformation
    * FileLinkInformationEx
* NtCreateSection の拡張バージョンが、実際には AWE セクションであることを示すために、[NtCreateSectionEx 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatesectionex)に追加されました。
* 新しい Ex マクロは、Ntoskernel によってエクスポートされる実際のプッシュ ロック API に直接アクセスを付与します。
  * [ExAcquirePushLockExclusive マクロ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exacquirepushlockexclusive)
  * [ExAcquirePushLockShared マクロ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exacquirepushlockshared)
  * [ExInitializePushLock 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializepushlock)
  * [ExReleasePushLockExclusive マクロ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreleasepushlockexclusive)
  * [ExReleasePushLockShared マクロ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreleasepushlockshared)
* [KzLowerIrql](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kzlowerirql) と [KzRaiseIrql](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kzraiseirql) は、フォワーダに依存してインライン関数の特殊なケースをインスタンス化するのではなく、Windows 8 以降のバージョンをターゲットとするカーネル コンポーネントでサポートされる extern forceinline に移動されました。
* PCI の Flattening Portal Bridge (FPB) がサポートされるようになりました。 詳しくは、[正式な仕様](https://pcisig.com/sites/default/files/specification_documents/ECN_FPB_9_Feb_2017.pdf)をご覧ください。 新しい API (_PCI_FPB_*) が [Ntddk.h](https://review.docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/) で宣言されています。

### <a name="networking-1809"></a>ネットワーク

#### <a name="netadaptercx"></a>NetAdapterCx

* [NetAdapterCx クライアント ドライバーの INF ファイル](https://docs.microsoft.com/windows-hardware/drivers/netcx/inf-files-for-netadaptercx-client-drivers)に関する新しいトピック。
* API サーフェスを簡略化するために、キューの送受信がパケット キューと呼ばれる単一のオブジェクトの種類に統合されました。 「[Transmit and receive queues (キューの送信および受信)](https://docs.microsoft.com/windows-hardware/drivers/netcx/transmit-and-receive-queues)」トピックに「[Polling model (ポーリング モデル)](https://docs.microsoft.com/windows-hardware/drivers/netcx/transmit-and-receive-queues#polling-model)」という新しいセクションが追加されました。
* [ハードウェア オフロード](https://docs.microsoft.com/windows-hardware/drivers/netcx/netadaptercx-hardware-offloads)が NetAdapterCx に追加されており、関連するパケット拡張機能のクライアント ドライバーへの登録も自動化されます。
* ネットワーク インターフェイスがドライバーの WDF デバイス オブジェクトから切り離されました。 これをサポートするために、*EvtNetAdapterSetCapabilities* コールバック関数が削除されました。 NetAdapterCx クライアント ドライバーは、既定のものを含め複数のネットワーク インターフェイスを持てるようになりました。

   ネットワーク インターフェイスとデバイス オブジェクトの分離をサポートするために、次のトピックが更新されました。

  * [Summary of NetAdapterCx objects (NetAdapterCx オブジェクトの概要)](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-netadaptercx-objects)
  * [Device and adapter initialization (デバイスとアダプターの初期化)](https://docs.microsoft.com/windows-hardware/drivers/netcx/device-and-adapter-initialization)
  * [Power-up sequence for a NetAdapterCx client driver (NetAdapterCx クライアント ドライバーの電源投入シーケンス)](https://docs.microsoft.com/windows-hardware/drivers/netcx/power-up-sequence-for-a-netadaptercx-client-driver)
  * [Power-down sequence for a NetAdapterCx client driver (NetAdapterCx クライアント ドライバーの電源切断シーケンス)](https://docs.microsoft.com/windows-hardware/drivers/netcx/power-down-sequence-for-a-netadaptercx-client-driver)

* [NetAdapterCx の Receive Side Scaling (RSS)](https://docs.microsoft.com/windows-hardware/drivers/netcx/netadaptercx-receive-side-scaling-rss-) をサポートする DDI が簡略化されました。
* パケット コンテキスト トークン ヘルパー マクロが削除されました。

#### <a name="ndis"></a>NDIS

[Receive Side Scaling バージョン 2 (RSSv2)](https://docs.microsoft.com/windows-hardware/drivers/network/receive-side-scaling-version-2-rssv2-) がバージョン 1.01 に更新されました。

### <a name="mobilebroadband-1809"></a>モバイル ブロードバンド

* MBB デバイスのマルチ パケット データ プロトコル (MPDP) インターフェイスをサポートする新しい [OID](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-mpdp) と DDI。
* MBB デバイスとドライバーのリセット回復の信頼性を高める新しい[デバイスベースのリセットと回復](https://docs.microsoft.com/windows-hardware/drivers/network/mb-device-based-reset-and-recovery)機能。

#### <a name="mobile-broadband-wdf-class-extension-mbbcx"></a>モバイル ブロードバンド WDF クラス拡張機能 (MBBCx)

MBBCx 電源管理の方法が簡略化されました。

Windows 10 Version 1803 では MBBCx のプレビュー コンテンツが提供されていましたが、現在、MBBCx は Windows 10 Version 1809 バージョンの WDK に付属するようになりました。

#### <a name="mobile-operators"></a>携帯電話会社

[AutoConnectOrder 設定](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/desktop-cosa-apn-database-settings#apn-database-and-desktop-cosa-settings)がデスクトップ COSA でサポートされるようになりました。

### <a name="sensors-1809"></a>センサー

明るさの自動調整機能のサポート:

センサーでの明るさの自動調整をサポートするために、PKEY_SensorData_IsValid データ フィールドが追加されました。

詳しくは、「[Light sensor data fields (光センサー データ フィールド)](https://docs.microsoft.com/windows-hardware/drivers/sensors/light-sensor-data-fields)」をご覧ください。

### <a name="usb-1809"></a>USB

**USB Type-C ドライバー開発者向けの新機能:**

お使いのハードウェアが UCSI に準拠しており、非 ACPI トランスポート経由の通信が必要な場合は、新しいクラス拡張機能 &mdash; (UcmUcsiCx.sys) を利用できます。 これは、トランスポートに依存しない方法で UCSI 仕様を実装します。 最小限のコードで、UcmUcsiCx へのクライアントであるドライバーが非 ACPI トランスポート経由で USB Type-C ハードウェアと通信できます。 このトピックでは、UCSI クラス拡張機能で提供されるサービスと、クライアント ドライバーの想定される動作について説明します。

* [Write a UCSI client driver (UCSI クライアント ドライバーの作成)](https://docs.microsoft.com/windows-hardware/drivers/usbcon/write-a-ucsi-driver)
* [UcmUcsiCx クラス拡張機能のリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)
* [UcmUcsiCx クライアント ドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmUcsiAcpiSample)

**USB Type-C ドライバー開発者向けの新機能により、USB Type-C コネクタのアクティビティを監視したり、USB Type-C コネクタに関するポリシーの決定に関与したりすることが可能になりました。**

たとえば、温熱条件に基づいてデバイスの充電を制御して、デバイスの過熱を防ぐことができます。

* [Write a USB Type-C Policy Manager client driver (USB Type-C ポリシー マネージャー クライアント ドライバーの作成)](https://www.microsoft.com/windows-hardware/drivers/usbcon/policy-manager-client)
* [Usbpmapi.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/) で利用可能な新しい API

**エミュレートされた USB デバイス (UDE) で利用可能なクラス拡張機能の新しいバージョン-- 1.1 および USB ホスト コントローラー (Ucx) 1.5:**

エミュレートされたデバイスで、機能のリセット (FLDR) やプラットフォームのリセット (PLDR) による、より信頼性の高いリセット回復がサポートされるようになりました。 クライアント ドライバーからシステムに、デバイスのリセットが必要であることと、リセットの種類 (機能またはプラットフォーム) を通知できるようになりました。

* [UdecxWdfDeviceNeedsReset 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceneedsreset)

ホスト コントローラーでも、以下を通じて FLDR と PLDR のリセットを行えます。

* [EVT_UCX_USBDEVICE_DISABLE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_disable)

### <a name="wifi-1809"></a>Wi-Fi

WLAN デバイス ドライバー インターフェイス (WDI) 仕様がバージョン 1.1.7 に更新されました。

* WDI ドライバーの最新の 802.11ax PHY タイプのサポートが追加されました。
* 承諾されていないデバイス サービスの状態表示のサポートが追加されました。

## <a name="whats-new-in-windows-10-version-1803"></a>Windows 10 バージョン 1803 の新機能

このセクションでは、Windows 10 Version 1803 (Windows 10 April 2018 Update) でのドライバー開発に関する新機能と更新された機能について説明します。

[ページのトップへ](#top)

### <a name="acpi-1803"></a>ACPI

Windows 10 Version 1803 では、プラットフォームの機能と物理デバイスの位置情報をサポートするために、ACPI の DDI が更新されています。

### <a name="audio-1803"></a>オーディオ

[音声による有効化](https://docs.microsoft.com/windows-hardware/drivers/audio/voice-activation)に関するトピックが更新され、APO 要件に関する情報が追加されました。

### <a name="bluetooth-1803"></a>Bluetooth

Windows 10 Version 1803 では、クイック ペアリングのサポートが導入されます。 ユーザーが設定アプリに移動して、ペア設定する周辺機器を検索する必要がなくなりました。 使用可能な新しい周辺機器が近くで検出されると、Windows によって通知がポップアップ表示されます。 お使いの周辺機器をクイック ペアリングに確実に対応させるには、2 つの要件セットがあります。 1 つは周辺機器の動作に関するもので、もう 1 つは Microsoft が定義したベンダーのアドバタイズ セクションの構造と値に関するものです。 詳しくは、次のトピックをご覧ください。

* [Bluetooth クイック ペアリング](https://docs.microsoft.com/windows-hardware/design/component-guidelines/bluetooth-swift-pair)
* [Bluetooth の機能と推奨事項](https://docs.microsoft.com/windows-hardware/design/component-guidelines/bluetooth)

Windows 10 Version 1803 では Bluetooth バージョン 5.0 がサポートされます。 プロファイルのサポートについては、「[Bluetooth Version and Profile Support in Windows 10 (Windows 10 での Bluetooth バージョンとプロファイルのサポート)](https://docs.microsoft.com/windows-hardware/drivers/bluetooth/general-bluetooth-support-in-windows)」をご覧ください。

### <a name="camera-1803"></a>カメラ

カメラ ドライバーの開発では、次の更新が行われました。

* [DShow Bridge implementation guidance for UVC devices (UVC デバイス向け DShow (DirectShow) ブリッジ実装ガイド)](https://docs.microsoft.com/windows-hardware/drivers/stream/dshow-bridge-implementation-guidance-for-usb-video-class-devices) - USB ビデオ クラス (UVC) 仕様に準拠しているカメラとデバイス向けに DShow ブリッジを構成するための実装ガイド。 このプラットフォームは、USB バス標準から Microsoft OS 記述子を使って DShow ブリッジを構成します。 拡張プロパティ OS 記述子は USB の標準的な記述子の拡張機能です。標準仕様では有効にされない Windows 固有のデバイス プロパティを返すために、USB デバイスによって使用されます。
* [360 カメラのビデオ キャプチャ](https://docs.microsoft.com/windows-hardware/drivers/stream/360-camera-video-capture) - 既存の MediaCapture API を使い、360 カメラのプレビュー、キャプチャ、録画のサポートを提供します。 これにより、プラットフォームで球面のフレーム ソース (正距円筒図法のフレームなど) を公開することができ、アプリで 360 カメラのビデオ ストリームを検出して処理するだけでなく、360 キャプチャ エクスペリエンスを提供することが可能になります。

### <a name="display-1803"></a>ディスプレイ

Windows 10 Version 1803 では、ディスプレイ ドライバー開発に関する次の更新が行われました。

* **間接ディスプレイ UMDF クラス拡張機能** - 間接ディスプレイ ドライバーは、レンダリング GPU に SRM を渡すことができ、使用中の SRM バージョンを問い合わせるメカニズムを持つことができます。

* **IOMMU ハードウェア ベースの GPU 分離のサポート** - システム メモリへの GPU アクセスを制限することで、セキュリティを向上させます。

* **GPU 準仮想化のサポート** - ディスプレイ ドライバーが Hyper-V 仮想化環境にレンダリング機能を提供できるようにします。

* **明るさ** - マルチ ディスプレイをサポートする新しい明るさインターフェイスで、調整されたニット ベースの明るさレベルに設定することができます。

* **D3D11 ビットストリーム暗号化** - 8 バイトまたは 16 バイトの初期化ベクトルを使用する CENC、CENS、CBC1、および CBCS の公開をサポートするために D3D11 に追加された GUID とパラメーター。

* **D3D11 と D3D12 のビデオ デコード ヒストグラム** - 輝度ヒストグラムにより、メディア チームがヒストグラムの固定機能ハードウェアを活用して、HDR/EDR のシナリオにおけるトーン マッピングの品質を向上させることができます。 固定機能ハードウェアは、これらのシナリオで GPU が既に飽和状態にあり、並列処理を有効にする場合に便利です。 この機能は省略可能です。固定機能ハードウェアが利用できる場合にのみ実装してください。 この機能は 3D または計算を使って実装しないでください。

* **D3D12 ビデオ デコード**でデコード階層 II がサポートされるようになりました。これは、ドライバーで "*テクスチャの配列*" がサポートされることにより、アプリケーションが割り当てコストを償却し、解像度の変更中にピーク時のメモリ使用量を削減できることを意味します。

* **タイル リソース階層と LDA アトミック** - リンクされたアダプター (LDA) ノード間で機能するアトミック シェーダー命令のサポートを追加する新しいクロス ノード共有階層。 これにより、ISV が分割フレーム レンダリング (SFR) などの GPU レンダリング手法を複数実装することができるため、D3D11 で実現可能な機能が明らかに向上します。

* **GPU ディザリングのサポート** - ドライバーは、特定の時点のモードに対して有線信号でディザリングを実行できるかどうかを報告できます。 これにより、モニター リンクで物理的に使用可能なものよりも高い有効ビット深度が必要なシナリオ (HDMI 2.0 を介した HDR10 など) で、OS が明示的にディザリングを要求できます。

* **後処理による色調整のオーバーライド**- ディスプレイの色を調整または変更するようなすべての後処理を一時的に無効にするよう、OS からドライバーに要求できるようにします。 これは、特定のアプリケーションがディスプレイでの比色分析による正確な色動作を強制するシナリオをサポートし、OEM または IHV 独自のディスプレイの色調整と安全に共存します。

* **Direct3D12 とビデオ** - 次の機能へのアクセスを提供する新しい API と DDI:
  * ハードウェア アクセラレータによるビデオのデコード
  * コンテンツの保護
  * ビデオの処理

* **DisplayID** - グラフィックス アダプターによって制御されているディスプレイから VESA の DisplayID 記述子を問い合わせることができるように設計され、DisplayID v1.3 と DisplayID v2.0 をサポートする新しい DDI。 この DDI は既存の DxgkDdiQueryAdapterInfo DDI の拡張機能であり、カーネル モードのディスプレイ専用ドライバーや間接ディスプレイ ドライバーを含む、DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WDDM2_3 のすべてのドライバーでサポートされます。

* **GPU パフォーマンス データ** - DdiQueryAdapterInfo の拡張機能により、温度、ファン速度、エンジンおよびメモリのクロック速度、メモリ帯域幅、電力、電圧などの情報が公開されます。

* その他 - IHV による新しいドライバーのオンボードに役立つ新しい SupportContextlessPresent ドライバー キャップ。

* OS での外部/リムーバブル GPU サポートの強化。 優れたサポートを追加する最初の手順として、Dxgkrnl では GPU が "切り離し可能" (ホットプラグ可能) かどうかを判断する必要があります。 RS4 では、独自のインフラストラクチャを構築する代わりに、ドライバーのこの情報を活用します。 このため、DXGK_ DRIVERCAPS 構造体に "Detachable" ビットが追加されています。 アダプターがホットプラグ可能な場合、アダプターの初期化中にドライバーによってこのビットが設定されます。

* **ディスプレイ診断** - カーネル モードのデバイス ドライバー インターフェイス (DDI) が変更され、ディスプレイ コントローラーのドライバーから OS に診断イベントを報告できるようになりました。  ドライバーはこのチャネルを通じて、(OS の要求に対する応答でも、OS による対応が必要なものでもないため) 通常は OS で認識されないイベントのログを記録することができます。

* **共有グラフィックス電源コンポーネント** - 非グラフィックス ドライバーでグラフィックス デバイスの電源管理を行えるようにします。  非グラフィックス ドライバーはグラフィックス ドライバーと連携し、ドライバー インターフェイスを介して 1 つ以上の共有電源コンポーネントを管理します。

* **共有テクスチャの機能強化** - プロセスや D3D デバイス間で共有可能なテクスチャの種類が増えました。 この設計により、最小限のメモリのコピーだけで、フレーム サーバーの OS コンポーネントでモノクロがサポートされるようになります。

### <a name="security-1803"></a>ドライバーのセキュリティ

[Windows ドライバー セキュリティ ガイダンス](https://docs.microsoft.com/windows-hardware/drivers/driversecurity/)と、ドライバー開発者向けにドライバー セキュリティのチェックリストを提供する[ドライバー セキュリティ チェックリスト](https://docs.microsoft.com/windows-hardware/drivers/driversecurity/driver-security-checklist)が更新されました。

### <a name="kernel-1803"></a>Windows カーネル

このセクションでは、Windows 10 Version 1803 での Windows カーネル ドライバー開発に関する新機能と更新された機能について説明します。

サード パーティが独自の KDNET 拡張性モジュールや KdSerial トランスポート レイヤーを作成できるように、新しい API のセットがキットに追加されました。 サンプル コードについては、Debuggers フォルダーの "カーネル トランスポート サンプル" (ddk\samples\kdserial および ddk\samples\kdnet) をご覧ください。

ファイルの状態を格納する場所として、(オペレーティング システムで認識されている) 承認された場所をドライバーに提供するためのサポートが追加されました。  この方法により、システムが格納場所にあるファイルをデバイスやドライバーと関連付けることができます。

ファイルの状態が格納される場所は、ドライバーの内部構成ごと、およびデバイスごとにそれぞれ異なります。 ファイルの状態を持つドライバーに対して、次のどちらの状態をディスクに書き込むかを指定できます。

* ドライバーの状態 ([IoGetDriverDirectory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdriverdirectory)): 複数のデバイスを制御している可能性があるドライバーに対してグローバル、または

* デバイスの状態 ([IoGetDeviceDirectory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdevicedirectory)): ドライバーによって制御される単一のデバイスに固有の値で、他のデバイスでは同様の状態であっても値が異なる場合があります。

機能ドライバー (FDO) で、それぞれの PCIe デバイスが D3Cold 状態にあるとき、追加の電力をネゴシエートできるようになりました。 たとえば、次のようなアニメーションや効果を作成できます。

* 補助電源要件 [D3COLD_REQUEST_AUX_POWER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-d3cold_request_aux_power)。
* コア電源レール [D3COLD_REQUEST_CORE_POWER_RAIL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-d3cold_request_core_power_rail)。
* システムが ACPI 動作状態にあり、対応するエンドポイントまたは PCI Express アップストリーム ポートが D3cold に遷移する間に、PCI Express ダウンストリーム ポートでメッセージを受信してからプラットフォームがスロットに PERST# をアサートするまでの固定遅延時間の要件。 「[D3COLD_REQUEST_PERST_DELAY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-d3cold_request_perst_delay)」を参照してください。

NT サービスおよびカーネル モードとユーザー モードのドライバーは、[RtlRaiseCustomSystemEventTrigger](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlraisecustomsystemeventtrigger) 関数を使うことで、デバイスに対してカスタム トリガーを実行することができます。 ドライバーの開発者が所有するカスタム トリガーは、カスタム トリガー ID によって識別される関連バック グラウンド タスクを開始するよう、システムのイベント ブローカーに通知します。

アクティブ セッションの変更通知に登録して、通知が発生したときにコールバックを取得できるようになりました。 この通知の一環として、一部のデータが呼び出し元で共有されます。 この関連付けられているデータは、[PO_SPR_ACTIVE_SESSION_DATA 構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntpoapi/ns-ntpoapi-_po_spr_active_session_data)を介して配信されます。

### <a name="networking-1803"></a>ネットワーク

このセクションでは、Windows 10 Version 1803 での Windows ネットワーク ドライバー開発に関する新機能と強化された機能について簡単に説明します。

#### <a name="ndis-and-netadaptercx"></a>NDIS および NetAdapterCx

NDIS では次の更新が行われました。

* [Receive Side Scaling V2](https://docs.microsoft.com/windows-hardware/drivers/network/receive-side-scaling-version-2-rssv2-in-ndis-6-80) が更新され、ステアリング パラメーターに関する詳細情報が追加されました。
* [同期 OID インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/network/synchronous-oid-request-interface-in-ndis-6-80)で NDIS 軽量フィルター ドライバーがサポートされるようになりました。

ネットワーク アダプターの WDF クラス拡張機能 (NetAdapterCx) に関する次のトピックが新たに追加されました。

* [NetAdapterCx 1.2 の概要](https://docs.microsoft.com/windows-hardware/drivers/netcx/introduction-to-netadaptercx-1-2)
* [Packet descriptors and extensions (パケットの記述子と拡張機能)](https://docs.microsoft.com/windows-hardware/drivers/netcx/packet-descriptors-and-extensions)
* [Network data buffer management (ネットワーク データ バッファーの管理)](https://docs.microsoft.com/windows-hardware/drivers/netcx/network-data-buffer-management)
* [NetAdapterCx Receive Side Scaling (RSS)](https://docs.microsoft.com/windows-hardware/drivers/netcx/netadaptercx-receive-side-scaling-rss-)

さらに、モバイル ブロードバンド クラス拡張機能 (MBBCx) に関する新しいトピックも追加されました。これは、モバイル ブロードバンド接続に NetAdapterCx モデルを使用するプレビュー専用の機能です。

* [Mobile Broadband Class Extension (MBBCx) (モバイル ブロードバンド クラス拡張機能 (MBBCx))](https://docs.microsoft.com/windows-hardware/drivers/netcx/mobile-broadband-mbb-wdf-class-extension-mbbcx-)
  * [Writing an MBBCx client driver (MBBCx クライアント ドライバーの作成)](https://docs.microsoft.com/windows-hardware/drivers/netcx/writing-an-mbbcx-client-driver)
  * [MBBCx API リファレンス](https://docs.microsoft.com/windows-hardware/drivers/netcx/mbbcx-api-reference)

### <a name="mobilebroadband-1803"></a>モバイル ブロードバンド

モバイル ブロードバンドについては、[MB 低レベル UICC アクセス](https://docs.microsoft.com/windows-hardware/drivers/network/mb-low-level-uicc-access)について詳しく説明した新しいトピックが追加されました。

#### <a name="mobile-operators"></a>携帯電話会社

新しいホットスポットと AppID の設定が[デスクトップ COSA](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/desktop-cosa-apn-database-settings#desktop-cosa-only-settings) の一部になりました。 通信事業者が [Sysdev メタデータ パッケージ](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/service-metadata)を使ってブロードバンド アプリ エクスペリエンスのアプリを提供している場合は、[MO UWP アプリ](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/uwp-mobile-broadband-apps)と [COSA データベース](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/desktop-cosa-apn-database-settings)に移行することを強くお勧めします。

### <a name="pci-1803"></a>PCIe

次のモダン スタンバイと PCI ホット プラグのシナリオをサポートするために、新しい ACPI _DSD メソッドが追加されました。

* PCIe ルート ポートでの DDRIPS (指示された最も深いランタイム アイドル電源状態) のサポート
* D3 でのホット プラグをサポートする PCIe ルート ポートの識別
* 外部に公開されている PCIe ルート ポートの識別

詳しくは、「[ACPI Interface:Device Specific Data (_DSD) for PCIe Root Ports (ACPI インターフェイス: PCIe ルート ポートのデバイス固有のデータ (_DSD))](https://docs.microsoft.com/windows-hardware/drivers/pci/dsd-for-pcie-root-ports)」をご覧ください。

### <a name="sensors-1803"></a>センサー

接続の種類のプロパティを明確にするために、[SENSOR_CONNECTION_TYPES 列挙](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsdef/ne-sensorsdef-sensor_connection_types)が追加されました。

### <a name="usb-1803"></a>USB

共有コネクタのデタッチをシミュレートするための新しい API が追加されました。 USB デバイスがホストに接続されているか共有コネクタを持っている場合、スタックが削除されるときにデバイスがホストに接続されているか共有コネクタを持っていれば、デタッチ イベントをシミュレートできます。 この時点ですべてのアタッチ/デタッチ通知メカニズムが無効になります。 詳しくは、「[UfxDeviceNotifyFinalExit 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdevicenotifyfinalexit)」をご覧ください。

### <a name="wifi-1803"></a>Wi-Fi

Wi-Fi ドライバーの開発では、[高度な電源管理機能である Nic Auto Power Saver (NAPS) の TLV](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-os-power-management-features) が新たに追加され、プラットフォーム レベルのデバイス回復サービス (PLDR) が更新されています。

## <a name="whats-new-in-windows-10-version-1709"></a>Windows 10 バージョン 1709 の新機能

このセクションでは、Windows 10 Version 1709 でのドライバー開発に関する新機能と更新された機能について説明します。

[ページのトップへ](#top)

### <a name="audio-1709"></a>オーディオ

Windows 10 Version 1709 では、Windows オーディオ ドライバーの開発に関する次の更新が行われました。

* 「[Configure and query audio device modules (オーディオ デバイス モジュールの構成とクエリ)](https://docs.microsoft.com/windows-hardware/drivers/audio/configure-and-query-audiodevicemodules)」が新たに追加されました。
* 「[voice activation (音声によるアクティブ化)](https://docs.microsoft.com/windows-hardware/drivers/audio/voice-activation)」が全面的に更新されました。
  * チェーンとキーワードのみのアクティブ化に関する詳細情報
  * 新しい用語集
  * トレーニングや認識に関する追加情報 (暗証番号やオーディオ形式の情報など)
  * 更新されたキーワード システムの概要
  * 音声によるスリープ解除に関する最新情報

### <a name="acpi-1709"></a>ACPI

以下は、入力/出力バッファーをサポートする新しい ACPI (Advanced Configuration and Power Interface) DDI の一覧です。

* [ACPI_EVAL_INPUT_BUFFER_COMPLEX_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1)
* [ACPI_EVAL_INPUT_BUFFER_COMPLEX_V1_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v1_ex)
* [ACPI_EVAL_INPUT_BUFFER_COMPLEX_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v2)
* [ACPI_EVAL_INPUT_BUFFER_COMPLEX_V2_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_complex_v2_ex)
* [ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v1)
* [ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v2)
* [ACPI_EVAL_INPUT_BUFFER_SIMPLE_INTEGER_V2_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_integer_v2_ex)
* [ACPI_EVAL_INPUT_BUFFER_SIMPLE_STRING_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1)
* [ACPI_EVAL_INPUT_BUFFER_SIMPLE_STRING_V1_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v1_ex)
* [ACPI_EVAL_INPUT_BUFFER_SIMPLE_STRING_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v2)
* [ACPI_EVAL_INPUT_BUFFER_SIMPLE_STRING_V2_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_simple_string_v2_ex)
* [ACPI_EVAL_INPUT_BUFFER_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1)
* [ACPI_EVAL_INPUT_BUFFER_V1_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v1_ex)
* [ACPI_EVAL_INPUT_BUFFER_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v2)
* [ACPI_EVAL_INPUT_BUFFER_V2_EX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_input_buffer_v2_ex)
* [ACPI_EVAL_OUTPUT_BUFFER_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v1)
* [ACPI_EVAL_OUTPUT_BUFFER_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_eval_output_buffer_v2)
* [ACPI_METHOD_ARGUMENT_V1](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v1)
* [ACPI_METHOD_ARGUMENT_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpiioct/ns-acpiioct-_acpi_method_argument_v2)
* [GIC_ITS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/acpitabl/ns-acpitabl-_gic_its)

### <a name="biometric-1709"></a>生体認証

Windows 生体認証ドライバーの署名の要件が追加されました。 詳しくは、「[Signing WBDI Drivers (WBDI ドライバーへの署名)](https://docs.microsoft.com/windows-hardware/drivers/biometric/signing-wbdi-drivers)」をご覧ください。

### <a name="display-1709"></a>ディスプレイ

Windows 10 Version 1709 では、Windows ディスプレイ ドライバーの開発に関する次の新機能が追加されました。

* Display ColorSpace Transform DDI により、ポストコンポジション ディスプレイ パイプラインに適用される色空間の変換をより詳細に制御できます。
* D3D12 のコピー キュー タイムスタンプ クエリ機能により、アプリケーションが COPY コマンドのリスト/キューに対してタイムスタンプ クエリを発行できるようになります。 これらのタイムスタンプを指定することで、他のエンジンのタイムスタンプと同じように機能します。
* 以下を介した Direct3D12 ランタイムへのビデオの統合が強化されました。
    1. ハードウェア アクセラレータによるビデオのデコード
    2. コンテンツの保護
    3. ビデオの処理

### <a name="hardware-notifications-1709"></a>ハードウェア通知

Windows 10 Version 1709 には、通知コンポーネント (LED、振動のメカニズムなど) のハードウェアに依存しないサポートのためのサポートがあります。 詳しくは、次のトピックをご覧ください。

* [Hardware notifications support (ハードウェア通知のサポート)](https://docs.microsoft.com/windows-hardware/drivers/gpiobtn/hardware-notifications-support)
* [ハードウェア通知リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_gpiobtn/)

### <a name="kernel-1709"></a>Windows カーネル

Windows 10 Version 1709 では、ドライバーの Windows カーネルに新しいルーチンがいくつか追加されています。

* ExGetFirmwareType および ExIsSoftBoot &ndash; エグゼクティブ ライブラリ サポート ルーチン。
* [PsSetLoadImageNotifyRoutineEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-pssetloadimagenotifyroutineex) &ndash; 実行可能なすべてのイメージ (オペレーティング システムのネイティブ アーキテクチャとは異なるアーキテクチャを持つイメージも含む) の拡張イメージ通知ルーチン。
* [MmMapMdl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmapmdl) &ndash; メモリ記述子の一覧 (MDL) に記述されている物理ページをシステムの仮想アドレス空間にマッピングするための[メモリ マネージャー](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-kernel-mode-memory-manager) ルーチン。
* [PoFxSetTargetDripsDevicePowerState](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxsettargetdripsdevicepowerstate) &ndash; デバイスのターゲット デバイスが DRIPS の電源状態になったことを電源マネージャーに通知する PoFx ルーチン。
* 以下は、処理ポリシーに関連する [ZwSetInformationThread](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-zwsetinformationthread) ルーチンの新しいオプションの一覧です。

  * [PROCESS_MITIGATION_CHILD_PROCESS_POLICY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_process_mitigation_child_process_policy)
  * [PROCESS_MITIGATION_PAYLOAD_RESTRICTION_POLICY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_process_mitigation_payload_restriction_policy)
  * PROCESS_READWRITEVM_LOGGING_INFORMATION

* [PsGetServerSiloActiveConsoleId](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetserversiloactiveconsoleid) と [PsGetParentSilo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-psgetparentsilo) &ndash; マシン上で作成および破棄されるサーバー サイロに関する情報を取得する新しいサイロ API。
* 以下は、イベントと生成されたログを診断目的で参照する相関関係ベクトルを使用するための新しい RTL 関数の一覧です。
  * [CORRELATION_VECTOR](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-correlation_vector)
  * [RtlExtendCorrelationVector](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlextendcorrelationvector)
  * [RtlIncrementCorrelationVector](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlincrementcorrelationvector)
  * [RtlInitializeCorrelationVector](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlinitializecorrelationvector)
  * [RtlValidateCorrelationVector](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-rtlvalidatecorrelationvector)

### <a name="mobilebroadband-1709"></a>モバイル ブロードバンド

Windows 10 Version 1709 では、ドライバー開発に関する Windows モバイル ブロードバンドと通信事業者のシナリオに次の新機能が追加されました。

* [UICC のリセット](https://docs.microsoft.com/windows-hardware/drivers/network/mb-uicc-reset-operations)と[モデムのリセット](https://docs.microsoft.com/windows-hardware/drivers/network/mb-modem-reset-operations)
* [プロトコル構成操作 (PCO)](https://docs.microsoft.com/windows-hardware/drivers/network/mb-protocol-configuration-operations--pco-)
* [基地局情報の問い合わせ](https://docs.microsoft.com/windows-hardware/drivers/network/mb-base-stations-information-query-support)
* [eSIM と MBIM ReadyState のガイダンス](https://docs.microsoft.com/windows-hardware/drivers/network/mb-esim-mbim-ready-state-guidance)

Windows 10 Version 1709 では、[デスクトップ COSA のドキュメント](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/planning-your-desktop-cosa-apn-database-submission)が更新され、ブランド関連のフィールドが新たに追加されました。
通信事業者のシナリオに関するその他の変更については、[非推奨の機能](#deprecated-features)の一覧をご覧ください。

### <a name="networking-1709"></a>ネットワーク

このセクションでは、Windows 10 Version 1709 での Windows ネットワーク ドライバー開発に関する新機能と強化された機能について簡単に説明します。

以下は、NDIS の新機能と更新された機能の一覧です。

* NewAdapterCx の新機能を含む NetAdapterCx 1.1 の概要:
  * パケット コンテキスト オプションの追加
  * リンク状態の微調整
  * 受信バッファーの管理とパフォーマンスの改善
  * 全般的なパフォーマンスの向上
* NDIS 6.80 の新しい[同期 OID 要求インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/network/synchronous-oid-request-interface-in-ndis-6-80)
* NDIS 6.80 の新しい [Receive Side Scaling バージョン 2 (RSSv2)](https://docs.microsoft.com/windows-hardware/drivers/network/receive-side-scaling-version-2-rssv2-in-ndis-6-80)
* [NDIS 6.80 の概要](https://docs.microsoft.com/windows-hardware/drivers/network/introduction-to-ndis-6-80)
* [NDIS 6.x ドライバーの NDIS 6.80 への移植](https://docs.microsoft.com/windows-hardware/drivers/network/porting-ndis-6-x-drivers-to-ndis-6-80)

### <a name="pci-1709"></a>仮想化 PCI

PCI Express シングルルート I/O 仮想化 (SR-IOV) 仕様に準拠するデバイスの物理機能ドライバーを作成するための新しいプログラミング インターフェイスがあります。 このインターフェイスは Pcivirt.h で宣言されます。 詳しくは、「[PCI virtualization (PCI の仮想化)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pcivirt/)」をご覧ください。

### <a name="pwm-1709"></a>パルス幅変調 (PWM) コントローラー

Windows 10 Version 1709 では、SoC の一部であるパルス幅変調 (PWM) コントローラーへのアクセスと SoC アドレス空間へのメモリ マップを提供するために、カーネル モードのドライバーを作成する必要があります。 詳しくは、「[PWM driver for an on-SoC PWM module (on-SoC PWM モジュールの PWM ドライバー)](https://docs.microsoft.com/windows-hardware/drivers/spb/pulse-width-controller%20driver?branch=spb)」をご覧ください。

PIN のパスを解析して検証し、PIN 番号を抽出するには、カーネル モデル ドライバーで [PwmParsePinPath](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pwmutil/nf-pwmutil-pwmparsepinpath) を使用する必要があります。

アプリは [PWM IOCTL](https://docs.microsoft.com/windows-hardware/drivers/spb/pulse-width-controller%20driver#pwm-ioctl-requests) 要求を送信することで、コントローラー ドライバーに要求を送ることができます。

### <a name="storage-1709"></a>ストレージとファイル システム

ファイル システムとストレージでは、Universal Flash Storage に追加のサポートを提供するために、ufs.h ヘッダーが Windows 10 Version 1709 に追加されました。

Posix の更新には、新しい関数 **delete** と **rename** が含まれています。

Windows 10 Version 1709 で更新されたヘッダーは次のとおりです。

* ata.h
* fltKernel.h
* minitape.h
* ntddscsi.h
* ntddstor.h
* ntddvol.h
* ntifs.h
* scsi.h
* storport.h

### <a name="usb-1709"></a>USB

このセクションでは、Windows 10 Version 1709 での USB に関する新機能について説明します。

#### <a name="media-agnostic-usb-ma-usb-protocol"></a>Media Agnostic USB (MA-USB) プロトコル

USB ドライバー スタックは、Media Agnostic USB (MA-USB) プロトコルを使うことで、Wi-Fi などの非 USB 物理メディアを介して USB パケットを送信することができます。 この機能を実装するために、新しいプログラミング インターフェイスがリリースされています。 ドライバーは、この新しい DDI により、[_URB_GET_ISOCH_PIPE_TRANSFER_PATH_DELAYS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_get_isoch_pipe_transfer_path_delays) に関連付けられている遅延を判断することができます。 この情報を取得するには、新しい URB 要求を作成します。
この新機能については、次のトピックをご覧ください。

* [Media-Agnostic (MA-USB) 用 USB クライアント ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-client-drivers-for-ma-usb)
* [_URB_GET_ISOCH_PIPE_TRANSFER_PATH_DELAYS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_get_isoch_pipe_transfer_path_delays)
* [USB 要求ブロック (URB)](https://docs.microsoft.com/windows-hardware/drivers/usbcon/communicating-with-a-usb-device)

MA-USB をサポートするには、ホスト コントローラーのドライバーが特定のコールバック関数を実装することでトランスポートの特性を提供する必要があります。 次の表は、MA-USB をサポートするコールバック関数と構造体を示しています。

| コールバック関数 | 構造体 |
| ----- | ----- |
| [EVT_UCX_USBDEVICE_GET_CHARACTERISTIC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_get_characteristic) | [UCX_ENDPOINT_ISOCH_TRANSFER_PATH_DELAYS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/ns-ucxendpoint-_ucx_endpoint_isoch_transfer_path_delays) |
| [EVT_UCX_USBDEVICE_RESUME](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_resume) | [UCX_CONTROLLER_ENDPOINT_CHARACTERISTIC_PRIORITY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/ne-ucxendpoint-_ucx_endpoint_characteristic_priority) |
| [EVT_UCX_USBDEVICE_SUSPEND](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_suspend) | [UCX_ENDPOINT_CHARACTERISTIC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/ns-ucxendpoint-_ucx_endpoint_characteristic) |
| [EVT_UCX_ENDPOINT_GET_ISOCH_TRANSFER_PATH_DELAYS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_get_isoch_transfer_path_delays) | [UCX_ENDPOINT_CHARACTERISTIC_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/ne-ucxendpoint-_ucx_endpoint_characteristic_type) |
| [EVT_UCX_ENDPOINT_SET_CHARACTERISTIC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_set_characteristic) | [UCX_ENDPOINT_ISOCH_TRANSFER_PATH_DELAYS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/ns-ucxendpoint-_ucx_endpoint_isoch_transfer_path_delays) |

#### <a name="synchronized-system-qpc-with-usb-frame-and-microframes"></a>USB のフレームやマイクロフレームと同期するシステム QPC

フレームやマイクロフレームと同期するシステム クエリ パフォーマンス カウンター (QPC) 値を取得する新しいプログラミング インターフェイスがあります。

この情報は、呼び出し元がホスト コントローラーでこの機能を有効にしている場合にのみ取得されます。 この機能を有効にするには、ホスト コントローラーのドライバーで次のコールバック関数を実装する必要があります。

* [EVT_UCX_CONTROLLER_GET_FRAME_NUMBER_AND_QPC_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_get_frame_number_and_qpc_for_time_sync)
* [EVT_UCX_CONTROLLER_START_TRACKING_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_start_tracking_for_time_sync)
* [EVT_UCX_CONTROLLER_STOP_TRACKING_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_stop_tracking_for_time_sync)

アプリケーションは、次の API を使って機能を有効または無効にし、情報を取得することができます。

* [WinUsb_GetCurrentFrameNumberAndQpc](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getcurrentframenumberandqpc)
* [WinUsb_StartTrackingForTimeSync](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_starttrackingfortimesync)
* [WinUsb_StopTrackingForTimeSync](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_stoptrackingfortimesync)

他のドライバーは、次の IOCTL 要求を送信して機能を有効または無効にし、情報を取得することができます。

* [IOCTL_USB_GET_FRAME_NUMBER_AND_QPC_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_get_frame_number_and_qpc_for_time_sync)
* [IOCTL_USB_START_TRACKING_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_start_tracking_for_time_sync)
* [IOCTL_USB_STOP_TRACKING_FOR_TIME_SYNC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_usb_stop_tracking_for_time_sync)

USB フレームやマイクロフレームと同期するシステム OPC のサポート構造を次に示します。

* [USB_START_TRACKING_FOR_TIME_SYNC_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ns-usbioctl-_usb_start_tracking_for_time_sync_information)
* [USB_STOP_TRACKING_FOR_TIME_SYNC_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ns-usbioctl-_usb_stop_tracking_for_time_sync_information)
* [USB_FRAME_NUMBER_AND_QPC_FOR_TIME_SYNC_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ns-usbioctl-_usb_frame_number_and_qpc_for_time_sync_information)

#### <a name="ioctl_ucmtcpci_port_controller_displayport_display_out_status_changed"></a>IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS_CHANGED

[IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS_CHANGED](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmtcpciportcontrollerrequests/ni-ucmtcpciportcontrollerrequests-ioctl_ucmtcpci_port_controller_displayport_display_out_status_changed) 要求は、USB Type-C ポート コントローラー インターフェイス フレームワーク拡張機能の新しい要求です。 この要求は、DisplayPort 接続のディスプレイ出力の状態が変更されたことをクライアント ドライバーに通知します。

IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS_CHANGED 要求をサポートする構造体を次に示します。

* [UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS_CHANGED_IN_PARAMS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmtcpciportcontrollerrequests/ns-ucmtcpciportcontrollerrequests-_ucmtcpci_port_controller_displayport_display_out_status_changed_in_params)
* [UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_DISPLAY_OUT_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmtcpciportcontrollerrequests/ne-ucmtcpciportcontrollerrequests-_ucmtcpci_port_controller_displayport_display_out_status)

## <a name="whats-new-in-windows-10-version-1703"></a>Windows 10 バージョン 1703 の最新情報

このセクションでは、Windows 10 Version 1703 でのドライバー開発に関する新機能と強化された機能について説明します。

[ページのトップへ](#top)

### <a name="audio-1703"></a>オーディオ

Windows 10 Version 1703 では、Windows オーディオ ドライバーの開発に関する次のトピックが新たに追加されました。

* [オーディオ モジュール通信の実装](https://docs.microsoft.com/windows-hardware/drivers/audio/implementing-audio-module-communication) - ユニバーサル Windows プラットフォーム (UWP) アプリからカーネル モードのオーディオ デバイス ドライバーへの通信のサポートについて説明します。
* APO モジュール通信の検出をサポートする新しい DDI とプロパティのリファレンス トピック:
  * [KSPROPSETID_AudioModule](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-audiomodule) - オーディオ モジュールに固有の 3 つのプロパティを定義する新しい KS プロパティ セット。
  * [KSPROPERTY_AUDIOMODULE_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audiomodule-command) プロパティ - オーディオ モジュールのクライアントがカスタム コマンドを送信して、オーディオ モジュールに対してクエリを実行してパラメーターを設定できるようにします。
  * [IPortClsNotifications](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportclsnotifications) - オーディオ モジュールの通信をサポートするために、ミニポートへの通知ヘルパーを提供する新しいポート クラスの通知。

### <a name="bluetooth-1703"></a>Bluetooth

Windows 10 Version 1703 では、Bluetooth に関する次の更新が行われました。

* Windows 10 デスクトップ エディションでの広帯域音声認識を含む、ハンズフリー プロファイル (HFP) 1.6 仕様。
* Windows 10 デスクトップ エディションでの[コール コントロール API](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Calls) のサポート。
* GATT サーバー、Bluetooth LE 周辺機器、および Bluetooth LE のペアリングなしのサポートに対するサポート。 詳しくは、[開発者の投稿](https://aka.ms/bluetoothgatt)をご覧ください。

Bluetooth の新機能について詳しくは、「[Bluetooth](https://docs.microsoft.com/windows-hardware/design/component-guidelines/bluetooth)」および「[Bluetooth LE pre-pairing (Bluetooth LE の事前ペアリング)](https://docs.microsoft.com/windows-hardware/design/component-guidelines/bluetooth-prepairing)」をご覧ください。

### <a name="camera-1703"></a>カメラ

Windows 10 Version 1703 では、カメラ ドライバーの開発に関する次の更新が行われました。

* [USB ビデオ クラス (UVC) ドライバー実装ガイド](https://docs.microsoft.com/windows-hardware/drivers/stream/uvc-driver-implementation-checklist)
* [USB ビデオ クラス 1.5 仕様に対する Microsoft の拡張機能](https://docs.microsoft.com/windows-hardware/drivers/stream/uvc-extensions-1-5)
* [デバイス変換マネージャー (DTM) のイベント](https://docs.microsoft.com/windows-hardware/drivers/stream/device-mft-events)
* [IMFDeviceTransform インターフェイス](https://docs.microsoft.com/windows/desktop/api/mftransform/nn-mftransform-imfdevicetransform)
* KSCategory_Xxx デバイス インターフェイス クラス
  * [KSCATEGORY_SENSOR_CAMERA](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-sensor-camera)
  * [KSCATEGORY_VIDEO_CAMERA](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-video-camera)

### <a name="kernel-1703"></a>Windows カーネル

[Windows カーネル モードのプロセスとスレッド マネージャー](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-kernel-mode-process-and-thread-manager) - Windows 10 Version 1703 以降、Windows Subsystem for Linux (WSL) により、他の Windows アプリケーションと共に、ネイティブの Linux ELF64 バイナリを Windows で実行できるようになりました。 バイナリの実行に必要な WSL アーキテクチャと、ユーザー モードとカーネル モードのコンポーネントについて詳しくは、[Windows Subsystem for Linux](https://blogs.msdn.microsoft.com/wsl/) ブログの投稿をご覧ください。

### <a name="mobilebroadband-1703"></a>モバイル ブロードバンド

[**モバイル ブロードバンド (MB)** ](https://docs.microsoft.com/windows-hardware/drivers/network/mobile-broadband--mb--design-guide) の更新には、[LTE アタッチ機能](https://docs.microsoft.com/windows-hardware/drivers/network/mb-lte-attach-operations)の向上、[マルチ SIM 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-multi-sim-operations)のサポート、モデムへの[コンテキストのプロビジョニング](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provisioned-context-operations)のサポート、[SAR (比吸収率) プラットフォーム](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)のサポート、[ネットワーク ブラックリスト登録](https://docs.microsoft.com/windows-hardware/drivers/network/mb-network-blacklist-operations)のサポートなどがあります。

[**通信事業者のシナリオ (MOs)** ](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/apn-database-overview) の更新では、Windows デスクトップ MB デバイスをプロビジョニングする MOs に使用する、[COSA FAQ](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/cosa-overview) と呼ばれる新しいデータベース形式が追加されました。 その他の更新内容については、次のトピックをご覧ください。

* [Planning your COSA/APN database submission (COSA/APN データベースの提出の計画)](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/planning-your-desktop-cosa-apn-database-submission)
* [Submitting the COSA/APN database update (COSA/APN データベースの更新の提出)](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/submitting-the-desktop-cosa-apn-database-update)
* [Testing your COSA/APN database submission (COSA/APN データベースの提出のテスト)](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/testing-your-desktop-cosa-apn-database-submission)

### <a name="networking-1703"></a>ネットワーク

Windows 10 Version 1703 でのネットワーク ドライバー開発に対する更新では、ストリーム ソケットと呼ばれる新しい種類のソケットが追加されました。これにより、Windows で Linux ネットワーク アプリケーションがサポートされます。 詳しくは、[**Winsock カーネル**](https://docs.microsoft.com/windows-hardware/drivers/network/winsock-kernel-socket-categories)に関する記事をご覧ください。 [WskConnectEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_connect_ex)、[WskListen](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_listen)、[WSK_CLIENT_STREAM_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_client_stream_dispatch)、[WSK_PROVIDER_STREAM_DISPATCH](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_provider_stream_dispatch) などの新しい関数や構造体が追加されています。

### <a name="pos-1703"></a>POS

Windows 10 Version 1703 では、POS に関する次のトピックが新たに追加されました。

* [Bluetooth バーコード スキャナー UUID](https://docs.microsoft.com/windows-hardware/drivers/pos/barcode-scanner-bluetooth-service-uuids)
* [BarcodeSymbologyDecodeLenthType 列挙](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicecommontypes/ne-pointofservicecommontypes-_barcodesymbologydecodelengthtype)
* [BarcodeSymbologyAttributesData 構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicecommontypes/ns-pointofservicecommontypes-_barcodesymbologyattributesdata)

[BarcodeSymbology 列挙](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicecommontypes/ne-pointofservicecommontypes-_barcodesymbology)に対する新しい Gs1DWCode シンボル体系があります。

### <a name="usb-1703"></a>USB

Windows 10 Version 1703 では、USB Type-C ポート コントローラー インターフェイス仕様をサポートする新しいクラス拡張機能 (UcmTcpciCx.sys) が提供されます。 USB Type-C コネクタ ドライバーで内部の PD/Type-C 状態を保持しておく必要はありません。 USB Type-C コネクタと USB 電源供給 (PD) ステート マシンの複雑な管理はシステムによって処理されます。 必要なのは、クラス拡張機能を介してハードウェアのイベントをシステムに通信するクライアント ドライバーを作成することだけです。 詳しくは、[USB Type-C コントローラー インターフェイスのドライバー クラス拡張機能のリファレンス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt805826(v=vs.85))をご覧ください。

## <a name="whats-new-in-windows-10-version-1607"></a>Windows 10 バージョン 1607 の新着情報

[ページのトップへ](#top)

このセクションでは、Windows 10 Version 1607 でのドライバー開発に関する新機能と強化された機能について説明します。

### <a name="audio-1607"></a>オーディオ

Windows 10 Version 1607 では、Windows オーディオ ドライバーの開発に関する次のトピックが新たに追加されました。

* [Windows オーディオ アーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/audio/windows-audio-architecture)
* Cortana エクスペリエンスのサポートを強化する構造体とプロパティ:
  * [**KSPROPERTY\_AUDIO\_MIC\_SENSITIVITY**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-mic-sensitivity)
  * [**KSPROPERTY\_AUDIO\_MIC\_SNR**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-mic-snr)
  * [**KSAUDIO\_PACKETSIZE\_CONSTRAINTS2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints2)
* [PKEY\_AudioEndpoint\_Default\_VolumeInDb](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-audioendpoint-default-volumeindb) &ndash; オーディオ信号に適切な増幅または減衰が適用されたときにより良いユーザー エクスペリエンスを提供する INF キー。

### <a name="camera-1607"></a>カメラ

Windows 10 Version 1607 では、Windows Hello と顔認証をサポートするために、カメラ ドライバーの開発に関するトピックが追加および更新されています。

* [Windows Hello カメラ ドライバー構築ガイド](https://docs.microsoft.com/windows-hardware/drivers/stream/windows-hello-camera-driver-bring-up-guide)
* [拡張カメラ コントロール](https://docs.microsoft.com/windows-hardware/drivers/stream/standardized-extended-controls-)
* [**KSPROPERTY\_CAMERACONTROL\_EXTENDED\_FACEAUTH\_MODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-faceauth-mode)

### <a name="location-1607"></a>位置情報

Windows 10 Version 1607 では、ロケーション ドライバーの開発に関する次の GNSS Breadcrumb DDI が新たに追加されています。

* [**GNSS\_BREADCRUMB\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ns-gnssdriver-gnss_breadcrumb_list)
* [**GNSS\_BREADCRUMB\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ns-gnssdriver-gnss_breadcrumb_v1)
* [**GNSS\_BREADCRUMBING\_ALERT\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ns-gnssdriver-gnss_breadcrumbing_alert_data)
* [**GNSS\_BREADCRUMBING\_PARAM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ns-gnssdriver-gnss_breadcrumbing_param)
* [**IOCTL\_GNSS\_LISTEN\_BREADCRUMBING\_ALERT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_listen_breadcrumbing_alert)
* [**IOCTL\_GNSS\_POP\_BREADCRUMBS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_pop_breadcrumbs)
* [**IOCTL\_GNSS\_START\_BREADCRUMBING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_start_breadcrumbing)
* [**IOCTL\_GNSS\_STOP\_BREADCRUMBING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gnssdriver/ni-gnssdriver-ioctl_gnss_stop_breadcrumbing)

### <a name="print-1607"></a>印刷

Windows 10 Version 1607 でのプリンター ドライバー開発には、コマンド ライン ツールの [JSConstraintsDebug](https://docs.microsoft.com/windows-hardware/drivers/devtest/jsconstraintsdebug) が含まれています。これにより、V4 プリンター ドライバー開発時の JavaScript 制限のデバッグがサポートされます。

### <a name="wlan-1607"></a>WLAN

Windows 10 Version 1607 では、WLAN デバイス ドライバー インターフェイス (WDI) バージョン 1.0.21 に関するトピックが追加および更新されています。 詳しくは、[WDI ドキュメントの変更履歴](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-doc-change-history)をご覧ください。

## <a name="whats-new-in-windows-10-version-1507"></a>Windows 10 バージョン 1507 の最新情報

[ページのトップへ](#top)

このセクションでは、Windows 10 でのドライバー開発に関する新機能と更新された機能について説明します。

### <a name="bluetooth-1507"></a>Bluetooth

Windows 10 では、[Microsoft が定義した Bluetooth HCI 拡張機能](https://docs.microsoft.com/windows-hardware/drivers/bluetooth/microsoft-defined-bluetooth-hci-commands-and-events)が新しく追加されています。

### <a name="buses-and-ports"></a>バスとポート

OneCoreUAP ベースの Windows エディションには、SPB (Simple Peripheral Bus) 用のドライバー プログラミング インターフェイスとインボックス ドライバー (I2C、SPI、GPIO など) が含まれています。 これらのドライバーは、Windows 10 デスクトップ エディションと Windows 10 Mobile の両方、およびその他のバージョンの Windows 10 で実行されます。

### <a name="camera-1507"></a>カメラ

カメラ ドライバーの DDI は、新しい[カメラ DDI](https://docs.microsoft.com/windows-hardware/drivers/stream/windows-10-technical-preview-camera-drivers-reference) を含むユニバーサル Windows ドライバー モデルに収束されました。 次のような追加機能も含まれています。

* [デジタル ビデオ手ブレ補正](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-videostabilization)
* [可変フレーム レート](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-vfr)
* [顔検出](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-facedetection)
* [ハイ ダイナミック レンジ (HDR) ビデオ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-videohdr)
* [光学式手ブレ補正](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-ois)
* [シーン分析: HDR 写真、フラッシュ/フラッシュなし、超ローライト](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-advancedphoto)
* [統計情報のキャプチャ: メタデータ フレームワーク/属性、ヒストグラム](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-histogram)
* [スムーズ ズーム](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-zoom)
* [ハードウェア最適化のヒント](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-optimizationhint-)
* [カメラ プロファイル](https://docs.microsoft.com/windows-hardware/drivers/stream/camera-driver-functions)

### <a name="cellular"></a>Cellular

Windows 10 の[携帯電話のアーキテクチャと実装](https://docs.microsoft.com/windows-hardware/drivers/network/cellular-architecture-and-driver-model)が更新されました。

### <a name="display-1507"></a>ディスプレイ

Windows 8.1 と Windows Phone の[ディスプレイ ドライバー モデル](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_display/)は、Windows 10 の統一モデルに収束されました。

各 GPU にプロセスごとに仮想アドレス空間を割り当てる新しいメモリ モデルが実装されています。 WDDMv2 では、ビデオ メモリの直接アドレス指定も引き続きサポートされ、それを必要とするグラフィックス ハードウェアに対応していますが、これはレガシ ケースと見なされます。 IHV は、仮想アドレス指定をサポートする新しいハードウェアを開発する必要があります。 この新しいメモリ モデルを有効にするために、DDI に対して大きな変更が加えられています。

### <a name="human-interface-device"></a>ヒューマン インターフェイス デバイス (HID)

新しい仮想 HID フレームワーク (VHF) により、カーネルモード トランスポート ミニドライバーを作成する必要がなくなりました。 このフレームワークは、ドライバーで使用されるプログラミング要素を公開するための、Microsoft が提供する静的ライブラリ (Vhfkm.lib) で構成されます。 また、1 つまたは複数の子デバイスを列挙し、仮想の[ヒューマン インターフェイス デバイス](https://docs.microsoft.com/windows-hardware/drivers/hid/) (HID) ツリーを構築する、Microsoft が提供するインボックス ドライバー (Vhf.sys) も含まれています。

* [仮想 HID フレームワーク (VHF) を使って HID ソース ドライバーを作成する](https://docs.microsoft.com/windows-hardware/drivers/hid/virtual-hid-framework--vhf-)
* [仮想 HID フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/vhf/)

### <a name="location-1507"></a>位置情報

全地球航法衛星システム (GNSS) ドライバーの DDI は、[GNSS ユニバーサル Windows ドライバー モデル](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_gnss/) (UMDF 2.0) に収束されました。

### <a name="near-field-communication"></a>近距離無線通信 (NFC)

[NFC DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_nfpdrivers/) は、モバイルおよびデスクトップのソリューションをサポートする新しいドライバー モデルに収束されました。

[NFC クラス拡張機能](https://docs.microsoft.com/windows-hardware/drivers/nfc/nfc-class-extension-):新しい NFC クラス拡張機能ドライバーを利用できます。 NFC クラス拡張機能ドライバーは、NFC コントローラー、セキュリティで保護された要素、およびリモート RF エンドポイントと対話するために、Windows 定義のすべての DDI を実装します。

### <a name="networking-1507"></a>ネットワーク

新しい [PacketDirect プロバイダー インターフェイス (PDPI)](https://docs.microsoft.com/windows-hardware/drivers/network/introduction-to-ndis-pdpi) は、既存の NDIS ミニポート ドライバー モデルの拡張機能として利用できます。 PDPI は、アプリケーションが独自のバッファーの管理、プロセッサのポーリング、ミニポート アダプターでのパケット送受信の直接管理を行うための I/O モデルを提供します。 これらの機能の組み合わせにより、アプリケーションは自身のコンテキストを全面的に制御し、はるかに高いパケット/秒 (pps) レートを実現できます。

### <a name="print-1507"></a>印刷

プリンター ドライバーの更新では、v4 プリンター ドライバーの機能強化と変更が行われ、モバイル デバイスからのワイヤレス印刷がサポートされるようになりました。また、次の点も強化されています。

* [V4 ドライバー マニフェスト](https://docs.microsoft.com/windows-hardware/drivers/print/v4-driver-manifest) &ndash; PWG ラスター レンダリング フィルターをサポートするための v4 プリンター ドライバー マニフェストの変更 (更新された DriverConfig ディレクティブと DriverRender ディレクティブを含む) と、更新されたサンプル マニフェストに関する情報を提供します。
* [WS-Discovery のモバイル印刷のサポート](https://docs.microsoft.com/windows-hardware/drivers/print/ws-discovery-mobile-printing-support) &ndash; Windows 10 Mobile デバイスから Windows 10 Mobile と互換性のあるプリンターへのモバイル印刷を可能にするための WS-Discovery の要件について説明します。
* [**IXpsRasterizationFactory2 インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/xpsrassvc/nn-xpsrassvc-ixpsrasterizationfactory2) &ndash; XPS ラスタライズ サービスを使った XPS から PWG ラスターへのプリンター コンテンツの変換をサポートします。 PWG ラスターは非正方形の DPI をサポートします。
* [**印刷パイプラインのプロパティ バッグ**](https://docs.microsoft.com/windows-hardware/drivers/print/print-pipeline-property-bag) &ndash; 新しい PrintDeviceCapabilities プロパティにより、XPS レンダリング フィルターが印刷フィルター パイプラインのプロパティ バッグから新しい PrintDeviceCapabilities XML ファイルを取得できるようになりました。
* [GetWithArgument の要求と応答のスキーマ](https://docs.microsoft.com/windows-hardware/drivers/print/getwithargument-request-and-response-schemas) &ndash; GetWithArgument の要求と応答の双方向通信スキーマの正式な定義と例を使ったモバイル印刷のサポートを提供します。
* [**IBidiSpl::SendRecv メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bidispl/nf-bidispl-ibidispl-sendrecv) &ndash; GetWithArgument 双方向スキーマの値を使ったモバイル印刷のサポートを追加します。

### <a name="smart-card"></a>スマート カード

Windows 10 には、複雑なドライバー操作を処理する新しいクラス拡張モジュール Wudfsmcclassext.dll が含まれています。 スマート カード ハードウェアに固有のタスクは、クライアント ドライバーによって処理されます。 クライアント ドライバーが要求を処理できるように、カードに関する情報をクラス拡張機能に送信するための新しいプログラミング インターフェイスがあります。 これらのドライバー プログラミング インターフェイスは、OneCoreUAP ベースの Windows エディションに含まれています。

* [スマート カード クライアント ドライバーのイベント コールバック関数](https://docs.microsoft.com/previous-versions/dn946583(v=vs.85))
* [スマート カード クライアント ドライバーのサポート メソッド](https://docs.microsoft.com/previous-versions/dn946584(v=vs.85))

### <a name="storage-1507"></a>ストレージ

Windows 10 では、アプリがネイティブのデバイス プロトコルを使用してストレージ デバイスと通信できるように、新しいプロトコル固有のインターフェイスが追加されました。 これらの更新には、次のものが含まれます。

* ストレージ プロトコルのパススルー &ndash; 更新されたストレージ パススルー IOCTL インターフェイスで、NVMe (non-volatile memory express) を含む新しいプロトコルがサポートされます。
* 拡張ストレージ クエリ インターフェイス &ndash; 拡張されたストレージ クエリ インターフェイスにより、アプリケーションがプロトコル依存の情報を照会できるようになります。

### <a name="system-supplied-driver-interfaces"></a>システム提供のドライバー インターフェイス

[GUID\_DEVICE\_RESET\_INTERFACE\_STANDARD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_reset_interface_standard) インターフェイスは、正常に機能しないデバイスのリセットと復旧をファンクション ドライバーが試行するための標準的な方法を定義します。

### <a name="usb-1507"></a>USB

Windows 10 の USB には次の新機能があります。 詳しくは、「[Windows 10:What's new for USB (Windows 10: USB の新機能)](https://docs.microsoft.com/windows-hardware/drivers/usbcon/windows-10--what-s-new-for-usb)」をご覧ください。

* USB 3.1 仕様の定義に従った USB Type-C のネイティブ サポート。 USB Type-C コネクタを使用するシステムを構築する場合は、インボックスの [USB Type-C コネクタ システム ソフトウェア インターフェイス (UCSI) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/ucsi)を使用するか、[USB Type-C コネクタ ドライバーを作成](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)することができます。
* デュアル ロール機能により、スマートフォン、ファブレット、タブレットなどのモバイル デバイスが、自身を "*デバイス*" または "*ホスト*" として指定することができます。 詳しくは、「[USB Dual Role Driver Stack Architecture (USB デュアル ロール ドライバー スタック アーキテクチャ)](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-dual-role-driver-stack-architecture)」をご覧ください。
* [Microsoft が提供する USB デバイス エミュレーション クラス拡張機能 (UdeCx)](https://docs.microsoft.com/windows-hardware/drivers/usbcon/system-supplied-usb-drivers) の使用による USB エミュレート デバイス用のドライバー作成のサポート。
* XHCI の仕様に準拠していないホスト コントローラーまたは仮想ホスト コントローラー用のドライバー作成のサポート。 このようなドライバーを作成する方法については、「[Developing Windows drivers for USB host controllers (USB ホスト コントローラー用 Windows ドライバーの作成)](https://docs.microsoft.com/windows-hardware/drivers/usbcon/developing-windows-drivers-for-usb-host-controllers)」をご覧ください。
* USB ファンクション クラス拡張機能 (UFX) の使用によるファンクション コントローラー ドライバー作成のサポート。 「[Developing Windows drivers for USB function controllers (USB ファンクション コントローラー用の Windows ドライバーの開発)](https://docs.microsoft.com/windows-hardware/drivers/usbcon/developing-windows-drivers-for-usb-function-controllers)」をご覧ください。

### <a name="wlan-1507"></a>WLAN

WDI (WLAN デバイス ドライバー インターフェイス) は、Windows 10 デスクトップ エディションと Windows 10 Mobile の WLAN ドライバーを収束する新しい [WLAN ユニバーサル Windows ドライバー モデル](https://docs.microsoft.com/windows-hardware/drivers/network/wifi-universal-driver-model)です。

[ページのトップへ](#top)

## <a name="deprecated-features"></a>推奨されなくなった機能

次の表では、Windows 10 で削除された Windows ドライバー開発の機能について説明します。

| ドライバーのテクノロジ | 機能 | 非推奨になったバージョン |
|---|---|---|
| GNSS/位置情報 | [Windows 8.1 用の位置情報ドライバー サンプル](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)とその関連ドキュメント | Windows 10 バージョン 1709 |
| 通信事業者のシナリオ (ネットワーク) | [AllowStandardUserPinUnlock](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/allowstandarduserpinunlock) | Windows 10 バージョン 1709 |
| スキャン/イメージ | [WSD (Web Services for Devices) Challenger](https://docs.microsoft.com/windows-hardware/drivers/image/challenging-a-disconnected-scanner-with-the-wsd-challenger) 機能とその関連ドキュメント | Windows 10 バージョン 1709 |
|通信事業者| Sysdev メタデータ パッケージを使ったモバイル ブロードバンド アプリ エクスペリエンスのアプリは非推奨になりました。代わりに MO UWP APPS と COSA が推奨されます。 | Windows 10 バージョン 1803|
