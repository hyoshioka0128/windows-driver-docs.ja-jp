---
title: ユーザー モード ディスプレイ ドライバーでの回転のサポート
description: ユーザー モード ディスプレイ ドライバーでの回転のサポート
ms.assetid: fb80e875-26d4-4928-9268-2c6b36bb5d20
keywords:
- ユーザー モード ドライバー WDK Windows Vista では、回転の表示します。
- WDK の表示の回転
- 画面の回転 WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da3a606fc565e59588441884cb1e21ccaf8d50a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578087"
---
# <a name="supporting-rotation-in-a-user-mode-display-driver"></a>ユーザー モード ディスプレイ ドライバーでの回転のサポート


ユーザー モードのディスプレイ ドライバーは、多くの要因に応じて異なる方法で、回転をサポートします。 たとえば、ユーザー モードのディスプレイ ドライバーする必要があります動作を全画面表示のデバイスはウィンドウのデバイスの場合よりも。 また、プライマリ サーフェスの作成は、デスクトップ ウィンドウ マネージャー (DWM) を実行しているかどうかに基づいて異なる方法で、グラフィックス アダプターには、Microsoft DirectX 9 L、または DirectX 9 L がサポートしているアプリケーションは回転に注意してください。

次のトピックでは、ユーザー モードのディスプレイ ドライバーがさまざまな状況の回転をサポートする方法について説明します。

[ウィンドウ表示モードの動作](windowed-mode-behavior.md)

[全画面-モードの動作](full-screen-mode-behavior.md)

[DirectX のランタイム動作](directx-runtime-behavior.md)

 

 





