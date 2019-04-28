---
title: EngExtCpp 拡張機能の構築
description: EngExtCpp 拡張機能の構築
ms.assetid: 63d73c4e-03b8-4bbe-9c2e-96cda3ad544c
keywords:
- EngExtCpp 拡張機能の構築
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84a512e56167b719808be5271fe45ca21d83308b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374048"
---
# <a name="building-engextcpp-extensions"></a>EngExtCpp 拡張機能の構築


## <span id="ddk_building_dbgeng_extensions_dbx"></span><span id="DDK_BUILDING_DBGENG_EXTENSIONS_DBX"></span>


EngExtCpp 拡張ライブラリは、DbgEng の拡張機能ライブラリとほぼ同じ方法で構築されます。 詳細については、次を参照してください。 [DbgEng 拡張機能の作成](building-dbgeng-extensions.md)です。

EngExtCpp 実装コード (engextcpp.cpp) は、スタティック ライブラリとリンクの代わりに使用されます。

EngExtCpp 拡張機能フレームワークが DbgEng 拡張機能フレームワークの上に構築されている、ため EngExtCpp 拡張 DLL は DbgEng 拡張 DLL として同じ関数をエクスポートする必要があります。

各拡張機能をエクスポートする必要があります。 使用すると、 [ **EXT\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/ff544514)マクロも拡張関数でこのマクロを定義する、拡張機能と同じ名前で C の関数を作成します。 この関数は DLL からエクスポートする必要があります。

次の関数が用意されて engextcpp EngExtCpp DLL からエクスポートする必要があります。

-   **DebugExtensionInitialize**ように--、 [**初期化**](https://msdn.microsoft.com/library/windows/hardware/ff550945)ライブラリを初期化するメソッドを呼び出すことができます。

-   **DebugExtensionUnitialize**ように--、 [**非**](https://msdn.microsoft.com/library/windows/hardware/ff558961)ライブラリを初期化するメソッドを呼び出すことができます。

-   **KnownStructOutputEx** --エンジンを呼び出すことができますができるように、 [ *ExtKnownStructMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff543989)構造体が既知の出力を書式設定する方法。

-   **DebugExtensionNotify** --エンジンを呼び出すことができますができるように、 [ **OnSessionActive**](https://msdn.microsoft.com/library/windows/hardware/ff552312)、 **OnSessionInactive**、 **OnSessionAccessible**、および**OnSessionInaccessible**デバッグ セッションの状態の変更の拡張機能ライブラリに通知するメソッド。

-   **ヘルプ**--EngExtCpp 拡張機能フレームワークが自動的に提供できるように、 **! ヘルプ**拡張機能。

提供される機能が必要でない場合でも、これらの関数をエクスポートできます。 さらに、エクスポートされない場合は、提供される機能が失われます。

**DebugExtensionInitialize**デバッガー エンジンとして有効な DbgEng 拡張 DLL、DLL を認識するためにエクスポートする必要があります。

 

 





