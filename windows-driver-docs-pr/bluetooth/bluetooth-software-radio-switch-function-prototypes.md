---
title: 以前の Windows バージョンでの Bluetooth バージョンとプロファイルのサポート
description: 以前の Windows バージョンでの Bluetooth バージョンとプロファイルのサポート
ms.assetid: A5A81EAA-0DC7-4725-AA0D-5C4867DDE47C
ms.date: 02/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: ca411bbe2ec5ca2b522230c1ed7e201e9105ea9c
ms.sourcegitcommit: 19ba939a139e8ad62b0086c30b2fe772a2320663
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/21/2019
ms.locfileid: "72681931"
---
# <a name="bluetooth-software-radio-switch-function-prototypes"></a>Bluetooth ソフトウェアの無線スイッチ関数のプロトタイプ

> 注: このトピックで説明されているように、このトピックで説明するように、Windows 8.1 ベンダーは、このトピックで説明するように、ソフトウェア DLL で無線オン/オフ機能 (Bluetooth 4.0 ラジオの場合) を実装する必要がなくなりました。これは、オペレーティングシステムがこの機能を処理するためです。 Windows 8.1 は、存在する場合でも、このような DLL を無視します。

Windows 8 では、Bluetooth ラジオはソフトウェアのオン/オフ機能をサポートする必要があります。 ベンダーが最大限の柔軟性を実現するために、Bluetooth Media Radio Manager は、この機能をユーザーに公開するためのプラグインをサポートしています。

この DLL プラグインを提供するには、2つの処理を行う必要があります。

Dll を作成して、正しい関数をエクスポートする必要があります DLL をコンピューターに登録する必要があります。 DLL は、システムの再起動を含め、次の2つの関数をエクスポートする必要があります。

- BluetoothEnableRadio: ラジオサポート DLL は、Windows が電源をオンまたはオフにできるように BluetoothEnableRadio を実装します。

```cpp
C++
DWORD WINAPI BluetoothEnableRadio(
   BOOL fEnable
);
```

fEnable: TRUE に設定すると、無線電源オンになります。 ラジオの電源をオフにするには、FALSE に設定します。

戻り値: 現在の状態が fEnable の状態に変更された場合は、ERROR_SUCCESS を返します。 それ以外の場合、現在の状態が変更されていない場合は、WIN32 エラーコードを返します。

- IsBluetoothRadioEnabled: ラジオサポート DLL は IsBluetoothRadioEnabled を実装して、Windows がラジオの電源がオンかオフかを判別できるようにします。

```cpp
C++
DWORD WINAPI IsBluetoothRadioEnabled(
   BOOL* pfEnabled
);
```

pfEnabled: ラジオの電源がオンかオフかを説明するバッファーへのポインター。

戻り値: 現在の状態が取得された場合は、ERROR_SUCCESS を返します。 PfEnabled によってポイントされた値に状態が含まれるようになりました。 (true または false)。 それ以外の場合、現在の状態が取得されなかった場合は、WIN32 エラーコードを返します。 PfEnabled によってポイントされる値は定義されていないため、使用しないでください

DLL の登録

メニューおよびコントロールパネルアプレットでソフトウェアオプションのスイッチコントロールを有効にするには、このサポート DLL を登録する必要があります。 次のレジストリ値を、問題の DLL への完全なパス (環境変数を含めることができます) に設定します。

キー: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Radio のサポート

値の名前: "SupportDLL"

値のデータ: (パス)

以下に例を示します。

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Radio サポート]

"SupportDLL" = "C: \\Program ファイル \\Fabrikam \\BthSupport"

DLL は、C:\Program Files\Fabrikam. などの安全な場所にインストールする必要があります。

## <a name="requirements-and-recommendations"></a>要件と推奨事項

この設計では、ハードウェアの制御方法を柔軟に行うことができますが、オフの状態では無線からの送信/受信が行われないようにする必要があります。 また、電力を節約し、それをバスから削除して Bluetooth スタックをアンロードできるようにするには、ラジオの電源を最も低い状態にすることをお勧めします。

BluetoothEnableRadio は、ラジオ状態の変更が発生した後にのみ結果を返します。 また、この DLL 拡張機能は、Windows 内で統合されたオプションのオン/オフのインフラストラクチャを提供することを目的としているため、DLL の使用は Windows コンポーネント用に予約する必要があります。 Dll が Windows 以外のコンポーネントによっても使用されている場合、または、Bluetooth メディアラジオマネージャー (スイッチなど) のコンテキスト外でオプションをオフにするハードウェアスイッチが実装されている場合、DLL の役割は、正しい結果が返されるようにすることです。電源を入れてラジオの電源をオフにします)。

Windows 8 のラジオ管理を行うには、DLL の指示をローカルサービスアカウントコンテキストで実行する必要があります。 このコンテキストでは、DLL にはローカルコンピューターに対する最小限の特権が与えられます。これは通常、通常のユーザーコンテキストよりも小さくなります。

ラジオサポート DLL は、適切なチェックを実行して、対応するハードウェアの存在を確認してから、アクションを実行します。 対応するハードウェアがシステムに見つからない場合は、ラジオサポート DLL から適切なエラーコードが返されます。

## <a name="bluetooth-software-radio-sample-sources"></a>Bluetooth ソフトウェアラジオのサンプルソース

レジストリファイル

Windows レジストリエディターバージョン5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BthServ]

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BthServ\Parameters]

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BthServ\Parameters\Radio サポート]

"SupportDLL" = hex (2):25、00、73、00、79、00、73、00、74、00、65、00、6d、00、72、00、6f、00、6f、\

00、74、00、25、00、5c、00、73、00、79、00、73、00、74、00、65、00、6d、00、33、00、32、00、5c、00、\

72、00、73、00、75、00、70、00、70、00、6f、00、72、00、74、00、2e、00、64、00、6c、00、6c、00、00、\

モスクワ

」

```cpp
###### --------------------------------------------------------------------

######

###### Copyright(c) Microsoft Corp., 2012

######

###### --------------------------------------------------------------------

!ifdef NTMAKEENV

!INCLUDE $(NTMAKEENV)\makefile.def

!else # NTMAKEENV

!error - You forgot to set your build environment

!endif

RSupport.cpp

/*++ Copyright (c) Microsoft Corporation. All rights reserved.

THIS CODE AND INFORMATION IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY

KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE

IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A PARTICULAR

PURPOSE.

Module Name:

Rsupport.cpp

Abstract:

--*/

DWORD WINAPI IsBluetoothRadioEnabled(BOOL* pfEnabled)

{

// If the radio is enabled, set *pfEnabled = TRUE else set *pfEnabled = FALSE

return ERROR_SUCCESS;

}

DWORD WINAPI BluetoothEnableRadio(BOOL fEnable)

{

if (fEnabled)

{

// Enable the radio here

}

else

{

// Disable the radio here

}

return ERROR_SUCCESS;

}

RSupport.def

/*++

Copyright (c) Microsoft Corporation. All rights reserved.

THIS CODE AND INFORMATION IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY

KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE

IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A PARTICULAR

PURPOSE.

Module Name:

Rsupport.def

Abstract:

--*/

LIBRARY rsupport.dll

EXPORTS

BluetoothEnableRadio

IsBluetoothRadioEnabled

Sample SOURCES

#

# Copyright 2012 - Microsoft Corporation

#

TARGETNAME=rsupport

TARGETPATH=obj

TARGETTYPE=DYNLINK

UMTYPE=windows

USE_MSVCRT=1

TARGETLIBS= \

$(SDK_LIB_PATH)\kernel32.lib \

$(SDK_LIB_PATH)\user32.lib \

C_DEFINES=-DWIN32 -DUNICODE -D_UNICODE

SOURCES = RSupport.cpp
```
