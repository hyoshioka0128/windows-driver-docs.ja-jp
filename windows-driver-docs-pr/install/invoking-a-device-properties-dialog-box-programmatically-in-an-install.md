---
title: インストール アプリケーションでデバイスのプロパティ ダイアログ ボックスを呼び出す
description: インストール アプリケーションでのプログラムによるデバイスのプロパティ ダイアログ ボックスの呼び出し
ms.assetid: c573acac-581e-44f1-b46b-eceb1f3d5484
keywords:
- デバイスのプロパティ ダイアログ ボックスの WDK デバイスのインストール
- デバイスのプロパティ ダイアログ ボックスを呼び出す
- DeviceProperties_RunDLL WDK デバイスのインストール
- デバイスのプロパティ ダイアログ ボックス WDK をプログラムで呼び出す
- pDeviceProperties 関数ポインター WDK
- machin
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3b92d4c9f74caf5b02dee1a54ae40cfe8be305f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346107"
---
# <a name="invoking-a-device-properties-dialog-box-programmatically-in-an-installation-application"></a>インストール アプリケーションでのプログラムによるデバイスのプロパティ ダイアログ ボックスの呼び出し


インストール アプリケーションでプログラムによってデバイスのプロパティ ダイアログ ボックスを呼び出すには、アプリケーション コードが、以下を実行します。

-   マクロ定義を含めるし、適切なバージョンのことを確認するアプリケーション コードの種類の定義[DeviceProperties_RunDLL](deviceproperties-rundll-function-prototype.md)アプリケーションのビルド時にリンクさせます。 Windows には、Unicode のバージョンと ASCII のバージョンがサポートしています。

-   ロード*devmgr.dll*します。

-   ポインターを取得、 **DeviceProperties_RunDLL**関数。

-   呼び出す**DeviceProperties_RunDLL**、適切なパラメーターを指定します。

次のコード例は、定義する方法を示します、 *pDeviceProperties*関数ポインターを参照する、 **DeviceProperties_RunDLL**関数。 _UNICODE マクロを定義して、コードをコンパイルすると場合、 *pDeviceProperties*はこの関数の Unicode バージョンへのポインターは、それ以外の場合*pDeviceProperties*の ASCII バージョンへのポインターです、関数。

```cpp
#ifdef _UNICODE 
  #define DeviceProperties_RunDLL  "DeviceProperties_RunDLLW"
 typedef void (_stdcall *PDEVICEPROPERTIES)(
    HWND hwndStub,
    HINSTANCE hAppInstance,
    LPWSTR lpCmdLine,
 int nCmdShow
   ;
#else
  #define DeviceProperties_RunDLL  "DeviceProperties_RunDLLA"
 typedef void (_stdcall *PDEVICEPROPERTIES)(
    HWND hwndStub,
    HHINSTANCE hAppInstance,
    LPSTR lpCmdLine,
 int nCmdShow
  );
#endif

PDEVICEPROPERTIES pDeviceProperties;
```

次のコード例の定義を使用して*pDeviceProperties*上記のコード例で指定されたを読み込む方法について説明*devmgr.dll*プログラムおよび関数を取得する方法適切なバージョンへのポインター **DeviceProperties_RunDLL**します。

```cpp
HINSTANCE  hDevMgr = LoadLibrary(_TEXT("devmgr.dll"));
 if (hDevMgr) {
 pDeviceProperties = (PDEVICEPROPERTIES)GetProcAddress((HMODULE)hDevMgr, DeviceProperties_RunDLL);
}
```

取得した後、 *pDeviceProperties*関数ポインターの場合は、コンピューター名を指定する必要がありますと[デバイス インスタンス識別子](device-instance-ids.md)への呼び出しで**DeviceProperties_RunDLL**します。 次のコード例は、適切な形式とこれらの項目の要件を示しています。

-   (Windows XP 以降)省略可能な*マシン-名前-パラメーター*フィールドが指定されていないことを示す、既定では、ローカル コンピューターが、コンピューターであります。 必要な*デバイス インスタンス ID パラメーター*フィールド デバイス インスタンス id を提供する"ルート\\システム\\0000"。
    ```cpp
    if (pDeviceProperties){
     pDeviceProperties(m_hWnd, NULL, _TEXT("/DeviceID root\\system\\0000"), NULL);
    };
    ```

-   (Windows XP 以降)省略可能な*マシン-名前-パラメーター*フィールドが指定されていないことを示す、既定では、ローカル コンピューターが、コンピューターであります。 必要な*デバイス インスタンス ID パラメーター*フィールド デバイス インスタンス id を提供する"PCI\\VEN_8086 & DEV_2445 & SUBSYS_010E1028 REV_12\\3 & 172E68DD & 0 & FD"。
    ```cpp
    if (pDeviceProperties){
     pDeviceProperties(m_hWnd, NULL, _TEXT("/DeviceID PCI\\VEN_8086\&DEV_2445\&SUBSYS_010E1028\&REV_12\\3\&172E68DD\&0\&FD"), NULL);
    };
    ```

-   (Windows 2000 以降)必要な*マシン-名前-パラメーター*フィールドは、二重引用符のペアを提供する ("") の*マシン名*コンピューターがローカル コンピューター。 必要な*デバイス インスタンス ID パラメーター*フィールド デバイス インスタンス id を提供する"ルート\\システム\\0000"。
    ```cpp
    if (pDeviceProperties){
     pDeviceProperties(m_hWnd, NULL, _TEXT("/MachineName \"\" /DeviceID root\\system\\0000"), NULL);
    };
    ```

-   (Windows 2000 以降)必要な*マシン-名前-パラメーター*フィールドは、リモート コンピューターの名前を提供"\\\\RemoteMachineAbc"と、必要な*デバイス インスタンス ID パラメーター*装置のフィールド、デバイス インスタンス id"ルート\\システム\\0000"。
    ```cpp
    if (pDeviceProperties){
     pDeviceProperties(m_hWnd, NULL, _TEXT("/MachineName \\\\RemoteMachineAbc /DeviceID root\\system\\0000"), NULL);
    };
    ```

 

 





