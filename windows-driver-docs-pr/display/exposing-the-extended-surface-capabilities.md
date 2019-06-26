---
title: 拡張サーフェス機能の公開
description: 拡張サーフェス機能の公開
ms.assetid: 833171f0-e86a-46c9-9596-87b9b292c03c
keywords:
- 描画サーフェイスの拡張機能 WDK DirectDraw、公開します。
- DirectDraw surface の拡張機能 WDK Windows 2000 を表示するを公開します。
- WDK の DirectDraw surface の機能を拡張し公開します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36f362f261552349b741c3fd7c58347d1b833def
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381889"
---
# <a name="exposing-the-extended-surface-capabilities"></a>拡張サーフェス機能の公開


## <span id="ddk_exposing_the_extended_surface_capabilities_gg"></span><span id="DDK_EXPOSING_THE_EXTENDED_SURFACE_CAPABILITIES_GG"></span>


[ **DDCORECAPS** ](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)構造に含まれる、 [ **DDSCAPS** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))フィールドをサポートするサーフェスの種類を示すためにどのドライバーを入力します。 これらの上限がアプリケーションに報告されると、DDCAPS、若干異なる構造体が返されます。 この DDCAPS 構造体がドライバーの DDCORECAPS およびを使用してクエリ実行されるその他の構造から構築された、 [ **DdGetDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)インターフェイス。 DirectX の最新バージョンにはアプリケーションに表示される DDCAPS が含まれています、 [ **DDSCAPS2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))メンバー。 この DDCAPS2 メンバーが DDCORECAPS 構造体で DDSCAPS メンバーから構築された、 **ddsCapsMore**のメンバー、 [ **DD\_MORESURFACECAPS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_moresurfacecaps)構造体。

DD\_MORESURFACECAPS 構造が使用して初期化時にドライバーをドライバーからクエリを実行、 *DdGetDriverInfo*呼び出します。 定義されている、適切な GUID *ddrawint.h*、GUID は、\_DDMoreSurfaceCaps します。

GUID に応答して\_DDMoreSurfaceCaps クエリは完全に省略可能です。 2 つの個別の作業を行うドライバーを許可するものでは。

-   表示メモリにドライバーを作成できるサーフェスの拡張機能を公開します。

-   DirectDraw surface これらの拡張機能の新しいヒープの制限に express します。

最初の項目は、前のセクションでカバーされていたし、自己記述的です。 2 番目の項目はより複雑であり、読者は、の重要性について熟知する必要があります、 **ddsCaps**と**ddsCapsAlt**のメンバー、 [**グラフィックスアクセラレータ**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_videomemory)で説明されている構造[メモリ ヒープ割り当て](memory-heap-allocation.md)、次のセクションを読む前にします。

 

 





