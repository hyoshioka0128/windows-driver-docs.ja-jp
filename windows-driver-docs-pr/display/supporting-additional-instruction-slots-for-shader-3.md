---
title: シェーダー 3 の追加の命令スロットのサポート
description: シェーダー 3 の追加の命令スロットのサポート
ms.assetid: 8ff00178-cd08-42ce-8dea-127fc0d04733
keywords:
- WDK DirectX 9.0 の命令スロット
- シェーダー WDK DirectX 9.0
- ピクセル シェーダー WDK DirectX 9.0
- 頂点シェーダー WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1859e6504b6f9eb7664d74864a3a453750efe2f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375904"
---
# <a name="supporting-additional-instruction-slots-for-shader-3"></a>シェーダー 3 の追加の命令スロットのサポート


## <span id="ddk_supporting_additional_instruction_slots_for_shader_3_gg"></span><span id="DDK_SUPPORTING_ADDITIONAL_INSTRUCTION_SLOTS_FOR_SHADER_3_GG"></span>


3.0 以降のピクセルまたは頂点シェーダーのバージョンをサポートしているディスプレイ デバイスは、いずれかのシェーダーの種類の少なくとも 512 命令スロットをサポートする必要があります。 ただし、このディスプレイ デバイスは、いずれかのシェーダーの種類に対して最大 32768 命令スロットをサポートできます。

頂点シェーダー 3.0 用のデバイスをサポートする命令スロット、デバイスのセットの DirectX 9.0 ドライバーの最大数を示すために、 **MaxVertexShader30InstructionSlots** D3DCAPS9 構造体のメンバー、最大数。

デバイスをサポートする、ピクセル シェーダー 3.0 命令スロット、デバイスのセットの DirectX 9.0 ドライバーの最大数を示すために、 **MaxPixelShader30InstructionSlots**最大 D3DCAPS9 構造体のメンバー数です。

命令の最大数は、ピクセルのスロット 3.0 を頂点シェーダーをさまざまなことができるため、DirectX 9.0 ドライバーを設定できます**MaxVertexShader30InstructionSlots**と**MaxPixelShader30InstructionSlots**ごとに異なる値。 ドライバーは、512 32768 の命令スロットの最大数を設定できます。 ドライバーは、いずれかを設定する場合**MaxVertexShader30InstructionSlots**または**MaxPixelShader30InstructionSlots**許容範囲外の値に、ドライバーの読み込みに失敗します。

ドライバーへの応答で D3DCAPS9 構造体を返す、 **GetDriverInfo2** 」の説明に従って D3DCAPS8 構造体を返すにする方法と同様にクエリ[DirectX 8.0 スタイル Direct3D の機能を Reporting](reporting-directx-8-0-style-direct3d-capabilities.md)します。 このクエリのサポートについては、「[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。

 

 





