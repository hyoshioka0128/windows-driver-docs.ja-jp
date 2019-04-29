---
title: DirectInput コントロール パネルについて
description: DirectInput コントロール パネルについて
ms.assetid: d6845778-1203-4b5a-8a7b-7d4eecbcc59e
keywords:
- プロパティは、コントロール パネルの WDK の DirectInput をシートします。
- ゲーム コント ローラー WDK DirectInput、コントロール パネルについて
- コントロール パネルの詳細については、コントロール パネル WDK DirectInput、
- Joy.cpl
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 25d058c55351bf8233cdd0d7a0f37cc07c6cff14
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390404"
---
# <a name="about-the-directinput-control-panel"></a>DirectInput コントロール パネルについて





DirectInput では、ゲーム パッド、ジョイスティック、フォース フィードバック デバイスなどのゲーム コント ローラーのサポートを提供します。 Microsoft DirectX 5.0 およびそれ以降のバージョンでは、DirectInput は Joy.cpl と呼ばれる新しいゲーム コント ローラーのコントロール パネルを提供します。 コントロール パネル のこのバージョンは、最初に、機能拡張を許可することで、各コント ローラーに表示されるプロパティ シートは、そのコント ローラーに固有のプロパティ ページ で置き換えることができます。 これは、これらのプロパティ シートに関する情報を含む DLL の作成に使用します。 この DLL は、コントロール パネルの DirectInput に呼び出される COM インターフェイスを公開します。

ゲーム コント ローラーのハードウェア ベンダーは、この拡張機能を使用して、個別のコントロール パネルを作成する代わりに、ゲーム コント ローラーのカスタマイズされたプロパティ シートを提供することが推奨されます。 これにより、構成して、ゲーム コント ローラーをテストする 1 つのコントロール パネルを開くことができます。

 

 




