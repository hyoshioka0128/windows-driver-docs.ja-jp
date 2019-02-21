---
title: オーバーレイ DDI プログラミングに関する考慮事項
description: オーバーレイ DDI プログラミングに関する考慮事項
ms.assetid: 887624a7-0293-4add-94a7-d490ebd93205
keywords:
- オーバーレイ DDI WDK Windows 7 の表示、プログラミングの考慮事項
- オーバーレイ DDI WDK Server 2008 R2 の表示、プログラミングの考慮事項
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f49981c4fb3826ecac1f3627ececc12a23f4621f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530704"
---
# <a name="overlay-ddi-programming-considerations"></a>オーバーレイ DDI プログラミングに関する考慮事項


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

実装する場合、[オーバーレイ DDI](overlay-ddi.md)ユーザー モードのディスプレイ ドライバーでは、次のプログラミングのヒントを検討してください。

-   D3DCAPS を設定する必要があります、ドライバーは、オーバーレイ DDI をサポートする場合\_オーバーレイ ビット、 **Cap**のメンバー [D3DCAPS9](https://go.microsoft.com/fwlink/p/?linkid=122122)構造体。 D3DCAPS9 構造体は、DirectX 9.0 SDK ドキュメントで説明します。 ドライバーの設定、D3DCAPS\_オーバーレイ ビットへの呼び出しに応答でその[ **GetCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff566762)関数を D3DDDICAPS\_GETD3D9CAPS 値で設定されます、**型**のメンバー、 [ **D3DDDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff543148)構造体、 *pData*パラメーターを指します。

-   32 ビットではなく、64 ビットの表示形式の場合 (たとえば、DWM が、D3DDDIFMT を使用する場合\_A16B16G16R16F 値から、 [ **D3DDDIFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff544312)表示モードの列挙体)、Direct3D のランタイムでのオーバーレイのカラー キーの下位 32 ビットの配置、 **DstColorKeyLow**のメンバー、 [ **D3DDDI\_OVERLAYINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff544621)構造との上位 32 ビット、 **DstColorKeyHigh**のメンバー **D3DDDI\_OVERLAYINFO**します。

 

 





