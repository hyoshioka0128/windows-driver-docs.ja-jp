---
title: InstallSelectedDriver 関数
description: InstallSelectedDriver 関数は、選択したデバイスを選択したドライバーをインストールします。
ms.assetid: 8a27f4bb-6d1e-4fe8-810f-23513418254d
keywords:
- InstallSelectedDriver 関数デバイスとドライバーのインストール
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
ms.openlocfilehash: e47d1c83babe694ba9e3a99fe0dd5aa11c026338
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390291"
---
# <a name="installselecteddriver-function"></a>InstallSelectedDriver 関数


**InstallSelectedDriver**関数が非推奨とされます。 Windows Vista 以降を使用して[ **DiInstallDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff544710)代わりにします。

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

*hwndParent* \[in\]  
最上位レベルのウィンドウのハンドルを**InstallSelectedDriver**関数を使用して、ドライバーのインストールに関連付けられているユーザー インターフェイス コンポーネントを表示します。

*DeviceInfoSet* \[で\]  
識別するハンドルを[デバイス情報設定されている](https://msdn.microsoft.com/library/windows/hardware/ff541247)選択したデバイスとデバイスの選択したドライバーを表すデバイス情報要素を格納しています。 デバイスとデバイスのドライバーを選択する方法の詳細については、次を参照してください。**解説**セクション。

*予約済み*\[で\]  
このパラメーターに設定する必要があります**NULL**します。

*バックアップ*\[で\]  
型を決定するブール型の値かどうか**InstallSelectedDriver**関数は、デバイスの選択したドライバーをインストールする前に、選択したデバイスの現在インストールされているドライバーをバックアップします。 現在インストールされているドライバーのバックアップをユーザーには、新しいドライバーを使用した問題が発生した場合は、ユーザーにロールバックできます新しいドライバーのインストール、バックアップ ドライバー。 現在インストールされているドライバーはバックアップされない場合、ユーザー ロールバックできません。 新しいドライバーのインストール、以前にインストールされたドライバー。 場合*バックアップ*に設定されている**TRUE**、 **InstallSelectedDriver** ; 現在インストールされているドライバーをバックアップしますそれ以外の場合、関数はバックアップされません現在インストールされています。ドライバーです。 ドライバーの詳細については、バックアップを参照してください**DiRollbackDriver**します。

*bReboot* \[out\]  
DWORD 型の変数へのポインターを**InstallSelectedDriver**をインストールを完了するシステムの再起動が必要かどうかを示すために設定します。 DI に変数が設定されている場合\_NEEDREBOOT、システムの再起動が必要です。 それ以外の場合、システムの再起動は必要ありません。 呼び出し元は、システムを再起動します。

<a name="return-value"></a>戻り値
------------

**InstallSelectedDriver**返します**TRUE** ; 選択されたデバイスで選択したドライバーがインストールされている場合、関数を返します**FALSE**され、ログに記録されたエラーを取得します。呼び出し**GetLastError**します。

一般的なエラーのいくつかの値を**GetLastError**返す可能性があります次に示します。

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
<td align="left"><p>選択したドライバーは、ドライバーがデバイスにインストールされていたドライバーよりも合わせてでした。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ERROR_IN_WOW64</strong></td>
<td align="left"><p>呼び出し元のアプリケーションとは、これは許可されていない 64 ビット環境で実行しようとする 32 ビット アプリケーションです。 詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541255" data-raw-source="[Installing Devices on 64-Bit Systems](https://msdn.microsoft.com/library/windows/hardware/ff541255)">64 ビット システムでのデバイスのインストール</a>します。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

アクセスする**InstallSelectedDriver**、呼び出す**LoadLibrary**を読み込む*Newdev.dll*を呼び出して**GetProcAddress**関数を取得するにはポインター **InstallSelectedDriver**します。

呼び出す必要がありますのみ**InstallSelectedDriver**特定のデバイスに特定のドライバーをインストールする必要がある場合。

**重要な**   For Windows Vista と Windows での以降のバージョンを呼び出す[ **DiInstallDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff544710)の代わりに**InstallSelectedDriver**にこの種の操作を実行します。

 

特定のデバイスで特定のドライバーのインストールを必要とする特別なアプリケーション、以外、インストール アプリケーションはデバイスに最適なものであるドライバーをインストールする必要があります。 デバイスに最適なものであるドライバーをインストールするには、呼び出す[ **DiInstallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff544717)または[ **UpdateDriverForPlugAndPlayDevices**](https://msdn.microsoft.com/library/windows/hardware/ff553534)します。 これらのデバイス ドライバーをインストールするために呼び出す関数の詳細については、次を参照してください。 [SetupAPI 関数を ドライバーのインストールの簡略化](https://msdn.microsoft.com/library/windows/hardware/ff550867)します。

呼び出しの前に**InstallSelectedDriver**デバイスを含むデバイス情報のセットを取得、セットでデバイスを選択およびデバイスのドライバーを選択する必要があります、呼び出し元。

デバイスを含むデバイス情報のセットを作成するには、次のいずれかの操作を行います。

-   呼び出す[ **SetupDiGetClassDevs** ](https://msdn.microsoft.com/library/windows/hardware/ff551069)デバイスを含むデバイス情報のセットを取得し、呼び出す[ **SetupDiEnumDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff551010)デバイス情報のセット内のデバイスを列挙します。 呼び出しごとに**SetupDiEnumDeviceInfo** SP が返す\_DEVINFO\_デバイス情報のセットで列挙されたデバイスを表すデータ構造体。 列挙されたデバイスに関する特定の情報を取得するには、呼び出す[ **SetupDiGetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551967) SP の指定と\_DEVINFO\_返されたデータの構造体によって**SetupDiEnumDeviceInfo**します。

    - または -

-   呼び出す[ **SetupDiOpenDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff552071)デバイス情報のセットに既知のデバイスのインスタンス ID を使用したデバイスを追加します。 **SetupDiOpenDeviceInfo**を返します、 [ **SP\_DEVINFO\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff552344)デバイス情報のセット内のデバイスを表す構造体です。

SP を取得した後\_DEVINFO\_呼び出し、デバイスのデータ構造[ **SetupDiSetSelectedDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff552176)デバイス情報のセットでデバイスを選択します。

デバイスのドライバーを取得する[ **SetupDiBuildDriverInfoList** ](https://msdn.microsoft.com/library/windows/hardware/ff550917)互換性のあるデバイス ドライバーの一覧を作成し、呼び出す[ **SetupDiEnumDriverInfo**](https://msdn.microsoft.com/library/windows/hardware/ff551018)デバイスのドライバーのリストの要素を列挙します。 各列挙のドライバーの**SetupDiEnumDriverInfo** SP を取得します。\_DRVINFO\_ドライバーを表すデータ構造。 [**SetupDiGetDriverInfoDetail** ](https://msdn.microsoft.com/library/windows/hardware/ff551973)列挙のドライバーに関する追加情報の取得を呼び出すことができます。

SP を取得した後\_DRVINFO\_、ドライバーでは、呼び出しのデータ構造[ **SetupDiSetSelectedDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff552183)をデバイスのドライバーを選択します。

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
<td align="left"><p>Microsoft Windows 2000 および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">None (、 <strong>InstallSelectedDriver</strong>関数は、パブリック ヘッダー ファイルで定義されていません。 詳細については、次を参照してください。、<strong>解説</strong>セクション。 )</td>
</tr>
<tr class="even">
<td align="left"><p>Library</p></td>
<td align="left">Newdev.lib</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">Newdev.dll</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DiInstallDevice**](https://msdn.microsoft.com/library/windows/hardware/ff544710)

[**DiInstallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff544717)

[**SetupDiBuildDriverInfoList**](https://msdn.microsoft.com/library/windows/hardware/ff550917)

[**SetupDiEnumDeviceInfo**](https://msdn.microsoft.com/library/windows/hardware/ff551010)

[**SetupDiEnumDriverInfo**](https://msdn.microsoft.com/library/windows/hardware/ff551018)

[**SetupDiGetClassDevs**](https://msdn.microsoft.com/library/windows/hardware/ff551069)

[**SetupDiGetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551967)

[**SetupDiGetDriverInfoDetail**](https://msdn.microsoft.com/library/windows/hardware/ff551973)

[**SetupDiOpenDeviceInfo**](https://msdn.microsoft.com/library/windows/hardware/ff552071)

[**SetupDiSetSelectedDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552176)

[**SetupDiSetSelectedDriver**](https://msdn.microsoft.com/library/windows/hardware/ff552183)

[**UpdateDriverForPlugAndPlayDevices**](https://msdn.microsoft.com/library/windows/hardware/ff553534)

 

 






