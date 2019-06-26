---
title: EngExtCpp 拡張機能の構築
description: EngExtCpp 拡張機能の構築
ms.assetid: 63d73c4e-03b8-4bbe-9c2e-96cda3ad544c
keywords:
- EngExtCpp 拡張機能の構築
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff36fbc9b815719f26518dfabdd08db1af403f48
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361471"
---
# <a name="building-engextcpp-extensions"></a>EngExtCpp 拡張機能の構築


## <span id="ddk_building_dbgeng_extensions_dbx"></span><span id="DDK_BUILDING_DBGENG_EXTENSIONS_DBX"></span>


EngExtCpp 拡張ライブラリは、DbgEng の拡張機能ライブラリとほぼ同じ方法で構築されます。 詳細については、次を参照してください。 [DbgEng 拡張機能の作成](building-dbgeng-extensions.md)です。

EngExtCpp 実装コード (engextcpp.cpp) は、スタティック ライブラリとリンクの代わりに使用されます。

EngExtCpp 拡張機能フレームワークが DbgEng 拡張機能フレームワークの上に構築されている、ため EngExtCpp 拡張 DLL は DbgEng 拡張 DLL として同じ関数をエクスポートする必要があります。

各拡張機能をエクスポートする必要があります。 使用すると、 [ **EXT\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/nf-engextcpp-ext_command)マクロも拡張関数でこのマクロを定義する、拡張機能と同じ名前で C の関数を作成します。 この関数は DLL からエクスポートする必要があります。

次の関数が用意されて engextcpp EngExtCpp DLL からエクスポートする必要があります。

-   **DebugExtensionInitialize**ように--、 [**初期化**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))ライブラリを初期化するメソッドを呼び出すことができます。

-   **DebugExtensionUnitialize**ように--、 [**非**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff558961(v=vs.85))ライブラリを初期化するメソッドを呼び出すことができます。

-   **KnownStructOutputEx** --エンジンを呼び出すことができますができるように、 [ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))構造体が既知の出力を書式設定する方法。

-   **DebugExtensionNotify** --エンジンを呼び出すことができますができるように、 [ **OnSessionActive**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552312(v=vs.85))、 **OnSessionInactive**、 **OnSessionAccessible**、および**OnSessionInaccessible**デバッグ セッションの状態の変更の拡張機能ライブラリに通知するメソッド。

-   **ヘルプ**--EngExtCpp 拡張機能フレームワークが自動的に提供できるように、 **! ヘルプ**拡張機能。

提供される機能が必要でない場合でも、これらの関数をエクスポートできます。 さらに、エクスポートされない場合は、提供される機能が失われます。

**DebugExtensionInitialize**デバッガー エンジンとして有効な DbgEng 拡張 DLL、DLL を認識するためにエクスポートする必要があります。

 

 





