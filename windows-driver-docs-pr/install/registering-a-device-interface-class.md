---
title: デバイス インターフェイス クラスの登録
description: デバイス インターフェイス クラスの登録
ms.assetid: 1518570d-1cfb-498e-91f7-35f9cc11aff5
keywords:
- インターフェイスクラス WDK デバイスのインストール
- デバイスインターフェイスクラスの登録
- デバイスインターフェイスクラス WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26a2a14777eb9158ffb1284bc6169ec9f255f650
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837372"
---
# <a name="registering-a-device-interface-class"></a>デバイス インターフェイス クラスの登録





デバイスインターフェイスクラスを登録するには、次の3つの方法があります。

-   ほとんどのドライバーなどのカーネルモードコンポーネントは、i/o マネージャールーチンを呼び出すことができます。 このトピックでは、これらのルーチンの使用方法について説明します。

-   ユーザーモードの*デバイスインストールアプリケーション*は、**setupdi * * * Xxx*関数を呼び出します。 これらの関数の詳細については、「 [Setupdi デバイスインターフェイス関数](using-device-installation-functions.md#ddk-setupdi-device-interface-functions-dg)」を参照してください。

-   INF ファイルには、 [**Inf DDInstall. インターフェイスセクション**](inf-ddinstall-interfaces-section.md)を含めることができます。

WDM ドライバーは、そのデバイスオブジェクトに名前を指定しません。 代わりに、ドライバーが[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)を呼び出してデバイスオブジェクトを作成するときは、デバイス名に null 文字列を指定する必要があります。 詳細については、「[デバイスオブジェクトの作成](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-a-device-object)」を参照してください。

デバイスオブジェクトを作成し、デバイススタックにアタッチすると、1つのドライバーが[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)を呼び出して、デバイスインターフェイスクラスを登録し、インターフェイスのインスタンスを作成します。 通常、関数ドライバーは[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンからこの呼び出しを行いますが、フィルタードライバーによってインターフェイスが登録される場合があります。

ルーチンは、シンボリックリンク名を返します。 ドライバーは、デバイスインターフェイスインスタンスを有効または無効にするときに、リンク名を渡します。 その他のシステムコンポーネントは、ドライバーが有効にするまで、デバイスインターフェイスインスタンスを使用できません。 詳細について[は、「デバイスインターフェイスインスタンスの有効化と無効化](enabling-and-disabling-a-device-interface-instance.md)」を参照してください。

また、ドライバーは、シンボリックリンク名を使用してレジストリキーにアクセスします。このキーには、デバイスインターフェイスに固有の情報を格納できます。 (詳細については、「 [**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey) 」を参照してください)。アプリケーションでは、リンク名を使用してデバイスを開きます。

ドライバーは、追加のデバイスインターフェイスクラスのインスタンスを登録するために必要な回数だけ[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)を呼び出すことができます。

 

 





