---
Description: WinUSB - Winusb.sys、カーネル モード ドライバーおよび Winusb.dll - ユーザー モード DLL の 2 つの主要コンポーネントで構成されます。
title: WinUSB アーキテクチャとモジュール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcf343743493aa12fe9d8c843b2ed322b9e8091c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385691"
---
# <a name="winusb-architecture-and-modules"></a>WinUSB アーキテクチャとモジュール


[WinUSB](winusb.md)の 2 つの主要なコンポーネントで構成されます。

-   Winusb.sys は、USB デバイスのカーネル モード デバイス スタックでプロトコル ドライバーの上のフィルターまたは関数のいずれかのドライバーとしてインストール可能なカーネル モード ドライバーです。
-   Winusb.dll が公開しているユーザー モード DLL [WinUSB functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)します。 アプリケーションでは、デバイスの機能のドライバーとしてインストールされているときに、Winusb.sys との通信にこれらの関数を使用できます。

デバイスのユーザー定義関数のドライバーを必要としない場合、機能のドライバーとして Winusb.sys デバイスのカーネル モード スタックでインストールできます。 ユーザー モード デバイス I/O 制御要求のセットを使用して、または呼び出すことによって、プロセスは Winusb.sys と通信し、できる[WinUSB functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)します。

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
[WinUSB 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)  
[WinUSB](winusb.md)  



