---
title: DeviceProperties_RunDLL 関数プロトタイプ
description: DeviceProperties_RunDLL 関数プロトタイプ
ms.assetid: 15c93f6d-56e7-4872-a94b-0c948e2cd76f
keywords:
- デバイスのプロパティ ダイアログ ボックスの WDK デバイスのインストール
- デバイスのプロパティ ダイアログ ボックスを呼び出す
- DeviceProperties_RunDLL WDK デバイスのインストール
- マシンのパラメーター名フィールド WDK デバイスのインストール
- デバイス インスタンス ID パラメーター フィールド WDK デバイス命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c761d8a554267920e29c8f53647ff0637d85dee1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532079"
---
# <a name="devicepropertiesrundll-function-prototype"></a>DeviceProperties_RunDLL 関数プロトタイプ


DeviceProperties_RunDLL 関数では、ローカルまたはリモート コンピューターにインストールされている指定されたデバイスのデバイスのプロパティ ダイアログ ボックスが開きます。

```cpp
void DeviceProperties_RunDLL(
  HWND       hwndStub,
  HINSTANCE  hAppInstance,
  LPCTSTR    lpCmdLine,
  int        nCmdShow
  );
```

### <a name="parameters"></a>パラメーター

<a href="" id="hwndstub"></a>*hwndStub*  
ユーザー インターフェイスがその DeviceProperties_RunDLL を項目を表示するウィンドウのハンドルを作成します。

<a href="" id="happinstance"></a>*hAppInstance*  
このパラメーターは、デバイスのプロパティ ダイアログ ボックスを呼び出すには使用されませんしに設定する必要があります**NULL**します。

<a href="" id="lpcmdline"></a>*lpCmdLine*  
定数を含む NULL で終わるコマンド ライン文字列へのポインターを*マシン-名前-パラメーター*フィールドが続く、*デバイス インスタンス ID パラメーター*フィールドで、次の形式。

*マシンの名前-パラメーター デバイス-インスタンスの ID-パラメーター*

<a href="" id="machine-name-parameter"></a>*マシンのパラメーター名*  
*マシン-名前-パラメーター*フィールドで指定されているデバイスに関連付けられているマシンの名前を提供する、*デバイス インスタンス ID パラメーター*フィールド。 形式、*マシン-名前-パラメーター*フィールドは **/MachineName** **** *マシン名*ここで、 **/MachineName**示します*マシン名*コンピューター名を提供します。 詳細については、*マシン-名前-パラメーター*フィールドに、「解説」を参照してください。

<a href="" id="device-instance-id-parameter"></a>*デバイス インスタンス ID パラメーター*  
*デバイス インスタンス ID パラメーター*装置のフィールドを[デバイス インスタンス識別子](device-instance-ids.md)のデバイスのプロパティ ダイアログ ボックスを表示するデバイス。 形式*デバイス インスタンス ID パラメーター*フィールドは **/DeviceId** **** *デバイス インスタンス ID*ここで、 **/DeviceId**ことを示します*デバイス インスタンス ID*デバイス インスタンス id を提供します。 *デバイス インスタンス ID パラメーター*フィールドは必須です。

<a href="" id="ncmdshow"></a>*nCmdShow*  
このパラメーターは、デバイスのプロパティ ダイアログ ボックスを呼び出すには使用されませんしに設定する必要があります**NULL**します。

### <a name="return-value"></a>戻り値

なし

### <a name="headers"></a>ヘッダー

DeviceProperties_RunDLL はパブリック ヘッダーで宣言されていないと、ことができますのみ間接的に呼び出す関数へのポインターをプログラムで取得することによって、または rundll32 を使用しています。

### <a href="" id="comments"></a>「解説」

Windows xp で、*マシン-名前-パラメーター*フィールドは、リモート コンピューターでのみ必要ですし、*マシン-名前-パラメーター*フィールドが指定されていない、既定では、ローカル コンピューターを使用します。 Windows 2000、*マシン-名前-パラメーター*フィールドは、ローカル コンピューターまたはリモート コンピューターに必須です。 ローカル コンピューターを指定するには、次のように設定します。*マシン名*で、*マシン-名前-パラメーター*引用符のペアにフィールド ("")。 コンピューターがリモート コンピューターの場合は、設定*マシン名*有効なコンピューター名にします。 有効なコンピューター名が円記号のペアで構成されるプレフィックスを含める必要があります (\\ \)続けてコンピューター名。

コマンドライン文字列の例を次に示します。

-   (Windows XP 以降)ローカル コンピューターを指定することは、省略可能なデバイスのインスタンス識別子のみを含めるコマンドライン文字列が必要な場合です。 たとえば、次のコマンド ラインには、既定とデバイスのインスタンス識別子によって、ローカル コンピューターを指定します。"ルート\\システム\\0000"。
    ```cpp
    /DeviceId root\system\0000
    ```

-   (Windows 2000 以降)次のコマンド ライン文字列は、リモート コンピューター名を指定します。"\\\\RemoteMachineAbc"とデバイスのインスタンス識別子"ルート\\システム\\0000"。
    ```cpp
    /MachineName \\RemoteMachineAbc /DeviceId root\system\0000
    ```

-   (Windows 2000 以降)次のコマンドライン文字列を引用符のペアで指定されているローカル コンピューターを指定します ("")、デバイスのインスタンス識別子を提供して"ルート\\システム\\0000"。
    ```cpp
    /MachineName "" /DeviceId root\system\0000
    ```

 

 





