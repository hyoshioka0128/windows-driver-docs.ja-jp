---
title: Direct3D の機能および WDDM 1.2 での要件
description: マイクロソフトの Direct3D には、3-D グラフィックス、複雑な視覚化とゲーム開発ソフトウェア アプリケーションで広く使用されている Api の豊富なコレクションが用意されています。
ms.assetid: 8A40276D-FAE3-4433-A3E5-573700331B07
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32befb6229afe1856f6dad3c66db68867b29f796
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560831"
---
# <a name="direct3d-features-and-requirements-in-wddm-12"></a>Direct3D の機能および WDDM 1.2 での要件


マイクロソフトの Direct3D には、3-D グラフィックス、複雑な視覚化とゲーム開発ソフトウェア アプリケーションで広く使用されている Api の豊富なコレクションが用意されています。 このセクションでは、機能の改善と Windows 8 の Direct3D ソフトウェアおよびハードウェア要件について説明します。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションでは


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="directx-feature-improvements-in-windows-8.md" data-raw-source="[DirectX feature improvements in Windows 8](directx-feature-improvements-in-windows-8.md)">Windows 8 での DirectX 機能の改善</a></p></td>
<td align="left"><p>Windows 8 には、開発者、エンドユーザーおよびシステムの製造元の利点を得られる Microsoft DirectX の機能強化が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="software-requirements.md" data-raw-source="[Direct3D software requirements in Windows 8](software-requirements.md)">Windows 8 で Direct3D ソフトウェア要件</a></p></td>
<td align="left"><p>このトピックでは、Windows 8 で Direct3D をサポートするためのソフトウェア要件について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="hardware-requirements.md" data-raw-source="[Hardware requirements](hardware-requirements.md)">ハードウェア要件</a></p></td>
<td align="left"><p>このトピックでは、Windows 8 で Direct3D をサポートするためのハードウェア要件について説明します。</p></td>
</tr>
</tbody>
</table>

 

グラフィックス アダプターの機能に応じては、Direct3D は、アプリケーションを全体の 3-D レンダリング パイプラインまたは部分的なアクセラレータ ハードウェア アクセラレーションを利用できます。 新しいバージョンの Direct3D 9Ex などの Direct3D Api と Microsoft direct3d10 Windows 表示 Driver Model (WDDM) の機能に必要なディスプレイ ドライバー インターフェイスを提供するため、Windows Vista でのみ開始を利用します。 この図は、WDDM のさまざまなバージョンでサポートされている Direct3D Api の増分バージョンを示しています。

![wddm のさまざまなバージョンでサポートされている direct3d api](images/direct3dapissupportedwddm.jpg)

**WDDM のさまざまなバージョンでサポートされている Direct3D Api**

 

 





