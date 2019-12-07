---
title: InstallSelectedDriver 関数
description: InstallSelectedDriver 関数は、選択したデバイスに選択したドライバーをインストールします。
ms.assetid: 8a27f4bb-6d1e-4fe8-810f-23513418254d
keywords:
- InstallSelectedDriver 関数のデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- InstallSelectedDriver
api_location:
- Newdev.dll
api_type:
- DllExport
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 508eccb24fb15d9b2004823939b8afc6e949f00f
ms.sourcegitcommit: a97a623d64ddf573c760664be17778606e156cf5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2019
ms.locfileid: "74907126"
---
# <a name="installselecteddriver-function"></a>InstallSelectedDriver 関数


**Installselecteddriver**関数は非推奨とされます。 Windows Vista 以降では、代わりに[**Diinstalldevice**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldevice)を使用します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
BOOL WINAPI InstallSelectedDriver(
  _In_  HWND     hwndParent,
  _In_  HDEVINFO DeviceInfoSet,
  _In_  LPCTSTR  Reserved,
  _In_  BOOL     Backup,
  _Out_ PDWORD   bReboot
);
```

<a name="parameters"></a>パラメーター
----------

\] の*hwndParent* \[  
**Installselecteddriver**関数が、ドライバーのインストールに関連付けられているユーザーインターフェイスコンポーネントを表示するために使用するトップレベルウィンドウへのハンドル。

\] の*Deviceinfoset* \[  
選択されたデバイスとデバイス用に選択されたドライバーを表すデバイス情報要素を含む[デバイス情報セット](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)へのハンドル。 デバイスとデバイスのドライバーを選択する方法の詳細については、次の「**解説**」を参照してください。

\] に*予約*された \[  
このパラメーターは**NULL**に設定する必要があります。

\] の*バックアップ*\[  
指定されたデバイス用に選択したドライバーをインストールする前に、 **Installselecteddriver**が現在インストールされているドライバーをバックアップするかどうかを決定する BOOL 型の値。 現在インストールされているドライバーがバックアップされていて、ユーザーが新しいドライバーで問題を検出した場合、ユーザーは、新しいドライバーのインストールをバックアップされたドライバーにロールバックすることができます。 現在インストールされているドライバーがバックアップされていない場合、ユーザーは、新しいドライバーのインストールを以前にインストールされたドライバーにロールバックすることはできません。 *Backup*が**TRUE**に設定されている場合、 **installselecteddriver**は現在インストールされているドライバーをバックアップします。それ以外の場合、関数は現在インストールされているドライバーをバックアップしません。 ドライバーのバックアップの詳細については、「 **DiRollbackDriver**」を参照してください。

*ブート*\[\]  
インストールを完了するためにシステムの再起動が必要かどうかを示すために**Installselecteddriver**によって設定される DWORD 型の変数へのポインター。 変数が DI に設定されている場合\_再起動が必要な場合は、システムを再起動する必要があります。それ以外の場合、システムの再起動は必要ありません。 呼び出し元は、システムの再起動を担当します。

<a name="return-value"></a>戻り値
------------

**Installselecteddriver**は、選択したデバイスに選択したドライバーがインストールされている場合に**TRUE**を返します。それ以外の場合、関数は**FALSE**を返し、ログに記録されたエラーは、 **GetLastError**を呼び出すことによって取得できます。

**GetLastError**が返す可能性のある一般的なエラー値のいくつかを次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターン コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>NO_ERROR</strong></td>
<td align="left"><p>選択したドライバーは、以前にデバイスにインストールされていたドライバーよりもドライバーと一致するようになりました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ERROR_IN_WOW64</strong></td>
<td align="left"><p>呼び出し元のアプリケーションは、64ビット環境で実行しようとしている32ビットアプリケーションですが、これは許可されていません。 詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/device-installations-on-64-bit-systems" data-raw-source="[Installing Devices on 64-Bit Systems](https://docs.microsoft.com/windows-hardware/drivers/install/device-installations-on-64-bit-systems)">64 ビットシステムへのデバイスのインストール</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**Installselecteddriver**にアクセスするには、 **LoadLibrary**を呼び出して*Newdev .dll*を読み込み、 **GetProcAddress**を呼び出して**installselecteddriver**への関数ポインターを取得します。

特定のデバイスに特定のドライバーをインストールする必要がある場合にのみ、 **Installselecteddriver**を呼び出す必要があります。

**重要**   windows Vista 以降のバージョンの windows では、この種類の操作を実行するには、 **installselecteddriver**ではなく[**diinstalldevice**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldevice)を呼び出します。

 

特定のデバイスに特定のドライバーをインストールする必要がある特殊なアプリケーション以外は、インストールアプリケーションで、デバイスに最適なドライバーをインストールする必要があります。 デバイスに最適なドライバーをインストールするには、 [**Diinstalldriver**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)または[**UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)を呼び出します。 これらの関数のうち、デバイスにドライバーをインストールするために呼び出すものの詳細については、「[ドライバーのインストールを簡略化する Setupapi.log 関数](https://docs.microsoft.com/windows-hardware/drivers/install/functions-that-simplify-driver-installation)」を参照してください。

**Installselecteddriver**を呼び出す前に、呼び出し元はデバイスを含むデバイス情報セットを取得し、セット内のデバイスを選択して、デバイスのドライバーを選択する必要があります。

デバイスを含むデバイス情報セットを作成するには、次のいずれかの操作を行います。

-   [**SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)を呼び出して、デバイスを含むデバイス情報セットを取得し、 [**SetupDiEnumDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo)を呼び出してデバイス情報セット内のデバイスを列挙します。 各呼び出しで、 **SetupDiEnumDeviceInfo**は、デバイス情報セット内の列挙されたデバイスを表す SP\_DEVINFO\_データ構造を返します。 列挙されたデバイスに関する特定の情報を取得するには、 [**SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)を呼び出し、 **SetupDiEnumDeviceInfo**によって返された SP\_DEVINFO\_データ構造体を指定します。

    - または -

-   [**SetupDiOpenDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinfoa)を呼び出して、既知のデバイスインスタンス ID を持つデバイスをデバイス情報セットに追加します。 **SetupDiOpenDeviceInfo**は、デバイス情報セット内のデバイスを表す[**SP\_DEVINFO\_データ**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)構造を返します。

デバイスの SP\_DEVINFO\_データ構造を取得した後、 [**Setupdisetselecteddevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetselecteddevice)を呼び出してデバイス情報セット内のデバイスを選択します。

デバイスのドライバーを取得するには、 [**Setupdibuilddriverinfolist**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuilddriverinfolist)を呼び出して、デバイスの互換性のあるドライバーの一覧を作成し、 [**Setupdienumdriverinfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdriverinfoa)を呼び出して、デバイスのドライバー一覧の要素を列挙します。 **Setupdienumdriverinfo**は、列挙されたドライバーごとに、ドライバーを表す SP\_DRVINFO\_データ構造を取得します。 [**Setupdigetdriverinfodetail**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdriverinfodetaila)は、列挙されたドライバーに関する追加情報を取得するために呼び出すことができます。

ドライバーの SP\_DRVINFO\_データ構造を取得したら、 [**Setupdisetselecteddriver**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetselecteddrivera)を呼び出して、デバイスのドライバーを選択します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Microsoft Windows 2000 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">None ( <strong>Installselecteddriver</strong>関数は、パブリックヘッダーファイルで定義されていません。 詳細については、「<strong>解説</strong>」を参照してください。 で、録画する時間数を設定)</td>
</tr>
<tr class="even">
<td align="left"><p>Library</p></td>
<td align="left">Newdev .lib</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">Newdev .dll</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DiInstallDevice**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldevice)

[**DiInstallDriver**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)

[**SetupDiBuildDriverInfoList**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuilddriverinfolist)

[**SetupDiEnumDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo)

[**SetupDiEnumDriverInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdriverinfoa)

[**SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)

[**SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)

[**SetupDiGetDriverInfoDetail**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdriverinfodetaila)

[**SetupDiOpenDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinfoa)

[**SetupDiSetSelectedDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetselecteddevice)

[**SetupDiSetSelectedDriver**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetselecteddrivera)

[**UpdateDriverForPlugAndPlayDevices**](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)

 

 






