---
title: Multiplane オーバーレイ VidPN プレゼンテーション
ms.assetid: BAD7FD48-905D-4547-8C69-133240B39FA3
description: 複数のサーフェスに存在するために使用する関数に適用される要件。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ea8a5bd67758f98cd2c0337b58613a84201dc59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536128"
---
# <a name="multiplane-overlay-vidpn-presentation"></a>Multiplane オーバーレイ VidPN プレゼンテーション


Multiplane オーバーレイを使用している場合は、関数が存在するネットワークのビデオ (VidPNs) 内の複数のサーフェスに存在するために使用するこれらの要件が適用されます。

<span id="DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay"></span><span id="dxgkddisetvidpnsourceaddresswithmultiplaneoverlay"></span><span id="DXGKDDISETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY"></span>[*DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay*](https://msdn.microsoft.com/library/windows/hardware/hh780298)  
-   場合[ **DXGK\_MULTIPLANE\_オーバーレイ\_平面**](https://msdn.microsoft.com/library/windows/hardware/hh780305).**有効になっている**が false の場合、ディスプレイのミニポート ドライバーには、指定した平面が無効にする必要があります。
-   以前の呼び出し、平面を有効にしたかどうか[ *DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay* ](https://msdn.microsoft.com/library/windows/hardware/hh780298)ですが、現在の呼び出しには存在しない、ドライバーはなくプレーンを表示する続行する必要がありますこれを反転します。
-   ドライバーが複数の呼び出しを受信することは[ *DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay* ](https://msdn.microsoft.com/library/windows/hardware/hh780298)同じの垂直同期中に (1 回の呼び出しを 1 つの平面を反転するのには、反転する別の呼び出し、さまざまな面)。 ここでは、ドライバーは、両方の呼び出しを処理する必要があります。
-   信頼できるソースでのユーザー モードで渡されるデータを検証されている必要があります。 ただし、ディスプレイのミニポート ドライバーでは、問題が原因であることを確認するデータがチェックもする必要があります。 呼び出し、データが正しくない場合、ドライバーに失敗する可能性を**状態\_無効な\_パラメーター**適切に処理されない可能性があります、エラー コードがこのようなエラーと、オペレーティング システムまたは、いずれかのバグを示すもので、ユーザー モード ドライバー。

<span id="DxgkDdiSetVidPnSourceVisibility"></span><span id="dxgkddisetvidpnsourcevisibility"></span><span id="DXGKDDISETVIDPNSOURCEVISIBILITY"></span>[*DxgkDdiSetVidPnSourceVisibility*](https://msdn.microsoft.com/library/windows/hardware/ff560771)  
ときに[ **DXGKARG\_SETVIDPNSOURCEVISIBILITY**](https://msdn.microsoft.com/library/windows/hardware/ff559486).**表示される**に設定されている**FALSE**でこの関数の呼び出しで指定したソースは、すべてのハードウェア面する必要があります無効にする、レイヤーの主なサーフェイスでの使用を含むです。 ときに**Visible**に設定されている**TRUE**、プライマリのサーフェイスでの使用、プレーンのみを有効にする必要があります、および他のすべての平面無効のままにする必要があります。

<span id="DxgkDdiSetVidPnSourceAddress"></span><span id="dxgkddisetvidpnsourceaddress"></span><span id="DXGKDDISETVIDPNSOURCEADDRESS"></span>[*DxgkDdiSetVidPnSourceAddress*](https://msdn.microsoft.com/library/windows/hardware/ff560767)  
この関数が呼び出されると、ドライバーはすべての非プライマリ オーバーレイ平面を無効にする必要があります。 使用して、プライマリの画面が反転される[ *DxgkDdiSetVidPnSourceAddressWithMultiPlaneOverlay* ](https://msdn.microsoft.com/library/windows/hardware/hh780298) multiplane オーバーレイ モードの場合にします。

 

 





