---
title: OpenGL のインストール可能なクライアント ドライバーの読み込み
description: OpenGL のインストール可能なクライアント ドライバーの読み込み
ms.assetid: 2b244bbf-f26c-4307-a347-a29e12c6d496
keywords:
- OpenGL ICD WDK ディスプレイ
- ドライバーの読み込みの WDK 表示
- の場合 WDK の表示
- インストール可能なクライアントドライバーの WDK ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a03d3197418eca3b5d71cfa09b655a3b7f17be8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840602"
---
# <a name="loading-an-opengl-installable-client-driver"></a>OpenGL のインストール可能なクライアント ドライバーの読み込み


OpenGL ランタイムはレジストリにアクセスして、読み込む OpenGL インストール可能なクライアントドライバー (ICD) を決定します。 Opengl ICD、OpenGL ランタイムを読み込むには、次のようにします。

-   [**D3DKMTQueryAdapterInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtqueryadapterinfo)関数を呼び出して、OpenGL ICD に関連付けられている名前、バージョン、およびフラグを決定します。 KMTQAITYPE\_UMOPENGLINFO 値は、 *pData*パラメーターが指す[**D3DKMT\_Queryadapterinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_queryadapterinfo)構造体の**Type**メンバーで設定されています。

-   OpenGL ICD のバージョンを検証するために**D3DKMTQueryAdapterInfo**が返す opengl icd のバージョン番号を確認します。

-   Opengl ICD の名前を使用して、OpenGL ICD を読み込みます。

-   OpenGL ICD の機能へのアクセスを初期化します。
    **注**   Opengl ICD Development Kit のライセンスを取得するには、 [opengl の問題](mailto:opengl@microsoft.com)チームにお問い合わせください。

     

OpenGL ICD の名前を検索するために、 [**D3DKMTQueryAdapterInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtqueryadapterinfo)は次のキーでレジストリを検索します。

```registry
HKLM/System/CurrentControlSet/Control/Class/{Adapter GUID}/0000/
```

このキーには、 [Microsoft Direct3D ユーザーモード表示ドライバー](initializing-communication-with-the-direct3d-user-mode-display-driver.md)の名前も含まれています。 このキーには、32ビットの windows vista で使用される32ビットの windows vista ディスプレイドライバの4つのレジストリエントリが含まれています。これは、64ビットの windows vista で使用される、32ビットの Windows Vista 表示ドライバーの4つのエントリです。 次のエントリは、32ビットの Windows Vista で使用される32ビットの Windows Vista ディスプレイドライバー用です。

<span id="UserModeDriverName"></span><span id="usermodedrivername"></span><span id="USERMODEDRIVERNAME"></span>**UserModeDriverName**  
REG\_SZ

Direct3D ユーザーモード表示ドライバーの名前。オペレーティングシステムで OpenGL ICD がサポートされているかどうかに関係なく、Direct3D レンダリングデバイスの操作に必要です。

<span id="OpenGLDriverName"></span><span id="opengldrivername"></span><span id="OPENGLDRIVERNAME"></span>**OpenGLDriverName**  
REG\_SZ

OpenGL ICD の名前。 たとえば、OpenGL ICD が*mydriver .dll*の場合、このエントリの値は**mydriver**.dll になります。

<span id="OpenGLVersion"></span><span id="openglversion"></span><span id="OPENGLVERSION"></span>**OpenGLVersion**  
REG\_DWORD

Opengl ランタイムが OpenGL ICD のバージョンを検証するために使用する OpenGL ICD のバージョン番号。

<span id="OpenGLFlags"></span><span id="openglflags"></span><span id="OPENGLFLAGS"></span>**OpenGLFlags**  
REG\_DWORD

フラグビットマスク。 現在、ビット 0 (0x00000001) は互換性のために設定されています。 ビット 1 (0x00000002) が設定されている場合、ランタイムが ICD のスワップバッファー関数を呼び出す前に、OpenGL ランタイムは ICD の finish 関数を呼び出しません。

次のエントリは、64ビットの Windows Vista で使用される32ビットの Windows Vista ディスプレイドライバー用です。

<span id="UserModeDriverNameWow"></span><span id="usermodedrivernamewow"></span><span id="USERMODEDRIVERNAMEWOW"></span>**UserModeDriverNameWow**  
REG\_SZ

64ビット Windows Vista 用の32ビット Microsoft Direct3D ユーザーモード表示ドライバーの名前。

<span id="OpenGLDriverNameWow"></span><span id="opengldrivernamewow"></span><span id="OPENGLDRIVERNAMEWOW"></span>**OpenGLDriverNameWow**  
REG\_SZ

64ビット Windows Vista の32ビット OpenGL ICD の名前。

<span id="OpenGLVersionWow"></span><span id="openglversionwow"></span><span id="OPENGLVERSIONWOW"></span>**OpenGLVersionWow**  
REG\_DWORD

64ビット Windows Vista の32ビット OpenGL ICD のバージョン番号。

<span id="OpenGLFlagsWow"></span><span id="openglflagswow"></span><span id="OPENGLFLAGSWOW"></span>**OpenGLFlagsWow**  
REG\_DWORD

64ビット Windows Vista の32ビット OpenGL ICD のフラグビットマスク。

 

 





