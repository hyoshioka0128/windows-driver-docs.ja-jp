---
title: コントロール パネルの ゲーム コント ローラー
description: コントロール パネルの ゲーム コント ローラー
ms.assetid: fb68102a-24d6-4dda-8f27-69366a2129bc
keywords:
- プロパティ シートの WDK DirectInput、コントロール パネルの構造体
- ゲーム コント ローラー WDK DirectInput、コントロール パネルの構造体
- コントロール パネルの WDK DirectInput、アーキテクチャ
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1beb73c41d4b2f2e6cfc116a0b92077a39febb63
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378794"
---
# <a name="game-controller-control-panel"></a>コントロール パネルの ゲーム コント ローラー





DirectInput ゲーム コント ローラーの [コントロール パネル] をサポートする抽象化レイヤー ライブラリから成る、DirectInput のコントロール パネルの基本的なアーキテクチャ、 **IDIGameCntrlPropSheet** COM インターフェイス、および各 COM オブジェクトゲーム コント ローラーのプロパティ シートです。

**注**   「オブジェクト」という単語は、これらのメソッドが C++ などのオブジェクト指向のプログラミング言語を使用して呼び出されていない場合でも、COM インターフェイスのメソッドをサポートするために、CreateInstance により作成されたエンティティをについて説明します。 「シート」という単語には、ページを挿入 ダイアログがについて説明します。 「ページ」という語には、「プロパティ シート」ダイアログ ボックスのコンテンツ、ダイアログ ボックスについて説明します。

 

Microsoft Windows 95/98/Me と Windows NT 4.0 およびそれ以降の間の移植性のため、DirectInput のコントロール パネルは DirectInput で、さらにデバイス ドライバーを直接操作を直接操作します。 これの副産物、としては、DirectInput のコントロール パネルは、アプリケーションがバック グラウンド場合でも、入力デバイスへのアクセスを持ちます。

 

 




