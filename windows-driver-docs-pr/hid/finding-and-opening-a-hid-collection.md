---
title: HID コレクションを検索して開く
description: HID コレクションを検索して開く
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
ms.openlocfilehash: 074582dffe13272a2f7e20f734b093078016cfbb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374331"
---
# <a name="finding-and-opening-a-hid-collection"></a>HID コレクションを検索して開く





このセクションでは、ユーザー モード アプリケーションとカーネル モード ドライバーが検索し、最上位を開く方法について説明します。 [HID コレクション](hid-collections.md)します。

### <a name="user-mode-application"></a>ユーザー モード アプリケーション

Microsoft Windows デバイスのインストール ルーチンを提供します (**SetupDi * * * Xxx*関数) を見つけて HIDClass デバイスを識別します。 Windows では、初期化、HID コレクションに接続するには、他の Win32 関数を提供します。

ユーザー モード アプリケーションが読み込まれた後に次の一連の操作を行います。

-   呼び出し[ **HidD\_GetHidGuid** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidsdi/nf-hidsdi-hidd_gethidguid) HIDClass デバイスのシステム定義の GUID を取得します。

-   呼び出し[ **SetupDiGetClassDevs** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)すべてでサポートされているデバイスのインターフェイスを記述する非透過的なデバイス情報のセットを識別するハンドルを取得する、 [HID コレクション](hid-collections.md)現在システムにインストールされています。 アプリケーションが DIGCF を指定する必要があります\_存在し、DIGCF\_で DEVICEINTERFACE、*フラグ*パラメーターに渡される**SetupDiGetClassDevs**します。

-   呼び出し[ **SetupDiEnumDeviceInterfaces** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)繰り返しを利用可能なインターフェイスのすべての情報を取得します。

-   呼び出し[ **SetupDiGetDeviceInterfaceDetail** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)形式インターフェイスについては、SP とコレクションごとに\_インターフェイス\_デバイス\_詳細\_データ構造体。 **DevicePath**この構造体のメンバーには、Win32 関数を使用したアプリケーションを使用してユーザー モードの名前が含まれています[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea) 、HID ファイル ハンドルを取得するには。コレクションです。

-   呼び出し[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea) HID コレクションにファイル ハンドルを取得します。

### <a name="kernel-mode-driver"></a>カーネル モード ドライバー

カーネル モード ドライバーが関数またはフィルター ドライバーの場合は、デバイス オブジェクトを HID コレクションのデバイス スタックにアタッチします。 ドライバーは、のみ、要求の作成を使用して、デバイスを開く必要があります。

通常使用して、ドライバーでない場合、関数またはフィルター ドライバー[プラグ アンド プレイ通知](https://docs.microsoft.com/windows-hardware/drivers/kernel/pnp-notification-overview)コレクションが見つかりません。 コレクションを検索した後、ドライバーは、コレクションを開く要求の作成を使用します。

 

 




