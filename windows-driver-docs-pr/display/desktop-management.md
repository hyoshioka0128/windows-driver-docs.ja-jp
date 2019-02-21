---
title: デスクトップ管理
description: デスクトップ管理
ms.assetid: 68ae302b-a39e-4aff-8be7-52081c318c9e
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、デスクトップ管理
- デスクトップ管理 WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b9c1acb1bfc2933535941d60162c373e3a3801a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539164"
---
# <a name="desktop-management"></a>デスクトップ管理


## <span id="ddk_desktop_management_gg"></span><span id="DDK_DESKTOP_MANAGEMENT_GG"></span>


ディスプレイ ドライバーを実装する必要があります[ **DrvAssertMode** ](https://msdn.microsoft.com/library/windows/hardware/ff556178)と[ **DrvGetModes** ](https://msdn.microsoft.com/library/windows/hardware/ff556233)デスクトップを管理します。

ディスプレイ ドライバーは、パレットで管理された場合への呼び出しは受信も[ **DrvSetPalette** ](https://msdn.microsoft.com/library/windows/hardware/ff556282)パレットを適切な状態にリセットします。

動的モードの変更を処理するための GDI のメカニズムは、Windows 2000 以降のオペレーティング システムのバージョンで大幅に変更されました。 モードの変更が完了した後に割り当てられている HDEV からの初期化中にドライバーに割り当てられている GDI HDEV が異なる場合があります。 ディスプレイ ドライバーは、一般にないこの変更による影響を受ける、次の理由です。

-   ドライバーが常に割り当てられている*ppdev -&gt;hdevEng = hdev*でその[ **DrvCompletePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556181)実装します。

-   ドライバーが常に参照する*ppdev -&gt;hdevEng* HDEV を必要とする任意のコールバックでします。

 

 





