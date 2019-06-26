---
title: デスクトップ管理
description: デスクトップ管理
ms.assetid: 68ae302b-a39e-4aff-8be7-52081c318c9e
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、デスクトップ管理
- デスクトップ管理 WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81328e656ac42b56ad857fa733f3b95c00b5839a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384891"
---
# <a name="desktop-management"></a>デスクトップ管理


## <span id="ddk_desktop_management_gg"></span><span id="DDK_DESKTOP_MANAGEMENT_GG"></span>


ディスプレイ ドライバーを実装する必要があります[ **DrvAssertMode** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvassertmode)と[ **DrvGetModes** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetmodes)デスクトップを管理します。

ディスプレイ ドライバーは、パレットで管理された場合への呼び出しは受信も[ **DrvSetPalette** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpalette)パレットを適切な状態にリセットします。

動的モードの変更を処理するための GDI のメカニズムは、Windows 2000 以降のオペレーティング システムのバージョンで大幅に変更されました。 モードの変更が完了した後に割り当てられている HDEV からの初期化中にドライバーに割り当てられている GDI HDEV が異なる場合があります。 ディスプレイ ドライバーは、一般にないこの変更による影響を受ける、次の理由です。

-   ドライバーが常に割り当てられている*ppdev -&gt;hdevEng = hdev*でその[ **DrvCompletePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcompletepdev)実装します。

-   ドライバーが常に参照する*ppdev -&gt;hdevEng* HDEV を必要とする任意のコールバックでします。

 

 





