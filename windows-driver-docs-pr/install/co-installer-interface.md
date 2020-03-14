---
title: 共同インストーラーのインターフェイス
description: 共同インストーラーのインターフェイス
ms.assetid: affcf2a5-5dbb-49bd-916c-bc99302b5bd8
keywords:
- 共同インストーラー WDK デバイスのインストール、インターフェイス
- インターフェイス WDK 共同インストーラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1eafe9d061dbffd91c29910e7f6ea3bf3db547c5
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242875"
---
# <a name="co-installer-interface"></a>共同インストーラーのインターフェイス


共同インストーラーのインターフェイスは、エクスポートされたエントリポイント関数と関連付けられたデータ構造で構成されます。

### <a href="" id="co-installer-entry-point"></a>共同インストーラーエントリポイント

共同インストーラーでは、次のプロトタイプを持つエントリポイント関数をエクスポートする必要があります。

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
処理されるデバイスのインストール要求を指定します。このとき、共同インストーラーには参加するオプションがあります。 これらの要求は、DIF_INSTALLDEVICE などの差分コードを使用して指定します。 詳細については、「[デバイスのインストールの機能コード](https://docs.microsoft.com/previous-versions/ff541307(v=vs.85))」を参照してください。

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
[デバイス情報セット](device-information-sets.md)へのハンドルを提供します。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
必要に応じて、デバイスのインストール要求の対象となるデバイスを識別します。 このパラメーターが**NULL**以外の場合は、デバイス情報セット内のデバイス情報要素を識別します。 [**Setupdicallclassinstaller**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)がデバイス固有の共同インストーラーを呼び出すと、 *deviceinfodata*は**NULL**以外になります。 クラス固有の共同インストーラーは、DIF_DETECT や DIF_FIRSTTIMESETUP などの、**NULL * * * DeviceInfoData*を持つ差分要求を使用して呼び出すことができます。

<a href="" id="context"></a>*関連*  
[**COINSTALLER_CONTEXT_DATA**](#coinstaller-context-data)構造体を指します。

デバイスの共同インストーラーは、次のいずれかの値を返します。

<a href="" id="no-error"></a>NO_ERROR  
共同インストーラーは、指定された*Installfunction*に対して適切な操作を実行したか、または要求に対してアクションを実行する必要がないと判断しました。

また、共同インストーラーは、認識されていない差分コードを受け取った場合に NO_ERROR も返す必要があります。 (クラスインストーラーは、認識されていない差分コードに対して ERROR_DI_DO_DEFAULT を返します)。

<a href="" id="error-di-postprocessing-required"></a>ERROR_DI_POSTPROCESSING_REQUIRED  
共同インストーラーは、指定された*Installfunction*に対して適切な操作を実行し、クラスインストーラーが要求を処理した後に再度呼び出すことを要求しています。

<a href="" id="a-win32-error"></a>*Win32 エラー*  
共同インストーラーでエラーが発生しました。

共同インストーラーでは、ERROR_DI_DO_DEFAULT の戻り値の状態は設定されません。 この状態は、クラスインストーラーによってのみ使用できます。 共同インストーラーによってこの状態が返された場合、 **Setupdicallclassinstaller**は DIF_*Xxx*要求を適切に処理しません。 共同インストーラーは、後処理パスで ERROR_DI_DO_DEFAULT の戻り値の状態を*反映*する場合がありますが、この値は*設定*されません。

### <a href="" id="coinstaller-context-data"></a>COINSTALLER_CONTEXT_DATA

COINSTALLER_CONTEXT_DATA は、インストール要求を記述する共同インストーラー固有のコンテキスト構造です。 構造体の形式は次のとおりです。

```cpp
typedef struct 
  _COINSTALLER_CONTEXT_DATA {
      BOOLEAN  PostProcessing;
      DWORD    InstallResult;
      PVOID    PrivateData;
  } COINSTALLER_CONTEXT_DATA, *PCOINSTALLER_CONTEXT_DATA;
```

次の一覧では、この構造体のメンバーについて説明します。

-   適切なクラスインストーラー (存在する場合) によって*Installfunction*によって指定された差分コードが処理された後に、共同インストーラーが呼び出された場合は、**後処理**が**当てはまり**ます。 **後処理**は、共同インストーラーに対しては読み取り専用です。

-   **後処理**が**FALSE**の場合、 **installresult**は関係しません。 **後処理**が**TRUE**の場合、 **installresult**はインストール要求の現在の状態です。 この値は NO_ERROR か、このインストール要求に対して呼び出された前のコンポーネントによって返されたエラー状態です。 共同インストーラーは、関数の戻り値としてこの値を返すことによって状態を伝達するか、別の状態を返すことができます。 **Installresult**は、共同インストーラーに対して読み取り専用です。

-   **Privatedata**は、インストーラーによって割り当てられたバッファーを参照します。 共同インストーラーがこのポインターを設定し、後処理を要求した場合、 **Setupdicallclassinstaller**は、後処理のために共同インストーラーを呼び出すときに、そのポインターを共同インストーラーに渡します。

 

 





