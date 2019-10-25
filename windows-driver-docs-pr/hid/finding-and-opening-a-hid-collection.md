---
title: HID コレクションを検索して開く
description: HID コレクションを検索して開く
ms.assetid: b46fdb06-e6ae-4376-994f-69bf6539f2ce
keywords:
- コレクション WDK HID、検索
- HID コレクション WDK、検索
- HID コレクションの検索
- コレクション WDK HID、開く
- HID コレクション WDK、開く
- HID コレクションを開く
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 025bb988eb7d61d5eb060e5b45bf918c58daadcc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824816"
---
# <a name="finding-and-opening-a-hid-collection"></a>HID コレクションを検索して開く





このセクションでは、ユーザーモードアプリケーションとカーネルモードドライバーが最上位の[HID コレクション](hid-collections.md)を検索して開く方法について説明します。

### <a name="user-mode-application"></a>ユーザーモードアプリケーション

Microsoft Windows では、デバイスのインストールルーチン (**Setupdi * * * Xxx* functions) を使用して、HIDClass デバイスを検索して特定します。 Windows には、HID コレクションを初期化して接続するための他の Win32 関数が用意されています。

ユーザーモードアプリケーションが読み込まれると、次の一連の操作が実行されます。

-   HIDClass デバイスのシステム定義の GUID を取得するために、 [**Hidd\_GetHidGuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidsdi/nf-hidsdi-hidd_gethidguid)を呼び出します。

-   [**SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)を呼び出して、システムに現在インストールされているすべての[HID コレクション](hid-collections.md)でサポートされているデバイスインターフェイスを記述する、不透明なデバイス情報セットへのハンドルを取得します。 アプリケーションでは、 **SetupDiGetClassDevs**に渡される*FLAGS*パラメーターに DIGCF\_PRESENT と DIGCF\_deviceinterface を指定する必要があります。

-   [**Setupdienumdeviceinterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)を繰り返し呼び出して、使用可能なすべてのインターフェイス情報を取得します。

-   [**Setupdigetdeviceinterfacedetail**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)を呼び出して、各コレクションのインターフェイス情報を SP\_インターフェイス\_デバイス\_詳細\_データ構造として書式設定します。 この構造体の**DevicePath**メンバーには、HID コレクションへのファイルハンドルを取得するために、アプリケーションが Win32 関数[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)と共に使用するユーザーモード名が含まれています。

-   [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)を呼び出して、HID コレクションへのファイルハンドルを取得します。

### <a name="kernel-mode-driver"></a>カーネルモードドライバー

カーネルモードドライバーが関数またはフィルタードライバーの場合、デバイスオブジェクトが HID コレクションのデバイススタックにアタッチされています。 ドライバーは、デバイスを開くために作成要求のみを使用する必要があります。

ドライバーが機能ドライバーまたはフィルタードライバーでない場合、通常は[プラグアンドプレイ通知](https://docs.microsoft.com/windows-hardware/drivers/kernel/pnp-notification-overview)を使用してコレクションを検索します。 コレクションを検索した後、ドライバーは create 要求を使用してコレクションを開きます。

 

 




