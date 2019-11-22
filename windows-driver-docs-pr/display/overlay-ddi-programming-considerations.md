---
title: オーバーレイ DDI のプログラミングに関する考慮事項
description: オーバーレイ DDI のプログラミングに関する考慮事項
ms.assetid: 887624a7-0293-4add-94a7-d490ebd93205
keywords:
- オーバーレイ DDI WDK Windows 7 の表示、プログラミングに関する考慮事項
- オーバーレイ DDI WDK サーバー 2008 R2 の表示、プログラミングに関する考慮事項
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31390ab118f7999bce950a3cf374cdf994f41211
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829891"
---
# <a name="overlay-ddi-programming-considerations"></a>オーバーレイ DDI のプログラミングに関する考慮事項


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

ユーザーモード表示ドライバーに[オーバーレイ DDI](overlay-ddi.md)を実装する場合は、次のプログラミングのヒントを考慮する必要があります。

-   ドライバーがオーバーレイ DDI をサポートしている場合は、 [D3DCAPS9](https://go.microsoft.com/fwlink/p/?linkid=122122)構造体の**CAPS**メンバーで D3DCAPS\_オーバーレイビットを設定する必要があります。 D3DCAPS9 構造体については、DirectX 9.0 SDK のドキュメントを参照してください。 このドライバーは、D3DDDICAPS\_GETD3D9CAPS 値が[**D3DDDIARG\_getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)構造体の**型**メンバーで設定さ*れている* [**getcaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)関数の呼び出しに応答して、D3DCAPS\_オーバーレイビットを設定します。

-   表示形式が32ビットではなく64ビットである場合 (たとえば、DWM が表示モードで[**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)列挙から D3DDDIFMT\_A16B16G16R16F 値を使用している場合)、Direct3D ランタイムはオーバーレイカラーキーの低32ビットをに配置します。[**D3DDDI\_OVERLAYINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_overlayinfo)構造体の**Dstcolorkeylow**メンバーと**D3DDDI\_OVERLAYINFO**の**dstcolorkeylow**メンバーの上位32ビット。

 

 





