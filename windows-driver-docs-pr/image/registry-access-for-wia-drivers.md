---
title: WIA ドライバーのレジストリ アクセス
description: WIA ドライバーのレジストリ アクセス
ms.assetid: 0e0b7493-858b-4add-9e1d-fd71bae21b6e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8fb15acd8b99e02b2c3ee3c3fe7efb9f9bdc7cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840758"
---
# <a name="registry-access-for-wia-drivers"></a>WIA ドライバーのレジストリ アクセス





ドライバー開発者は、アクセスする必要があるレジストリキーのアクセス許可を把握している必要があります。 レジストリの多くは、ドライバーが読み取るために使用できます。 ただし、WIA ドライバーは、 [**Ib usd:: Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)メソッドで渡されたレジストリキーにのみ書き込む必要があります。

Windows XP では他のレジストリキーへの書き込みが可能ですが、WIA サービスは高い特権を持つ**LocalSystem**アカウントで実行されるため、Microsoft windows Server の低い特権の**LocalService**アカウントでは使用できなくなります。2003以降。

多くの場合、ドライバーは、 **Iと usd:: Initialize**以外のレジストリキーへの書き込みアクセスを必要とします。 ほとんどのドライバーは**devicedata**サブキーにデータを格納するため、 **devicedata**サブキーを開いて、開いているキーへのハンドルを格納し、後で使用することが簡単です。 ドライバーは、キーが不要になったときにのみ、レジストリキーを閉じる必要があります。

次のコード例は、 **Devicedata**レジストリサブキーの使用方法を示しています。

```cpp
STDMETHODIMP CWIADevice::Initialize(
  PSTIDEVICECONTROL   pIStiDevControl,
  DWORD               dwStiVersion,
  HKEY                hParametersKey)
{
  .
  .
  .
  //
  // Open the DeviceData key since this is where the
  // driver-specific settings will be stored.
  //
  DWORD dwError = RegOpenKeyEx(
                 hParametersKey,     // handle to open key
                 TEXT("DeviceData"), // subkey to open
                 0,                  // options (must be NULL)
                 KEY_READ|KEY_WRITE, // requesting read/write access
                 &m_hMyWritableRegistryKey);
  if (dwError == ERROR_SUCCESS)
  {
      //
      //  m_hMyWritableRegistryKey now contains a handle to the
      //  DeviceData subkey which can be used to store information
      //  in the registry.
      //  Notice that it isn't closed here, but instead,
      //  kept open because it is needed later.
     //
  }
  else 
  {
      // Handle error
      .
      .
      .
  }
  .
  .
  .
}

STDMETHODIMP CWIADevice::SomeDriverMethod()
{
  .
  .
  .
  //
  //  We need to store some setting in the registry here.
  //
  DWORD dwError = RegSetValueEx(
                     m_hMyWritableRegistryKey,
                     TEXT("MyDriverValueName"),
                     0,
                     REG_DWORD,
                     (BYTE*)&dwValue,
                     sizeof(dwValue));
  if (dwError == ERROR_SUCCESS)
  {
      //
      //  We successfully stored dwValue in the registry
      //
  }
  else 
  {
      // Handle error
      .
      .
      .
  }
  .
  .
  .
}

CWIADevice:: CWIADevice () :
  m_hMyWritableRegistryKey(NULL),
  .
  .
  .
{
  //  Rest of constructor goes here.  Ensure that the
  //   handle to the registry key is initialized to NULL.
}

CWIADevice::~CWIADevice(void)
{
  .
  .
  .
  //
  // If the writable registry key isn't closed  yet, do it now,
  // because the driver is about to be unloaded.
  //
  if (m_hMyWritableRegistryKey) 
  {
      RegCloseKey(m_hMyWritableRegistryKey);
      m_hMyWritableRegistryKey = NULL;
  }

  .
  .
  .
}
```

**Devicedata**レジストリサブキーは、windows Me および windows XP 以降のドライバーへの読み取り/書き込みアクセスのために開かれています。 デバイスキー自体 (たとえば、 **Devicedata**の親レジストリキー) は、オペレーティングシステムのバージョンに応じて、ドライバーによる書き込みアクセス用に開かれている場合もあれば、開いていない場合もあります。

ドライバーは、不要になったときに開かれたすべてのレジストリキーを閉じる*必要がある*  、アンロードする前にすべてのレジストリキーを閉じる必要がある**ことに注意**してください。

 

 

 




