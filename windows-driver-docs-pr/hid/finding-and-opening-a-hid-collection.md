---
title: 検索して HID コレクションを開く
description: 検索して HID コレクションを開く
ms.assetid: b46fdb06-e6ae-4376-994f-69bf6539f2ce
keywords:
- コレクション WDK の HID、検索
- HID コレクション WDK の検索
- HID コレクションの検索
- WDK を非表示、開くコレクション
- HID コレクション WDK を開く
- HID のコレクションを開く
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaba2c5dfbfac7b488103a5e1388cf424b2ecb23
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559428"
---
# <a name="finding-and-opening-a-hid-collection"></a>検索して HID コレクションを開く





このセクションでは、ユーザー モード アプリケーションとカーネル モード ドライバーが検索し、最上位を開く方法について説明します。 [HID コレクション](hid-collections.md)します。

### <a name="user-mode-application"></a>ユーザー モード アプリケーション

Microsoft Windows デバイスのインストール ルーチンを提供します (**SetupDi * * * Xxx*関数) を見つけて HIDClass デバイスを識別します。 Windows では、初期化、HID コレクションに接続するには、他の Win32 関数を提供します。

ユーザー モード アプリケーションが読み込まれた後に次の一連の操作を行います。

-   呼び出し[ **HidD\_GetHidGuid** ](https://msdn.microsoft.com/library/windows/hardware/ff538924) HIDClass デバイスのシステム定義の GUID を取得します。

-   呼び出し[ **SetupDiGetClassDevs** ](https://msdn.microsoft.com/library/windows/hardware/ff551069)すべてでサポートされているデバイスのインターフェイスを記述する非透過的なデバイス情報のセットを識別するハンドルを取得する、 [HID コレクション](hid-collections.md)現在システムにインストールされています。 アプリケーションが DIGCF を指定する必要があります\_存在し、DIGCF\_で DEVICEINTERFACE、*フラグ*パラメーターに渡される**SetupDiGetClassDevs**します。

-   呼び出し[ **SetupDiEnumDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff551015)繰り返しを利用可能なインターフェイスのすべての情報を取得します。

-   呼び出し[ **SetupDiGetDeviceInterfaceDetail** ](https://msdn.microsoft.com/library/windows/hardware/ff551120)形式インターフェイスについては、SP とコレクションごとに\_インターフェイス\_デバイス\_詳細\_データ構造体。 **DevicePath**この構造体のメンバーには、Win32 関数を使用したアプリケーションを使用してユーザー モードの名前が含まれています[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858) 、HID ファイル ハンドルを取得するには。コレクションです。

-   呼び出し[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858) HID コレクションにファイル ハンドルを取得します。

### <a name="kernel-mode-driver"></a>カーネル モード ドライバー

カーネル モード ドライバーが関数またはフィルター ドライバーの場合は、デバイス オブジェクトを HID コレクションのデバイス スタックにアタッチします。 ドライバーは、のみ、要求の作成を使用して、デバイスを開く必要があります。

通常使用して、ドライバーでない場合、関数またはフィルター ドライバー[プラグ アンド プレイ通知](https://msdn.microsoft.com/library/windows/hardware/ff559640)コレクションが見つかりません。 コレクションを検索した後、ドライバーは、コレクションを開く要求の作成を使用します。

 

 




