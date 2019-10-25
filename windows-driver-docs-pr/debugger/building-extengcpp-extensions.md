---
title: EngExtCpp 拡張機能の構築
description: EngExtCpp 拡張機能の構築
ms.assetid: 63d73c4e-03b8-4bbe-9c2e-96cda3ad544c
keywords:
- EngExtCpp 拡張機能, ビルド
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e5372cfffba989313f5f0574dda046844396007
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837829"
---
# <a name="building-engextcpp-extensions"></a>EngExtCpp 拡張機能の構築


## <span id="ddk_building_dbgeng_extensions_dbx"></span><span id="DDK_BUILDING_DBGENG_EXTENSIONS_DBX"></span>


EngExtCpp 拡張ライブラリは、DbgEng 拡張ライブラリとほぼ同じように構築されています。 詳細については、「 [DbgEng 拡張機能のビルド](building-dbgeng-extensions.md)」を参照してください。

EngExtCpp 実装コード (EngExtCpp) は、スタティックライブラリとリンクする代わりに使用されます。

EngExtCpp extension framework は DbgEng 拡張機能フレームワークの上に構築されているため、EngExtCpp extension DLL は DbgEng 拡張 DLL と同じ関数をエクスポートする必要があります。

各拡張機能をエクスポートする必要があります。 [**EXT\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/engextcpp/nf-engextcpp-ext_command)マクロを使用して拡張関数を定義すると、このマクロによって、拡張機能と同じ名前の C 関数も作成されます。 この関数は DLL からエクスポートする必要があります。

Engextcpp によって提供される次の関数は、EngExtCpp DLL からエクスポートする必要があります。

-   **Debugextensioninitialize** -- [**initialize**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))メソッドを呼び出してライブラリを初期化できるようにします。

-   **DebugExtensionUnitialize** --[**初期化**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff558961(v=vs.85))されていないメソッドを呼び出して、ライブラリを初期化解除できます。

-   **KnownStructOutputEx** --エンジンが[*ExtKnownStructMethod*](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))メソッドを呼び出して、既知の構造体の出力を書式設定できるようにします。

-   **Debugextensionnotify** --エンジンが[**onsessionactive**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552312(v=vs.85))、 **onsessionactive**、 **Onsessionactive 可能**、および**onsessionactive**の各メソッドを呼び出して、変更の変更を拡張ライブラリに通知できるようにします。セッションの状態をデバッグしています。

-   **help** --EngExtCpp extension framework が **! help**拡張機能を自動的に提供できるようにします。

これらの関数は、提供される機能が不要な場合でもエクスポートできます。 さらに、エクスポートされていない場合、提供される機能は失われます。

デバッガーエンジンが DLL を有効な DbgEng 拡張 DLL として認識できるようにするには、 **Debugextensioninitialize**をエクスポートする必要があります。

 

 





