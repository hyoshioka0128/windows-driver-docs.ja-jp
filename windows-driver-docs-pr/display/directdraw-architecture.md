---
title: DirectDraw アーキテクチャ
description: DirectDraw アーキテクチャ
ms.assetid: 3bdde4f0-7502-4ca0-80bd-c4d3d93b85fd
keywords:
- GDI WDK DirectDraw
- 描画の WDK DirectDraw、アーキテクチャ
- DirectDraw WDK Windows 2000 の表示、アーキテクチャ
- ユーザー モード DirectDraw WDK Windows 2000 の表示
- カーネル モード DirectDraw WDK Windows 2000 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe32349048421cd29066bac2b299719e3c4a49a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352905"
---
# <a name="directdraw-architecture"></a>DirectDraw アーキテクチャ


## <span id="ddk_directdraw_architecture_gg"></span><span id="DDK_DIRECTDRAW_ARCHITECTURE_GG"></span>


Microsoft DirectDraw には、次のコンポーネントが含まれています。

-   ユーザー モード DirectDraw (*ddraw.dll*) では、システム提供ダイナミック リンク ライブラリ (DLL) ですが読み込まれ、DirectDraw アプリケーションによって呼び出されます。 このコンポーネントでは、ハードウェア エミュレーションを提供し、さまざまな DirectDraw オブジェクトを管理して、表示メモリとディスプレイ ハードウェアの管理サービスを提供します。

-   整数であるカーネル モード DirectDraw 一部分*win32k.sys*、カーネル モードのディスプレイ ドライバーによって読み込まれるシステム提供のグラフィック エンジン。 DirectDraw のこの部分より堅牢なドライバーを実装しやすく、ドライバーのパラメーターの検証を実行します。 これは、ディスプレイ ドライバーは、Microsoft Windows 2000、および以降のオペレーティング システムの信頼されたコンポーネントであるために、重要な設計目標です。 DirectDraw をカーネル モードでは、GDI とプロセス間のすべての状態との同期も処理します。

-   ディスプレイ ドライバーの残りの部分と共にグラフィックス ハードウェア ベンダーによって実装されているディスプレイ ドライバーの DirectDraw 部分。 このコンポーネントは、このドキュメントで、DirectDraw ドライバーと呼ばれます。 ディスプレイ ドライバー ハンドル GDI の他の部分とその他の非 DirectDraw 関連の呼び出しを実行します。

このドキュメントは、一般的に、DirectDraw としてシステムが指定したコンポーネントの両方を参照します。

次の図は、DirectDraw ドライバーのアーキテクチャの図を示します。

![directdraw ドライバーのアーキテクチャを示す図](images/ddfig1.png)

上記の図に示すように、アプリケーションは GDI (ユーザーとカーネル モードの部分) を使ってディスプレイ カードと、ディスプレイ ドライバーにアクセスします。 Direct3D の呼び出しを GDI 呼び出しと、通常、DirectDraw、ディスプレイ ドライバーが常にサポートします。 GDI のデバイスに依存しないビットマップ (DIB) エンジンの部分は、ディスプレイ ドライバーによってサポートされていないときに、機能をエミュレートします。

DirectDraw が呼び出されたときに、DirectDraw ドライバーから直接グラフィックス カードにアクセスします。 DirectDraw では、サポートされているハードウェア関数では、DirectDraw ドライバーやハードウェアのエミュレーション層 (HEL) を呼び出す関数で、ソフトウェアでエミュレートする必要があります。 一方、GDI の呼び出しは、呼び出す必要がありますし、戻る DIB エンジンに、呼び出しがサポートされていない場合、ドライバーに送信されます。

**注**   DirectDraw ドライバーには、操作が失敗した場合、DirectDraw では、操作を DirectDraw HEL にパスしませんでしたが、代わりに、DirectDraw ドライバーのエラー コードをアプリケーションに渡します。

 

初期化時にモードを変更するとき、ディスプレイ ドライバー関数機能 (cap) のビット DirectDraw をします。 これにより、利用可能なドライバ関数やそのアドレスでは、ディスプレイ カードとドライバーの機能に関する情報にアクセスして DirectDraw (、伸縮など透明のブリット表示ピッチ、およびその他の高度な特性)。 DirectDraw がこの情報を持つ、ディスプレイ カードに直接アクセスせず、GDI の呼び出しを行うか、ディスプレイ ドライバーの GDI の特定の部分を使用して、DirectDraw ドライバーを使用できます。

 

 





