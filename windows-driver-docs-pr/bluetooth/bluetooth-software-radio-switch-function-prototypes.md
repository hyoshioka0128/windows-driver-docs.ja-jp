---
title: 以前の Windows バージョンでの Bluetooth バージョンとプロファイルのサポート
description: 以前の Windows バージョンでの Bluetooth バージョンとプロファイルのサポート
ms.assetid: A5A81EAA-0DC7-4725-AA0D-5C4867DDE47C
ms.date: 02/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: ce02d9d590e14f1cbff085c8f403e6f83aca5306
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328246"
---
# <a name="bluetooth-software-radio-switch-function-prototypes"></a>Bluetooth ソフトウェアの無線スイッチ関数のプロトタイプ

> 注:以降では、Windows 8.1 オペレーティング システムがこの機能を今すぐ処理するため、ソフトウェアのように、このトピックで説明されている DLL で無線 (Bluetooth 4.0 ラジオ) の機能のオン/オフを実装するためにベンダーは必要なくなりました。 Windows 8.1 では、このような DLL を無視します。 存在する場合でもです。

Windows 8 では、Bluetooth 無線がソフトウェア機能のオン/オフをサポートする必要があります。 ベンダー最大限の柔軟性を許可するのにメディアの Bluetooth 無線マネージャーには、ユーザーに公開するには、この機能を許可するプラグインがサポートしています。

この DLL のプラグインを提供するには、2 つの処理を行う必要があります。

コンピューターに DLL を登録する必要があります、適切な関数をエクスポートする DLL を作成する必要があります。 DLL にオプションの状態を保持する役割が、システムの再起動後を含む DLL は 2 つの関数をエクスポートする必要があります。

-    BluetoothEnableRadio:ラジオ サポート DLL は、BluetoothEnableRadio 無線の電源をオンまたはオフにする Windows を有効にするを実装します。

```cpp
C++ 
DWORD WINAPI BluetoothEnableRadio(
   BOOL fEnable
);
``` 

fEnable:ラジオの電源をオンにするの TRUE に設定します。 ラジオの電源をオフに FALSE に設定します。

値が返されます。FEnable の状態を現在の状態が変更された場合は、ERROR_SUCCESS を返します。 それ以外の場合、現在の状態が変更されていない場合は、WIN32 エラー コードを返します。

-    IsBluetoothRadioEnabled:無線のサポート DLL は、無線の電源がオンかオフのかどうかを決定する Windows を有効にする IsBluetoothRadioEnabled を実装します。

```cpp
C++ 
DWORD WINAPI IsBluetoothRadioEnabled(
   BOOL* pfEnabled
);
```
pfEnabled:電源オプションにバッファーを記述するへのポインターが有効か無効です。

値が返されます。現在の状態を取得した場合は、ERROR_SUCCESS を返します。 今すぐ pfEnabled が指す値には、状態が含まれています。 (true または false)。 それ以外の場合、現在の状態が取得されていない場合は、WIN32 エラー コードを返します。 PfEnabled によって示される値は未定義とは使用できません。

DLL の登録

メニューと、コントロール パネル アプレットでソフトウェアのオプションのスイッチ コントロールを有効にするには、このサポートの DLL を登録する必要があります。 対象の DLL への完全パス (環境変数を含めることがあります) に次のレジストリ値を設定します。

記号の意味:HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Radio サポート

値の名前: "SupportDLL"

値のデータ: (パス)

以下に例を示します。

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Radio サポート]

"SupportDLL「=」c:\\プログラム ファイル\\Fabrikam\\BthSupport.dll"

C:\Program Files\Fabrikam など、セキュリティで保護された場所に DLL をインストールすることが必要です。

要件と推奨事項

この設計では、ハードウェアの制御方法の柔軟性、中には、必要なオプションから送信/受信ありませんオフの状態が得られる。 さらに、お勧め Bluetooth スタックを許可するエネルギーを節約バスから削除するために最低の電源状態にラジオの電源をアンロードします。

オプションの状態の変更が行われた後のみ BluetoothEnableRadio は結果を返します。 さらに、この DLL の拡張機能は、Windows 内のインフラストラクチャのオン/オフの統合オプションを提供するものでは、ため、DLL の使用状況は Windows コンポーネントの予約する必要があります。 コンテキストの Bluetooth メディア ラジオ マネージャー (例: スイッチの外部の無線をオフにするにする場合は、DLL は、Windows 以外のコンポーネントでも使用、またはハードウェア スイッチが実装されている場合、正しい結果が返されるようにする DLL の役目です。有線、無線の電源を切ります)。

Windows 8 のラジオの管理には、ローカル サービス アカウントのコンテキストで、特定の命令を実行する DLL が必要です。 このコンテキストで、DLL が通常のユーザー コンテキストの場合よりも小さいか通常、ローカル コンピューターで最低限の特権があります。

ラジオ サポート DLL には、すべてのアクションを実行する前に、対応するハードウェアの有無を確認する適切なチェックを実行する必要があります。 システムに対応するハードウェアが見つからない場合、無線のサポートを DLL は、適切なエラー コードを返す必要があります。

## <a name="bluetooth-software-radio-sample-sources"></a>Bluetooth ソフトウェア無線サンプル ソース
レジストリ ファイル

Windows レジストリ エディタ Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BthServ]

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BthServ\Parameters]

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BthServ\Parameters\Radio サポート]

"SupportDLL"= 16 進数 (2): 25, 00、73、00、79、00、73、00、74、00、65、00, 6 d、00, 72, 00、6f、00、6f、\

00,74,00,25,00、5c、00、73、00、79、00、73、00、74、00、65、00、6 d、00、33、00、32、00, 5 c, 00 \

72,00,73,00,75,00,70,00,70,00、6f、00、72、00、74、00、2e、00、64、00、6 c、00、6 c、00 時 00 分、\

00


メイクファイル
```cpp
###### --------------------------------------------------------------------

######

###### Copyright(c) Microsoft Corp., 2012

######

###### --------------------------------------------------------------------
```

! ifdef NTMAKEENV

!INCLUDE $(NTMAKEENV)\makefile.def

! else # NTMAKEENV

! ビルド環境を設定していません - エラー

! endif 


RSupport.cpp

/* + Copyright (c) Microsoft Corporation です。 All rights reserved.

このコードと情報姿提供される「現状有姿のいずれか

種類、またはいずれかが含まれるなどに限られず、

商品性や特定の適合性の黙示の保証

目的。

モジュール名:

Rsupport.cpp

概要:

--*/

DWORD WINAPI IsBluetoothRadioEnabled(BOOL* pfEnabled)

{

オプションが有効になっている場合は、設定 * pfEnabled = TRUE 他セット * pfEnabled = FALSE

ERROR_SUCCESS; を返す

}

DWORD WINAPI BluetoothEnableRadio(BOOL fEnable)

{

場合 (fEnabled)

{

ここでオプションを有効にします。

}

その他

{

ここでオプションを無効にします。

}

ERROR_SUCCESS; を返す

}


RSupport.def

/*++

Copyright (c) Microsoft Corporation. All rights reserved.

このコードと情報姿提供される「現状有姿のいずれか

種類、またはいずれかが含まれるなどに限られず、

商品性や特定の適合性の黙示の保証

目的。

モジュール名:

Rsupport.def

概要:

--*/

ライブラリ rsupport.dll

EXPORTS

BluetoothEnableRadio

IsBluetoothRadioEnabled 


サンプル ソース

#

# <a name="copyright-2012---microsoft-corporation"></a>Copyright 2012 - Microsoft Corporation

#

TARGETNAME=rsupport

TARGETPATH=obj

TARGETTYPE DYNLINK を =

UMTYPE windows を =

USE_MSVCRT = 1

TARGETLIBS= \

$(SDK_LIB_PATH)\kernel32.lib \

$(SDK_LIB_PATH)\user32.lib \

C_DEFINES=-DWIN32 -DUNICODE -D_UNICODE

SOURCES = RSupport.cpp 




