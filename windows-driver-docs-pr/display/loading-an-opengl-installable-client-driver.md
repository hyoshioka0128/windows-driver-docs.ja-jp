---
title: OpenGL のインストール可能なクライアント ドライバーの読み込み
description: OpenGL のインストール可能なクライアント ドライバーの読み込み
ms.assetid: 2b244bbf-f26c-4307-a347-a29e12c6d496
keywords:
- OpenGL ICD WDK の表示
- WDK を表示するドライバーの読み込み
- ICD WDK の表示
- インストール可能なクライアント ドライバー WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 338c0d0896a789b659c17d4a5a4b5c0a5941e829
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531395"
---
# <a name="loading-an-opengl-installable-client-driver"></a>OpenGL のインストール可能なクライアント ドライバーの読み込み


OpenGL ランタイムでは、OpenGL インストール可能なクライアント ドライバーを読み込むには、(ICD) を確認するレジストリにアクセスします。 OpenGL ICD、OpenGL のランタイムを読み込めません。

-   名前、バージョン、および呼び出すことによって、OpenGL ICD に関連付けられているフラグを指定、 [ **D3DKMTQueryAdapterInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff547100) 、KMTQAITYPE で関数を\_UMOPENGLINFO 値の設定、**型**のメンバー、 [ **D3DKMT\_QUERYADAPTERINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff548203)構造体、 *pData*パラメーターポインター。

-   OpenGL ICD のバージョン番号を確認するを**D3DKMTQueryAdapterInfo** OpenGL ICD のバージョンを検証するを返します。

-   OpenGL ICD の名前を使用して OpenGL ICD を読み込みます。

-   OpenGL ICD の関数へのアクセスを初期化します。
    **注**   OpenGL ICD Development kit のライセンスを取得するには、 [OpenGL 問題](mailto:opengl@microsoft.com)チーム。

     

OpenGL ICD の名前を検索する[ **D3DKMTQueryAdapterInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff547100)次のキーにレジストリを検索します。

```registry
HKLM/System/CurrentControlSet/Control/Class/{Adapter GUID}/0000/
```

このキーは、の名前も含まれています。、 [Microsoft Direct3D ユーザー モードのディスプレイ ドライバー](initializing-communication-with-the-direct3d-user-mode-display-driver.md)します。 このキーには、32 ビット Windows Vista で使用されている 32 ビット Windows Vista のディスプレイ ドライバーの 4 つのレジストリ エントリが含まれていて、Windows Vista の 32 ビットの 4 つのエントリは、64 ビット Windows Vista で使用されるドライバーを表示します。 次のエントリは、32 ビット Windows Vista で使用されている 32 ビット Windows Vista のディスプレイ ドライバーのことです。

<span id="UserModeDriverName"></span><span id="usermodedrivername"></span><span id="USERMODEDRIVERNAME"></span>**UserModeDriverName**  
REG\_SZ

オペレーティング システムが、OpenGL ICD をサポートするかどうかに関係なく、Direct3D レンダリング デバイスの操作のために必要な Direct3D ユーザー モード ディスプレイ ドライバーの名前。

<span id="OpenGLDriverName"></span><span id="opengldrivername"></span><span id="OPENGLDRIVERNAME"></span>**OpenGLDriverName**  
REG\_SZ

OpenGL ICD の名前。 たとえば、OpenGL ICD *Mydriver.dll*、このエントリの値が**Mydriver.dll**します。

<span id="OpenGLVersion"></span><span id="openglversion"></span><span id="OPENGLVERSION"></span>**OpenGLVersion**  
REG\_DWORD

OpenGL のランタイムを使用して OpenGL ICD のバージョンを検証する OpenGL ICD のバージョン番号。

<span id="OpenGLFlags"></span><span id="openglflags"></span><span id="OPENGLFLAGS"></span>**OpenGLFlags**  
REG\_DWORD

フラグのビット マスク。 現時点では、ビット 0 (0x00000001) は、互換性を設定されています。 ビット 1 (0x00000002) が設定されている場合、OpenGL のランタイムは呼び出しません ICD の finish 関数ランタイムが ICD のスワップ バッファー関数を呼び出す前にします。

次のエントリは、64 ビット Windows Vista で使用されている 32 ビット Windows Vista のディスプレイ ドライバーのことです。

<span id="UserModeDriverNameWow"></span><span id="usermodedrivernamewow"></span><span id="USERMODEDRIVERNAMEWOW"></span>**UserModeDriverNameWow**  
REG\_SZ

32 ビット Microsoft Direct3D のユーザー モードの名前は、64 ビット Windows Vista のドライバーを表示します。

<span id="OpenGLDriverNameWow"></span><span id="opengldrivernamewow"></span><span id="OPENGLDRIVERNAMEWOW"></span>**OpenGLDriverNameWow**  
REG\_SZ

64 ビット Windows Vista の 32 ビットの OpenGL ICD の名前。

<span id="OpenGLVersionWow"></span><span id="openglversionwow"></span><span id="OPENGLVERSIONWOW"></span>**OpenGLVersionWow**  
REG\_DWORD

64 ビット Windows Vista の 32 ビットの OpenGL ICD のバージョン番号。

<span id="OpenGLFlagsWow"></span><span id="openglflagswow"></span><span id="OPENGLFLAGSWOW"></span>**OpenGLFlagsWow**  
REG\_DWORD

64 ビット Windows Vista の 32 ビットの OpenGL ICD のフラグ ビットマスクを指定します。

 

 





