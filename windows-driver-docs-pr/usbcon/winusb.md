---
Description: ここでは、すべての USB デバイス用に Microsoft が提供する汎用 WinUSB ドライバー (Winusb .sys) とそのユーザーモードコンポーネント (Winusb .dll) について説明します。
title: WinUSB (Winusb.sys)
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 420c7656d81c1849bb51237cab2d700f65950a8c
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007619"
---
# <a name="winusb-winusbsys"></a>WinUSB (Winusb.sys)


ここでは、すべての USB デバイス用に Microsoft が提供する汎用 WinUSB ドライバー (Winusb .sys) とそのユーザーモードコンポーネント (Winusb .dll) について説明します。

Windows XP Service Pack 2 (SP2) より前のバージョンの Windows では、すべての USB デバイスドライバーがカーネルモードで動作する必要がありました。 オペレーティングシステムにネイティブクラスドライバーがない USB デバイスを作成した場合は、デバイス用のカーネルモードデバイスドライバーを作成する必要がありました。

Windows USB (WinUSB) は、windows XP SP2 用の Windows ドライバーフレームワーク (WDF) と同時に開発された USB デバイス用の汎用ドライバーです。 WinUSB アーキテクチャは、 [winusb 機能](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)を公開するカーネルモードドライバー (winusb .sys) とユーザーモードダイナミックリンクライブラリ (winusb .dll) で構成されています。 これらの機能を使用して、ユーザーモードソフトウェアで USB デバイスを管理できます。

また、このコンポーネントは、UMDF 関数ドライバーと関連付けられているデバイスとの間のリンクの重要な部分です。 Winusb .sys は、上位フィルタードライバーとしてデバイスのカーネルモードスタックにインストールされます。 アプリケーションは、デバイスの UMDF 関数ドライバーと通信して、読み取り、書き込み、またはデバイスの i/o 制御要求を発行します。 ドライバーは、要求を Winusb .sys に渡すフレームワークと対話します。 次に、要求を処理し、プロトコルドライバーと最終的にデバイスに渡します。 すべての応答は、逆パスによって返されます。 Winusb .sys は、デバイススタックのプラグアンドプレイと電源所有者としても機能します。

**注**  WinUSB 関数には、Windows XP 以降が必要です。 これらの関数を C/C++ アプリケーションで使用して、USB デバイスと通信することができます。 Microsoft は WinUSB 用のマネージ API を提供していません。

このセクションでは、WinUSB を使用して USB デバイスと通信する方法について説明します。 このセクションのトピックでは、デバイスに適切なドライバーを選択するためのガイドライン、USB デバイスの機能ドライバーとしての Winusb のインストールに関する情報、およびアプリケーションと USB デバイスのしくみを示すコード例を使用した詳細なチュートリアルについて説明します。相互に通信します。

ここでは、次のトピックについて説明します。

-   [WinUSB アーキテクチャとモジュール](winusb-architecture.md)
-   [WinUSB (Winusb.sys) のインストール](winusb-installation.md)
-   [WinUSB デバイス](automatic-installation-of-winusb.md)
-   [WinUSB 機能を使用して USB デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md)
-   [パイプ ポリシー修正のための WinUSB 関数](winusb-functions-for-pipe-policy-modification.md)
-   [WinUSB 電源管理](winusb-power-management.md)

## <a name="windows-support-for-winusb"></a>WinUSB の Windows サポート


次の表は、さまざまなバージョンの Windows での WinUSB のサポートをまとめたものです。

| Windows のバージョン      | WinUSB サポート |
|----------------------|----------------|
| Windows 10 以降 | ○²           |
| Windows 7            | はい¹           |
| Windows Server 2008  | ○²           |
| Windows Vista        | ○²           |
| Windows Server 2003  | X             |
| Windows XP           | はい³           |
| Windows 2000         | X             |

 

**注**   はい¹: このバージョンの Windows のすべての sku は、x86 ベース、x64 ベース、および Itanium ベースのシステムで winusb をサポートしています。

○²: このバージョンの Windows のすべての Sku は、x86 ベースおよび x64 ベースのシステムで WinUSB をサポートしています。

はい³: Windows XP SP2 service pack のすべてのクライアント Sku で WinUSB がサポートされています。 WinUSB は Windows XP にネイティブではありません。WinUSB 共同インストーラーと共にインストールする必要があります。

いいえ: WinUSB は、このバージョンの Windows ではサポートされていません。

 

## <a name="usb-features-supported-by-winusb"></a>WinUSB でサポートされる USB 機能


次の表は、さまざまなバージョンの Windows で WinUSB でサポートされている高レベルの USB 機能を示しています。

| 機能                                | Windows 8.1 以降 | Windows 7/Vista/XP |
|----------------------------------------|-----------------------|--------------------|
| デバイス i/o 制御要求            | サポート対象             | サポート対象          |
| アイソクロナス転送                  | サポート対象             | サポートされない      |
| 一括転送、制御転送、割り込み転送 | サポート対象             | サポート対象          |
| 選択的中断                      | サポート対象             | サポート対象          |
| リモートウェイク                            | サポート対象             | サポート対象          |

 

## <a name="related-topics"></a>関連トピック
[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  



