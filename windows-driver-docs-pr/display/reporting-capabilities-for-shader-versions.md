---
title: シェーダー バージョンの機能のレポート
description: シェーダー バージョンの機能のレポート
ms.assetid: a82ac539-1386-417a-a64f-0a7ddc6d28d9
keywords:
- シェーダー WDK DirectX 9.0
- 頂点シェーダー WDK DirectX 9.0
- ピクセル シェーダー WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5db7ce746ff7868b7535b2bee67a96924c065a41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571625"
---
# <a name="reporting-capabilities-for-shader-versions"></a>シェーダー バージョンの機能のレポート


## <span id="ddk_reporting_capabilities_for_shader_versions_gg"></span><span id="DDK_REPORTING_CAPABILITIES_FOR_SHADER_VERSIONS_GG"></span>


2.0 または 3.0 以降のピクセルまたは頂点シェーダーのバージョンをサポートしているディスプレイ デバイスの DirectX 9.0 バージョンのドライバーでは、デバイスをシェーダーのバージョンにバインドするには機能の最小セットをサポートしているを示す必要があります。 ドライバーは、機能のサポートを示すため D3DCAPS9 構造体のメンバーを設定する必要があります。 ドライバーへの応答で D3DCAPS9 構造体を返す、 **GetDriverInfo2** 」の説明に従って D3DCAPS8 構造体を返すにする方法と同様にクエリ[DirectX 8.0 スタイル Direct3D の機能を Reporting](reporting-directx-8-0-style-direct3d-capabilities.md)します。 このクエリのサポートについては、「[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。 これらの機能は、次のトピックについて説明します。

[シェーダー 2 のサポートに対するレポート機能](reporting-capabilities-for-shader-2-support.md)

[Shader 3 のサポートに対するレポート機能](reporting-capabilities-for-shader-3-support.md)

 

 





