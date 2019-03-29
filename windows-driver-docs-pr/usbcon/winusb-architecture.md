---
Description: WinUSB consists of two primary components - Winusb.sys, a kernel-mode driver and Winusb.dll - user-mode DLL.
title: WinUSB アーキテクチャとモジュール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8af8e1ac30fd4585ee25864ed38080d3a4cc6fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580682"
---
# <a name="winusb-architecture-and-modules"></a>WinUSB アーキテクチャとモジュール


[WinUSB](winusb.md)の 2 つの主要なコンポーネントで構成されます。

-   Winusb.sys は、USB デバイスのカーネル モード デバイス スタックでプロトコル ドライバーの上のフィルターまたは関数のいずれかのドライバーとしてインストール可能なカーネル モード ドライバーです。
-   Winusb.dll が公開しているユーザー モード DLL [WinUSB functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)します。 アプリケーションでは、デバイスの機能のドライバーとしてインストールされているときに、Winusb.sys との通信にこれらの関数を使用できます。

デバイスのユーザー定義関数のドライバーを必要としない場合、機能のドライバーとして Winusb.sys デバイスのカーネル モード スタックでインストールできます。 ユーザー モード デバイス I/O 制御要求のセットを使用して、または呼び出すことによって、プロセスは Winusb.sys と通信し、できる[WinUSB functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)します。

次の図には、Winusb.sys のいくつかのインスタンスを含む USB ドライバー スタックが表示されます。

![winusb ドライバーとデバイス オブジェクトのスタック](images/winusb-architecture.png)

上記の図は、WinUSB 構成の例を次の 3 つのデバイスのインターフェイス クラスを実装する 1 つの登録済みデバイスのインターフェイスを持つを示しています。

-   Winusb.sys のインスタンス 1 では、デバイス インターフェイス A は、ユーザー モード ドライバー (Usboem.dll) のサポートを登録します。
-   Winusb.sys のインスタンス 2 では、システム サービス (SVCHOST) を使用する Winusb.dll と通信するスキャナー (Usbscan.exe) のユーザー モード ドライバーをサポートするデバイス インターフェイス B を登録します。
-   Winusb.sys のインスタンス 3 は、デバイス インターフェイス C は、ファームウェアの更新プログラム ユーティリティ (Usbfw.exe) のサポートを登録します。

Winusb.sys の 1 つだけの読み込まれたインスタンスがあります。 インターフェイスまたは複合デバイス (たとえば、インスタンス 2 および 3) のインターフェイスのコレクションを表すことがまたは PDO が非複合デバイス (たとえば、図にインスタンス 1) を表すことができます。 USB ワイヤレス モバイル通信デバイス クラス (WMCDC) のデバイスの PDO はもいくつかのインターフェイスのコレクションを表すことができます。 (WMCDC デバイス用 Pdo の詳細については、次を参照してください[ワイヤレス モバイル通信デバイス クラスに対するサポート](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)。)。

任意のユーザー モード アプリケーションは、WinUSB ダイナミック リンク ライブラリ (Winusb.dll) の読み込みと、このモジュールによって公開されている WinUSB 関数を呼び出すことによって、USB スタックと通信できます。

## <a name="related-topics"></a>関連トピック
[WinUSB (winusb.sys) のインストール](winusb-installation.md)  
[WinUSB 関数を使用して、USB デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md)  
[ポリシーの変更をパイプ WinUSB 関数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 電源管理](winusb-power-management.md)  
[WinUSB 関数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)  
[WinUSB](winusb.md)  



