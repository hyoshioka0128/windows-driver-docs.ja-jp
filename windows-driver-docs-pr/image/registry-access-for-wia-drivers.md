---
title: WIA ドライバーのレジストリ アクセス
description: WIA ドライバーのレジストリ アクセス
ms.assetid: 0e0b7493-858b-4add-9e1d-fd71bae21b6e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d83eff681187d392c1b1a9f79c43278d2b0efe24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379609"
---
# <a name="registry-access-for-wia-drivers"></a>WIA ドライバーのレジストリ アクセス





ドライバー開発者向けには、アクセスに必要なレジストリ キーのアクセス許可が知っておく必要があります。 レジストリの多くは、ドライバーの読み取りに使用できます。 ただし、WIA ドライバーがそれらに渡されるレジストリ キーにのみ書き込む必要があります、 [ **IStiUSD::Initialize** ](https://msdn.microsoft.com/library/windows/hardware/ff543824)メソッド。

WIA サービスは、高い特権で実行されるので、他のレジストリ キーへの書き込みが Windows XP で可能ですが**LocalSystem**アカウントでは、このことはできません、低い特権の下で**LocalService** Microsoft Windows Server 2003 以降のアカウント。

ドライバーは、多くの場合の外部のレジストリ キーへの書き込みアクセスを必要**IStiUSD::Initialize**します。 ほとんどのドライバーでデータを格納するため、 **DeviceData**サブキー、簡単に開くが、 **DeviceData**サブキーし、後で使用するキーを開いているハンドルを格納します。 キーが必要がなくなった場合にのみ、ドライバーは、レジストリ キーを閉じる必要があります。

次のコード例に示しますを使用して、 **DeviceData**レジストリ サブキー。

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

**DeviceData**レジストリ サブキーには、Windows Me では、および Windows XP 上のドライバーへの読み取り/書き込みアクセス用に開かれて以降。 デバイス キー自体 (に親レジストリ キーなど、 **DeviceData**) は、オペレーティング システムのバージョンに応じて、ドライバーによって書き込みアクセス用に開くことができない可能性があります。

**注**  ドライバー*する必要があります*で開く必要がなくなったらとアンロードする前にすべてのレジストリ キーを閉じる必要がありますが、レジストリ キーを閉じます。

 

 

 




