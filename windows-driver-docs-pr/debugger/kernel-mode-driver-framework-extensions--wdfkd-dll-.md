---
title: Windows ドライバー フレームワークの拡張機能 (Wdfkd.dll)
description: Windows ドライバー フレームワークの拡張機能 (Wdfkd.dll)
ms.assetid: 2fa2b131-f6fd-459b-a4e3-799246076338
keywords:
- カーネル モード ドライバー フレームワークの拡張機能 (wdfkd.dll) をデバッグします。
- カーネル モード ドライバー フレームワークの拡張機能 (wdfkd.dll)
- wdfkd.dll (カーネル モード ドライバー フレームワークの拡張機能)
- カーネル モード ドライバー フレームワークの拡張機能
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60d86f7b5473e3d39375fa7f5bfd571535f8782f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553143"
---
# <a name="windows-driver-framework-extensions-wdfkddll"></a>Windows ドライバー フレームワークの拡張機能 (Wdfkd.dll)


カーネル モード ドライバー フレームワーク (KMDF) またはユーザー モード ドライバー フレームワーク (UMDF 2) のバージョン 2 で作成されたドライバーのデバッグに役立つ拡張機能のコマンドは、Wdfkd.dll で実装されます。

これらの拡張機能は、Microsoft Windows XP 以降のオペレーティング システムで使用できます。 一部の拡張機能がある追加の制限これらの制限は、個々 のリファレンス ページに記載されています。

**注**  新しい KMDF または UMDF ドライバーを作成するときに、32 文字のあるドライバー名を選択する必要がありますまたはそれ以下。 この長さの制限は、wdfglobals.h で定義されています。 ドライバー名は、最大長を超えている場合、ドライバーは読み込みに失敗します。

 

これらの拡張機能を使用する方法の詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

 

 





