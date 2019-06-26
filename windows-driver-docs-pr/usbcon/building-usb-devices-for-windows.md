---
Description: このセクションでは、USB 周辺機器の製造元からのリンクを示します。
title: Windows 用 USB デバイスの構築
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90da4770af8bfd5b97524870ee50b8b636d8b82d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384481"
---
# <a name="building-usb-devices-for-windows"></a>Windows 用 USB デバイスの構築

## <a name="summary"></a>概要

* USB デバイス ビルダー用のリソース

このセクションでは、USB 周辺機器の製造元からのリンクを示します。

## <a name="usb-device-enumeration-process"></a>USB デバイスの列挙プロセス

[USB スタックがデバイスを列挙する方法](https://go.microsoft.com/fwlink/p/?linkid=617517)  
スタックが、デバイスの存在を検出し、PnP マネージャーに新しいデバイスが到着したことを示します - Microsoft USB ドライバー スタックで使用される列挙プロセスの詳細な説明。

[USB 2.1、2.0、Windows 8 で 1.1 のデバイス列挙の変更](https://go.microsoft.com/fwlink/p/?linkid=617518)  
Windows 8 でスタックが 2.1、2.0、および 1.1 の USB デバイスを列挙する方法の USB ドライバー スタックでの変更を行いましたしました。 これらの変更は、USB の新機能をサポートし、デバイス列挙のパフォーマンスを向上させます。 読み取り、投稿は、それらのわずかな変更を認識してもらうと、簡単に列挙体のエラーの根本原因を特定する/デバイスのファームウェア ビルダーを有効にするのには。

## <a name="microsoft-os-descriptors"></a>Microsoft OS ディスクリプター

USB デバイスは、デバイス、インターフェイス、およびエンドポイントのファームウェアに標準の記述子を格納します。 さらに、デバイスでは、クラスとベンダー固有の記述子を格納できます。 ただし、これらの記述子を格納できる情報の種類が制限されています。 Ihv 通常必要がありますを使用して、Windows Update またはメディア Cd など、ユーザーにさまざまな画像、アイコン、およびカスタム ドライバーなどのデバイスに固有の情報を提供します。

IHV は、個別に提供することではなくファームウェアで情報を格納するのに Microsoft OS ディスクリプターを使用できます。 ウィンドウでは、Microsoft OS ディスクリプターを読み取り、その情報を取得し、使用してインストールし、ユーザーの介入を必要とせず、デバイスの構成をします。 参照してください[USB デバイスの Microsoft OS ディスクリプター](microsoft-defined-usb-descriptors.md)します。

[Microsoft OS 1.0 記述子の仕様](https://go.microsoft.com/fwlink/p/?linkid=617519)  
このドキュメントでは、Microsoft OS ディスクリプターを紹介します。 これには、OS 文字列記述子は、拡張プロパティ OS 機能の記述子、および OS 機能記述子の形式の仕様が含まれます。

[Microsoft OS 2.0 記述子の仕様](https://go.microsoft.com/fwlink/p/?linkid=306681)  
このドキュメントを定義し、Microsoft OS ディスクリプターのバージョン 2.0 の実装について説明します。 Microsoft OS 2.0 記述子の目標は、制限事項と OS ディスクリプター version 1.0 での信頼性の問題に対処し、USB デバイスの新しい Windows 固有の機能を有効にすること。

[Microsoft OS ディスクリプターを使用して、関数のドライバーとして Winusb.sys の読み込み](automatic-installation-of-winusb.md)  
IHV は、"WINUSB"として特定の Microsoft オペレーティング システム (OS) 機能の記述子をレポートの互換性のある ID を定義できます。 これらの記述子は、カスタムの INF ファイルを使用せず、デバイスの機能のドライバーとして Winusb.sys を読み込む Windows を許可します。 互換性のある ID を定義する方法の例については、拡張互換性 ID OS 機能記述子仕様の例を参照してください。 ダウンロードに仕様が含まれている[Microsoft OS 1.0 記述子仕様](https://go.microsoft.com/fwlink/p/?linkid=617519)します。

## <a name="setting-a-container-id"></a>コンテナー ID を設定

[USB デバイス用のコンテナー Id](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids-for-usb-devices)  
ユニバーサル シリアル バス (USB) デバイス用のコンテナーの Id を生成する方法について説明します。

[Windows での USB ContainerIDs](usb-containerids-in-windows.md)  
Windows で正しく検出されるように、多機能の USB デバイスをプログラミングするデバイスの製造元向けガイドライン。

[USB デバイス用のコンテナーの ID を生成する方法](https://go.microsoft.com/fwlink/p/?linkid=617520)  
ブログの投稿では、デバイスがコンテナーを報告する必要がある方法について説明します ID などの Windows を列挙し、デバイスで表示されます**デバイスとプリンター**適切です。 を複数の (複合デバイス) の機能またはコンポーネント (複合デバイス) をサポートするデバイスのデバイスは、各部分と同じ ID を報告する必要があります。 デバイスには、Microsoft OS ContainerID 記述子で ID を報告する必要があります。

## <a name="implementing-power-management"></a>電源管理の実装

[USB 3.0 のハードウェアでの電源管理をリンクします。](link-power-management-in-usb-3-0-hardware.md)  
このドキュメントでは、ハードウェア ベンダーと Oem セレクティブ サスペンドと組み合わせてリンク電源管理 (LPM) を使用して USB デバイスの電源管理を実装するためのガイドラインを提供します。 U2 に U1 からハードウェアの移行について説明し、USB コント ローラー、ハブ、およびデバイスで、LPM 実装でよくある落とし穴について説明します。

[選択的分かりやすい解説を中断](link-power-management-in-usb-3-0-hardware.md)  
このブログ投稿では、USB ドライバー スタックが関数を処理する方法について説明しますと選択的に USB 3.0 デバイスを中断します。

## <a name="debugging-and-diagnostic-tools"></a>デバッグおよび診断ツール

[Windows のイベント トレースは USB](usb-event-tracing-for-windows.md)  
Event Tracing for Windows (ETW) は、オペレーティング システムによって提供される高速な汎用トレース機能です。 ツールをインストールし、トレース ファイルを作成し、USB のトレース ファイル内のイベントを分析する方法に関する情報が含まれます。

[WPP ソフトウェア トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)  
Windows ソフトウェア トレース プリプロセッサ (WPP) の既定の操作を使用して、ソフトウェア コンポーネント (トレース プロバイダー) の操作を追跡する方法。

[USB 3.0 の拡張機能](https://docs.microsoft.com/windows-hardware/drivers/debugger/usb-3-extensions)(usb3kd.dll)  
これらのコマンドは、USB 3.0 スタック内の 3 つのドライバーによって維持されるデータ構造から情報を表示します。 USB 3.0 ハブのドライバー、USB ホスト コント ローラーの拡張機能ドライバーと、USB 3.0 ホスト コント ローラー ドライバー。

[USB 2.0 の拡張機能](https://docs.microsoft.com/windows-hardware/drivers/debugger/usb-2-0-extensions)(usb2kd.dll)  
これらのコマンドは、USB 2.0 スタックのドライバーによって管理されるデータ構造から情報を表示します。 USB 2.0 ハブのドライバーと USB 2.0 ホスト コント ローラー ドライバー。

## <a name="related-topics"></a>関連トピック

[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  
