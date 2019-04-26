---
title: 共同インストーラーのインターフェイス
description: 共同インストーラーのインターフェイス
ms.assetid: affcf2a5-5dbb-49bd-916c-bc99302b5bd8
keywords:
- 共同インストーラー WDK デバイス インストールでは、インターフェイスします。
- インターフェイスの WDK 共同インストーラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b82a56a3952f71ef8ff024cb81f22034521525b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357047"
---
# <a name="co-installer-interface"></a>共同インストーラーのインターフェイス


Co-インストーラーのインターフェイスは、エクスポートされたエントリ ポイント関数と、関連付けられているデータ構造で構成されます。

### <a href="" id="co-installer-entry-point"></a> 共同インストーラー エントリ ポイント

共同インストーラーを次のプロトタイプを持つエントリ ポイント関数をエクスポートする必要があります。

```cpp
typedef DWORD 
  (CALLBACK* COINSTALLER_PROC) (
    IN DI_FUNCTION  InstallFunction,
    IN HDEVINFO  DeviceInfoSet,
    IN PSP_DEVINFO_DATA  DeviceInfoData  OPTIONAL,
    IN OUT PCOINSTALLER_CONTEXT_DATA  Context
    );
```

<a href="" id="installfunction"></a>*InstallFunction*  
共同インストーラーが参加しているのオプションを含むで処理されているデバイスのインストール要求を指定します。 これらの要求は DIF_INSTALLDEVICE などの差分のコードを使用して指定します。 詳細については、次を参照してください。[デバイス インストールの関数コード](https://msdn.microsoft.com/library/windows/hardware/ff541307)します。

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
識別するハンドルを提供する[デバイス情報設定されている](device-information-sets.md)します。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
必要に応じて、デバイスのインストール要求の対象となっているデバイスを識別します。 このパラメーターがない場合、**NULL**デバイスの情報セット内のデバイス情報要素を識別します。 *DeviceInfoData*以外**NULL**とき[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)デバイスに固有の共同インストーラーを呼び出します。 クラスに固有の共同インストーラーを持つ差分要求で呼び出すことができます、**NULL * * * DeviceInfoData*DIF_DETECT や DIF_FIRSTTIMESETUP など。

<a href="" id="context"></a>*コンテキスト*  
指す、 [ **COINSTALLER_CONTEXT_DATA** ](#coinstaller-context-data)構造体。

デバイスの共同インストーラーは、次の値のいずれかを返します。

<a href="" id="no-error"></a>NO_ERROR  
指定された共同インストーラーが、適切なアクションを実行*InstallFunction*、または共同インストーラーは、要求のすべてのアクションを実行する必要はなかったことを決定します。

認識できない DIF コードを受信した場合、共同インストーラーは NO_ERROR も返す必要があります。 (クラスのインストーラーが認識されない DIF コード ERROR_DI_DO_DEFAULT を返すことに注意してください)。

<a href="" id="error-di-postprocessing-required"></a>ERROR_DI_POSTPROCESSING_REQUIRED  
共同インストーラーが、指定された適切なアクションを実行*InstallFunction*クラスのインストーラーが、要求を処理した後でもう一度呼び出されるを要求しているとします。

<a href="" id="a-win32-error"></a>*Win32 エラー*  
共同インストーラーには、エラーが発生しました。

共同インストーラーでは、ERROR_DI_DO_DEFAULT の状態の戻り値は設定されません。 この状態は、クラスのインストーラーによってのみ使用できます。 共同インストーラーが、この状態を返す場合**SetupDiCallClassInstaller** 、DIF_ は処理されません*Xxx*適切に要求します。 共同インストーラーが*伝達*状態の戻り値の ERROR_DI_DO_DEFAULT の処理後のパスが決して*設定*値。

### <a href="" id="coinstaller-context-data"></a> COINSTALLER_CONTEXT_DATA

COINSTALLER_CONTEXT_DATA は、インストール要求を記述する installer 共同に固有のコンテキスト構造です。 構造体の形式です。

```cpp
typedef struct 
  _COINSTALLER_CONTEXT_DATA {
      BOOLEAN  PostProcessing;
      DWORD    InstallResult;
      PVOID    PrivateData;
  } COINSTALLER_CONTEXT_DATA, *PCOINSTALLER_CONTEXT_DATA;
```

次の一覧には、この構造体のメンバーについて説明します。

-   **処理後の**は**TRUE** 、いずれかがで指定された差分コードを処理する場合に、適切なクラスのインストーラーを後で共同インストーラーが呼び出されたとき*InstallFunction*します。 **処理後の**は共同インストーラーには読み取り専用です。

-   場合**後処理**は**FALSE**、 **InstallResult**は関係ありません。 場合**後処理**は**TRUE**、 **InstallResult**インストール要求の現在の状態します。 この値は NO_ERROR またはこのと呼ばれる以前のコンポーネントによって返されたエラー状態が要求をインストールします。 共同インストーラーは、その関数の戻り値のこの値を返すことによって、状態を伝達できますか、別の状態を返すことができます。 **InstallResult**は共同インストーラーには読み取り専用です。

-   **PrivateData**共同 installer が割り当てたバッファーを指します。 このポインターと要求の処理後の共同インストーラーが設定されている場合**SetupDiCallClassInstaller**処理後の共同インストーラーを呼び出すときに、共同インストーラーにポインターを渡します。

 

 





