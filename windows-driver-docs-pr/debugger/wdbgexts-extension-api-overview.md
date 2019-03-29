---
title: WdbgExts 拡張機能 API の概要
description: WdbgExts 拡張機能 API の概要
ms.assetid: e54d330f-ab48-407f-a9f2-e4a521f5e27b
keywords:
- WdbgExts 拡張機能、概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4abcdb6db8fdbbbd4222229cf74c5bfa9f9e704
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577931"
---
# <a name="wdbgexts-extension-api-overview"></a>WdbgExts 拡張機能 API の概要


## <span id="ddk_wdbgexts_extension_api_overview_dbwx"></span><span id="DDK_WDBGEXTS_EXTENSION_API_OVERVIEW_DBWX"></span>


各 WdbgExts 拡張 DLL は、実装するために使用される 1 つまたは複数の関数をエクスポートします。*拡張コマンド*します。 これらの関数は C の標準の規則に従ってという名前が、大文字が許可されていません。

関数名と拡張機能コマンド名は同じですが、拡張機能のコマンドは、感嘆符が開始される点を除いて ( **!** ). たとえばと Myextension.dll をデバッガーに読み込むし、入力した **! スタック**デバッガー コマンド ウィンドウに、デバッガーがという名前のエクスポートされた関数を検索**スタック**Myextension.dll で。

Myextension.dll が既に読み込まれていないかどうか、またはその他の拡張 Dll で同じ名前を持つその他の拡張機能コマンドがある場合は、入力 **! myextension.stack**拡張 DLL を示すデバッガー コマンド ウィンドウに、この DLL 内の拡張機能コマンド。

各 WdbgExts 拡張 DLL の数をエクスポート*コールバック関数*します。 拡張機能のコマンドを使用する場合と、DLL が読み込まれるときに、これらの関数がデバッガーによって呼び出されます。

デバッガー エンジンは配置を**試用/を除く**拡張 DLL への呼び出しの周囲にブロックします。 これにより、拡張機能コードのバグの一部の種類から、エンジンが保護されます。 ただし、拡張機能の呼び出しは、エンジンと同じスレッドで実行される、ためクラッシュするエンジンまだことができます。

 

 





