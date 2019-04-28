---
title: カーネルモード ドライバー フレームワークのデバッグ
description: カーネルモード ドライバー フレームワークのデバッグ
ms.assetid: bec840f8-b500-464f-8e49-53f03f34aa6a
keywords:
- カーネル モード ドライバー フレームワークのデバッグ
- Windows Driver Foundation
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 035e3f133e113bb9501413a954a8eb8283bc53c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367200"
---
# <a name="kernel-mode-driver-framework-debugging"></a>カーネルモード ドライバー フレームワークのデバッグ


デバッグ拡張機能のカーネル モード ドライバー フレームワーク (KMDF) Wdfkd.dll の拡張機能ライブラリに格納されます。

KMDF を使用するデバッグ ドライバーに Wdfkd.dll の拡張機能ライブラリを含む拡張機能のコマンドを使用することができます。

Wdfkd.dll で拡張機能コマンドの説明は、次を参照してください。[カーネル モード ドライバー フレームワークの拡張機能 (Wdfkd.dll)](kernel-mode-driver-framework-extensions--wdfkd-dll-.md)します。

これらの拡張機能は、Microsoft Windows XP 以降のオペレーティング システムで使用できます。 一部の拡張機能がある追加の制限これらの制限は、個々 のリファレンス ページに記載されています。

**注**  新しい KMDF ドライバーか UMDF ドライバーを作成する場合、32 文字以下のドライバー名を選ぶ必要があります。 この長さの制限は、wdfglobals.h で定義されています。 ドライバー名は、最大長を超えている場合、ドライバーは読み込みに失敗します。

 

この拡張機能ライブラリを使用するには、デバッガーに、ライブラリを読み込む必要があります。 デバッガーに拡張機能ライブラリを読み込む方法については、次を参照してください。[デバッガー拡張 Dll の読み込み](loading-debugger-extension-dlls.md)します。

 

 





