---
title: カスタム プロパティ ページの作成
description: カスタム プロパティ ページの作成
ms.assetid: 2481450f-ebb2-40e3-8a42-eabaecc1c7e4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 897cf3f7d0d0e2575d37de6649b11d45476a571b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363129"
---
# <a name="creating-custom-property-pages"></a>カスタム プロパティ ページの作成


ときに、[デバイスのプロパティ ページのプロバイダー](types-of-device-property-page-providers.md) 、そのデバイスまたはデバイス クラスのプロパティ ページを作成する要求をハンドル、プロバイダーは、次の手順を実行する必要があります。

1.  呼び出す[ **SetupDiGetClassInstallParams** ](https://msdn.microsoft.com/library/windows/hardware/ff551083)現在を取得するクラスは、デバイスのパラメーターをインストールします。 次に、例を示します。

    ```cpp
    SP_ADDPROPERTYPAGE_DATA AddPropertyPageData;
    :
    ZeroMemory(&AddPropertyPageData, sizeof(SP_ADDPROPERTYPAGE_DATA));
    AddPropertyPageData.ClassInstallHeader.cbSize = sizeof(SP_CLASSINSTALL_HEADER);

    if (SetupDiGetClassInstallParams(DeviceInfoSet, DeviceInfoData,
         (PSP_CLASSINSTALL_HEADER)&AddPropertyPageData,
         sizeof(SP_ADDPROPERTYPAGE_DATA), NULL )) {
    ...
    ```

    この例で、コードを 0 に初期化する、デバイスのインストール パラメーターが返されます、構造体とセットのヘッダーをインストールする、クラスのサイズ、 **cbSize**で必要なフィールド**SetupDiGetClassInstallParams**します。 クラスのインストールのヘッダーは、各クラスのインストールのパラメーター構造体の最初のメンバーです。

2.  あるデバイスの動的なページの最大数がまだ満たされていない、次のステートメントを使用して確認します。

    ```cpp
    if (AddPropertyPageData.NumDynamicPages < 
        MAX_INSTALLWIZARD_DYNAPAGES)
     ...
    ```

    テストが失敗した場合、初期化およびありませんページを作成します。 代わりに、NO_ERROR を返します。

3.  後で、ダイアログ ボックス プロシージャで必要になるし、データでは、このメモリが初期化される任意のデバイスに固有のデータを保存するためのメモリを割り当てます。 プロバイダーは、プロパティ ページが破棄されるときに、そのプロパティ ページのコールバックでは、このメモリを解放する必要があります。

    プロバイダーの[共同インストーラー](writing-a-co-installer.md)、このデバイスに固有のデータを含める必要があります、 *DeviceInfoSet*と*DeviceInfoData*で渡される、 [ **DIF_ADDPROPERTYPAGE_ADVANCED** ](https://msdn.microsoft.com/library/windows/hardware/ff543656)デバイス インストール機能 (差分) コード。

    たとえば、プロパティ ページのプロバイダーは定義して、構造体を使用して、次の例に示すようにできます。

    ```cpp
    typedef struct _TEST_PROP_PAGE_DATA {
        HDEVINFO DeviceInfoSet;
        PSP_DEVINFO_DATA DeviceInfoData;
    } TEST_PROP_PAGE_DATA, *PTEST_PROP_PAGE_DATA;
    ...
    PTEST_PROP_PAGE_DATA     pMyPropPageData;
    ...
    pMyPropPageData = HeapAlloc(GetProcessHeap(), 0, sizeof(TESTPROP_PAGE_DATA));
    ```

4.  カスタム プロパティ ページに関する情報を含む PROPSHEETPAGE 構造体を初期化します。

    -   **DwFlags**、PSP_USECALLBACK フラグとカスタム プロパティ ページに必要なその他のフラグを設定します。 PSP_USECALLBACK フラグは、コールバック関数が指定されていることを示します。
    -   **PfnCallback**、プロパティ ページのコールバック関数へのポインターを設定します。 コールバックでは、PSPCB_RELEASE メッセージを処理し、手順 3. で割り当てられたメモリを解放します。
    -   **PfnDlgProc**、プロパティ ページのダイアログ ボックス プロシージャへのポインターを設定します。
    -   **LParam**、メモリ領域に割り当てられ、手順 3 で初期化されたポインターを渡します。
    -   カスタム プロパティ ページに適したその他のメンバーを設定します。 PROPSHEETPAGE 構造の詳細については、Microsoft Windows SDK ドキュメントを参照してください。

5.  呼び出す**CreatePropertySheetPage**新しいページを作成します。

6.  動的プロパティ ページの一覧に新しいページを追加、 **DynamicPages**クラスのメンバーは、パラメーターとインクリメントをインストール、 **NumDynamicPages**メンバー。

7.  各追加のカスタム プロパティ ページの手順 2. ~ 6. を繰り返します。

8.  呼び出す[ **SetupDiSetClassInstallParams** ](https://msdn.microsoft.com/library/windows/hardware/ff552122)新しいクラスをセットアップするには、インストールのパラメーターで、更新されたプロパティのページ構造が含まれます。

9.  NO_ERROR を返します。

Windows が、デバイスのプロパティ シートに新しく作成されたプロパティ ページを追加し、デバイス マネージャーにより、シートを作成するための Microsoft Win32 API 呼び出し。 プロパティ ページが表示されたら、システムは PROPSHEETPAGE 構造体で指定されているダイアログ ボックス プロシージャを呼び出します。

 

 





