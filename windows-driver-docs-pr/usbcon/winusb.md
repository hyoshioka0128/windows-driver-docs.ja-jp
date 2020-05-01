---
Description: このセクションでは、すべての USB デバイス用に Microsoft が提供する汎用 WinUSB ドライバー (Winusb.sys) とそのユーザーモード コンポーネント (Winusb.dll) について説明します。
title: WinUSB (Winusb.sys)
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 420c7656d81c1849bb51237cab2d700f65950a8c
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "72007619"
---
# <a name="winusb-winusbsys"></a>WinUSB (Winusb.sys)


このセクションでは、すべての USB デバイス用に Microsoft が提供する汎用 WinUSB ドライバー (Winusb.sys) とそのユーザーモード コンポーネント (Winusb.dll) について説明します。

Windows XP with Service Pack 2 (SP2) より前のバージョンの Windows では、すべての USB デバイス ドライバーはカーネル モードで動作する必要がありました。 オペレーティング システムにネイティブ クラス ドライバーがない USB デバイスを作成した場合は、デバイス用のカーネル モード デバイス ドライバーを作成する必要がありました。

Windows USB (WinUSB) は、Windows XP with SP2 用の Windows Driver Frameworks (WDF) と同時に開発された USB デバイス用の汎用ドライバーです。 WinUSB アーキテクチャは、カーネル モード ドライバー (Winusb.sys) と、[WinUSB 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)を公開するユーザー モード ダイナミック リンク ライブラリ (Winusb.dll) で構成されています。 これらの関数を使用して、ユーザー モード ソフトウェアで USB デバイスを管理できます。

また、Winusb.sys は UMDF 関数ドライバー、および関連付けられているデバイスとの間のリンクにおける重要な部分です。 Winusb.sys は、上位フィルター ドライバーとしてデバイスのカーネル モード スタックにインストールされます。 アプリケーションでは、デバイスの UMDF 関数ドライバーとの通信が行われ、読み取り、書き込み、またはデバイスの I/O 制御要求が発行されます。 ドライバーは、要求を Winusb.sys に渡すフレームワークと連携します。 Winusb.sys では要求が処理され、要求はプロトコル ドライバー、そして最終的にはデバイスに渡されます。 すべての応答は、リバース パスによって返されます。 Winusb.sys は、デバイス スタックのプラグ アンド プレイ、および電源管理者としても機能します。

**注**  WinUSB 関数には、Windows XP 以降が必要です。 これらの関数を C/C++ アプリケーションで使用して、USB デバイスと通信することができます。 Microsoft は WinUSB 用のマネージ API を提供していません。

このセクションでは、WinUSB を使用して USB デバイスと通信する方法について説明します。 このセクションのトピックでは、デバイスの適切なドライバーを選択するためのガイドライン、Winusb.sys を USB デバイスの関数ドライバーとしてインストールする方法、およびアプリケーションと USB デバイスが相互に通信する方法を示す、コード例付きの詳細なチュートリアルを提供します。

このセクションには、次のトピックがあります。

-   [WinUSB アーキテクチャとモジュール](winusb-architecture.md)
-   [WinUSB (Winusb.sys) のインストール](winusb-installation.md)
-   [WinUSB デバイス](automatic-installation-of-winusb.md)
-   [WinUSB 関数を使用して USB デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md)
-   [パイプ ポリシー修正のための WinUSB 関数](winusb-functions-for-pipe-policy-modification.md)
-   [WinUSB 電源管理](winusb-power-management.md)

## <a name="windows-support-for-winusb"></a>WinUSB の Windows サポート


次の表は、さまざまなバージョンの Windows における WinUSB のサポートをまとめたものです。

| Windows のバージョン      | WinUSB サポート |
|----------------------|----------------|
| Windows 10 以降 | はい²           |
| Windows 7            | はい¹           |
| Windows Server 2008  | はい²           |
| Windows Vista        | はい²           |
| Windows Server 2003  | いいえ             |
| Windows XP           | はい³           |
| Windows 2000         | いいえ             |

 

**注**   はい¹:このバージョンの Windows のすべての SKU では、x86 ベース、x64 ベース、および Itanium ベースのシステムで WinUSB がサポートされています。

はい²:このバージョンの Windows のすべての SKU では、x86 ベース、および x64 ベースのシステムで WinUSB がサポートされています。

はい³:Windows XP with SP2 サービス パックのすべてのクライアント SKU で WinUSB がサポートされています。 WinUSB は Windows XP にネイティブではありません。そのため、WinUSB 共同インストーラーを使用してインストールする必要があります。

いいえ:WinUSB は、このバージョンの Windows ではサポートされていません。

 

## <a name="usb-features-supported-by-winusb"></a>WinUSB でサポートされる USB 機能


次の表は、さまざまなバージョンの Windows の WinUSB でサポートされている上位レベルの USB 機能を示しています。

| 機能                                | Windows 8.1 以降 | Windows 7/Vista/XP |
|----------------------------------------|-----------------------|--------------------|
| デバイス I/O の制御要求            | サポート             | サポート          |
| 等時性転送                  | サポート             | サポートしていません。      |
| 一括転送、制御転送、割り込み転送 | サポート             | サポート          |
| セレクティブ サスペンド                      | サポート             | サポート          |
| リモート スリープ解除                            | サポート             | サポート          |

 

## <a name="related-topics"></a>関連トピック
[Microsoft が提供する USB ドライバー](system-supplied-usb-drivers.md)  



