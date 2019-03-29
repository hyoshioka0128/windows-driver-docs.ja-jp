---
title: DirectX 9.0 ドライバーの推奨されるサポート
description: DirectX 9.0 ドライバーの推奨されるサポート
ms.assetid: 57b4dac8-c694-47ec-b5f9-19247b4de433
keywords:
- 使用されていないチャネル WDK DirectX 9.0 の既定値します。
- チャネルの既定値 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0240c934f019cea6514bfe7d459a8f9be264fb70
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571017"
---
# <a name="recommended-directx-90-driver-support"></a>DirectX 9.0 ドライバーの推奨されるサポート


## <span id="ddk_recommended_directx_9_0_driver_support_gg"></span><span id="DDK_RECOMMENDED_DIRECTX_9_0_DRIVER_SUPPORT_GG"></span>


DirectX 9.0 ドライバーが使用されていないチャネルのテクスチャ形式の既定値を設定することをお勧めします。

### <a name="span-idsettingdefaultsforunusedchannelsoftextureformatsspanspan-idsettingdefaultsforunusedchannelsoftextureformatsspanspan-idsettingdefaultsforunusedchannelsoftextureformatsspansetting-defaults-for-unused-channels-of-texture-formats"></a><span id="Setting_Defaults_for_Unused_Channels_of_Texture_Formats"></span><span id="setting_defaults_for_unused_channels_of_texture_formats"></span><span id="SETTING_DEFAULTS_FOR_UNUSED_CHANNELS_OF_TEXTURE_FORMATS"></span>テクスチャ形式の使用されていないチャネルの既定値の設定

ドライバーとそのデバイスが使用されていないチャネルの既定値をテクスチャ形式でように設定アプリケーションは、入力のテクスチャで提供されていないこれらのチャネルに存在している既知の値に依存できます。

リファレンス ラスタライザー DirectX 8.1 以降のバージョンが、D3DFMT で未使用の B チャネルの既定値を設定する方法と同様に\_1.0f に G16R16 テクスチャ形式 (を参照してください*refrast.cpp*サンプル コード)、DirectX9.0 のバージョンのドライバーは、1.0 f には、次の DirectX 9.0 浮動小数点のテクスチャ形式で使用されていないチャネルの既定値を設定する必要があります。

-   D3DFMT\_R16F

-   D3DFMT\_G16R16F

-   D3DFMT\_R32F

-   D3DFMT\_G32R32F

DirectX 9.0 ドライバーでは、次の既定値は設定も必要があります。

-   アルファ チャネル (A) (透明度) を 1.0 f に対して非透過的です。

-   最大の照度が生成される 1.0f に輝度チャネル (L)。

リファレンス ラスタライザーも B チャネルの既定値また (RGBA) の A チャネルに 1.0f の設定、D3DFMT\_V16U16 形式。 この方法は、D3DFMT で\_V16U16 形式は同じ意味で、D3DFMT\_L6V5U5 形式は、実際には、L、チャネル。 D3DFMT\_L6V5U5 形式、ルミナンスは B チャネルに配置されます。

 

 





