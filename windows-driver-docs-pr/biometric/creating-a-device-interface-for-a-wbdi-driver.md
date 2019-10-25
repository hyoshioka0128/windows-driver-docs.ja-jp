---
title: WBDI ドライバー用のデバイス インターフェイスの作成
description: WBDI ドライバー用のデバイス インターフェイスの作成
ms.assetid: 8595092c-9105-4638-814a-74cdfa372638
keywords:
- 生体認証ドライバー WDK、デバイスインターフェイス
- デバイスインターフェイス WDK 生体認証
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02981a59046637324eb6e9b7823d6031ce759305
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833949"
---
# <a name="creating-a-device-interface-for-a-wbdi-driver"></a>WBDI ドライバー用のデバイス インターフェイスの作成


デバイスコールバックオブジェクトが初期化され、ドライバーに返されると、キューのセットアップ時に、ドライバーは生体認証デバイス用のデバイスインターフェイスインスタンスを作成する必要があります。

具体的には、WBDI ドライバーは、 [**Iwdfdevice:: CreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createdeviceinterface)を呼び出すことによって、GUID\_devinterface\_生体認証\_リーダーデバイスインターフェイスを公開する必要があります。

```cpp
hr = m_FxDevice->CreateDeviceInterface(&GUID_DEVINTERFACE_BIOMETRIC_READER, NULL);
```

この呼び出しの後に、 [**Iwdfdevice:: 割り当て Deviceinterfacestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-assigndeviceinterfacestate)が呼び出されます。

```cpp
hr = m_FxDevice->AssignDeviceInterfaceState(&GUID_DEVINTERFACE_BIOMETRIC_READER,
 NULL,
 TRUE);
```

レガシ (WBDI) 生体認証スタックに機能を公開する WBDI ドライバーでは、レガシアプリケーション用に別のデバイスインターフェイスを公開し、レガシスタックをインストールする INX ファイルで排他値がゼロに設定されていることを確認する必要があります。

GUID\_DEVINTERFACE\_生体認証\_リーダーデバイスインターフェイスを公開すると、WBF サービスによってドライバーのみが列挙されます。 排他モードが設定されていない場合、WBF はデバイスを開いて制御しようとしません。

または、ドライバーがレガシモードであることを内部で検出した後、GUID\_DEVINTERFACE\_生体認証\_リーダーデバイスインターフェイスに公開しないようにすることもできます。

 

 





