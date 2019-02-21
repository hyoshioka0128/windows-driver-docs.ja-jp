---
title: WBDI ドライバーのデバイスのインターフェイスを作成します。
description: WBDI ドライバーのデバイスのインターフェイスを作成します。
ms.assetid: 8595092c-9105-4638-814a-74cdfa372638
keywords:
- 生体認証ドライバー WDK、デバイス インターフェイス
- WDK の生体認証デバイスのインターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f67ae29b232a0d3f688a3e347badfd6bb40aec01
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550058"
---
# <a name="creating-a-device-interface-for-a-wbdi-driver"></a>WBDI ドライバーのデバイスのインターフェイスを作成します。


デバイス コールバック オブジェクトを初期化し、キューのセットアップ時に、ドライバーに返されるドライバーは、生体認証デバイスのデバイス インターフェイスのインスタンスを作成する必要があります。

具体的には、WBDI ドライバーは、GUID を公開する必要があります\_DEVINTERFACE\_生体認証の\_リーダー デバイスのインターフェイスを呼び出して[ **IWDFDevice::CreateDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff557016):

```cpp
hr = m_FxDevice->CreateDeviceInterface(&GUID_DEVINTERFACE_BIOMETRIC_READER, NULL);
```

この呼び出しがへの呼び出しに続く[ **IWDFDevice::AssignDeviceInterfaceState**](https://msdn.microsoft.com/library/windows/hardware/ff557006):

```cpp
hr = m_FxDevice->AssignDeviceInterfaceState(&GUID_DEVINTERFACE_BIOMETRIC_READER,
 NULL,
 TRUE);
```

レガシ (WBDI 以外) の生体認証スタックへの機能を公開する必要がある WBDI ドライバーは、レガシ アプリケーションの別のデバイスのインターフェイスを公開して、排他値は、従来のスタックをインストールする INX ファイルでは 0 に設定されていることを確認する必要があります。

GUID を公開する\_DEVINTERFACE\_生体認証の\_リーダー デバイスのインターフェイスが原因で、ドライバーのみを列挙する WBF サービス。 排他モードが設定されていない場合 WBF を開き、デバイスを制御しません。

または、ドライバーを検出でした内部的にレガシ モードとし、GUID を公開していません内にある\_DEVINTERFACE\_生体認証の\_リーダー デバイスのインターフェイス。

 

 





