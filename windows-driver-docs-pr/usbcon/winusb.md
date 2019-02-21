---
Description: This section describes the generic WinUSB driver (Winusb.sys) and its user-mode component (Winusb.dll) provided by Microsoft for all USB devices.
title: WinUSB (Winusb.sys)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c5d624fc901e7b8a587b123590fc58aa75b89c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529289"
---
# <a name="winusb-winusbsys"></a>WinUSB (Winusb.sys)


このセクションでは、汎用 WinUSB ドライバー (Winusb.sys) とすべての USB デバイスに Microsoft によって提供される、ユーザー モード コンポーネント (Winusb.dll) について説明します。

Windows XP Service Pack 2 (SP2) より前のバージョンの Windows ですべての USB デバイス ドライバーはカーネル モードで動作する必要があります。 オペレーティング システムがネイティブ クラス ドライバーをいない USB デバイスを作成する場合は、デバイスのカーネル モード デバイス ドライバーを作成する必要があります。

Windows USB (WinUSB) は、Windows XP SP2 の Windows Driver Frameworks (WDF) と同時に開発された USB デバイスの一般的なドライバーです。 WinUSB アーキテクチャは、カーネル モード ドライバー (Winusb.sys) および公開するユーザー モード ダイナミック リンク ライブラリ (Winusb.dll) [WinUSB functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)します。 これらの関数を使用すると、ユーザー モード ソフトウェアでの USB デバイスを管理できます。

Winusb.sys が UMDF 関数のドライバーと関連付けられているデバイスの間のリンクの重要な部分もあります。 Winusb.sys は、デバイスのカーネル モード スタックの上位のフィルター ドライバーとしてインストールされます。 アプリケーションは、読み取り、書き込み、またはデバイスの I/O 制御要求を発行するため、デバイスの UMDF 関数ドライバーと通信します。 ドライバー、フレームワークは、Winusb.sys に要求を渡しますとやり取りします。 Winusb.sys は、要求を処理し、プロトコル ドライバーに渡され、最終的には、デバイスにします。 逆方向のパス、すべての応答を返します。 Winusb.sys は、デバイス スタックのプラグ アンド プレイと電源の所有者としても機能します。

**注**  WinUSB 関数に必要な Windows XP またはそれ以降。 USB デバイスとの通信に、C/C++ アプリケーションでこれらの関数を使用できます。 Microsoft では、WinUSB のマネージ API は提供されません。

このセクションでは、WinUSB を使用して、USB デバイスと通信する方法について説明します。 このセクションのトピックでは、USB デバイスの機能のドライバーとを示すコード例の詳細なチュートリアルとして Winusb.sys のインストールについては、デバイスの適切なドライバーの選択に関するガイドラインを提供する方法のアプリケーションと USB デバイス互いと通信します。

ここでは、次のトピックについて説明します。

-   [WinUSB アーキテクチャとモジュール](winusb-architecture.md)
-   [WinUSB (Winusb.sys) のインストール](winusb-installation.md)
-   [WinUSB デバイス](automatic-installation-of-winusb.md)
-   [WinUSB 関数を使用して、USB デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md)
-   [ポリシーの変更をパイプ WinUSB 関数](winusb-functions-for-pipe-policy-modification.md)
-   [WinUSB 電源管理](winusb-power-management.md)

## <a name="windows-support-for-winusb"></a>WinUSB の Windows のサポート


次の表は、異なるバージョンの Windows で WinUSB サポートをまとめたものです。

| Windows のバージョン      | WinUSB サポート |
|----------------------|----------------|
| Windows 10 以降 | Yes²           |
| Windows 7            | Yes¹           |
| Windows Server 2008  | Yes²           |
| Windows Vista        | Yes²           |
| Windows Server 2003  | X             |
| Windows XP           | Yes³           |
| Windows 2000         | X             |

 

**注**   Yes¹:このバージョンの Windows サポート WinUSB x86 ベース、x64 ベースおよび Itanium ベース システム上のすべての Sku。

Yes²:このバージョンの Windows サポート WinUSB x86 ベースおよび x64 ベースのシステム上のすべての Sku。

Yes³:すべてのクライアント Sku の Windows XP SP2 サービス パックではサポート WinUSB です。 WinUSB は Windows XP; にネイティブではありません。WinUSB 共同インストーラーによるインストールがあります。

違います：WinUSB はこのバージョンの Windows でサポートされていません。

 

## <a name="usb-features-supported-by-winusb"></a>WinUSB でサポートされている USB 機能


WinUSB で異なるバージョンの Windows でサポートされている高度な USB 機能を次の表に示します。

| 機能                                | Windows 8.1 以降 | Windows 7/Vista/XP |
|----------------------------------------|-----------------------|--------------------|
| デバイス I/O 制御要求            | サポート対象             | サポート対象          |
| アイソクロナス転送                  | サポート対象             | サポートされない      |
| 一括、制御、および割り込みの転送 | サポート対象             | サポート対象          |
| セレクティブ サスペンドします。                      | サポート対象             | サポート対象          |
| リモート ウェイク                            | サポート対象             | サポート対象          |

 

## <a name="related-topics"></a>関連トピック
[Microsoft 提供の USB ドライバー](system-supplied-usb-drivers.md)  



