---
title: 画面の拡張機能を公開します。
description: 画面の拡張機能を公開します。
ms.assetid: 833171f0-e86a-46c9-9596-87b9b292c03c
keywords:
- 描画サーフェイスの拡張機能 WDK DirectDraw、公開します。
- DirectDraw surface の拡張機能 WDK Windows 2000 を表示するを公開します。
- WDK の DirectDraw surface の機能を拡張し公開します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db1f1b89d3f6c2d508036d42090dab67f855784c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527435"
---
# <a name="exposing-the-extended-surface-capabilities"></a>画面の拡張機能を公開します。


## <span id="ddk_exposing_the_extended_surface_capabilities_gg"></span><span id="DDK_EXPOSING_THE_EXTENDED_SURFACE_CAPABILITIES_GG"></span>


[ **DDCORECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549248)構造に含まれる、 [ **DDSCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff550286)フィールドをサポートするサーフェスの種類を示すためにどのドライバーを入力します。 これらの上限がアプリケーションに報告されると、DDCAPS、若干異なる構造体が返されます。 この DDCAPS 構造体がドライバーの DDCORECAPS およびを使用してクエリ実行されるその他の構造から構築された、 [ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)インターフェイス。 DirectX の最新バージョンにはアプリケーションに表示される DDCAPS が含まれています、 [ **DDSCAPS2** ](https://msdn.microsoft.com/library/windows/hardware/ff550292)メンバー。 この DDCAPS2 メンバーが DDCORECAPS 構造体で DDSCAPS メンバーから構築された、 **ddsCapsMore**のメンバー、 [ **DD\_MORESURFACECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff551659)構造体。

DD\_MORESURFACECAPS 構造が使用して初期化時にドライバーをドライバーからクエリを実行、 *DdGetDriverInfo*呼び出します。 定義されている、適切な GUID *ddrawint.h*、GUID は、\_DDMoreSurfaceCaps します。

GUID に応答して\_DDMoreSurfaceCaps クエリは完全に省略可能です。 2 つの個別の作業を行うドライバーを許可するものでは。

-   表示メモリにドライバーを作成できるサーフェスの拡張機能を公開します。

-   DirectDraw surface これらの拡張機能の新しいヒープの制限に express します。

最初の項目は、前のセクションでカバーされていたし、自己記述的です。 2 番目の項目はより複雑であり、読者は、の重要性について熟知する必要があります、 **ddsCaps**と**ddsCapsAlt**のメンバー、 [**グラフィックスアクセラレータ**](https://msdn.microsoft.com/library/windows/hardware/ff570171)で説明されている構造[メモリ ヒープ割り当て](memory-heap-allocation.md)、次のセクションを読む前にします。

 

 





