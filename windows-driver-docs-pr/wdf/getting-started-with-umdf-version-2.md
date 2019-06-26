---
title: UMDF の概要
description: このセクションでは、ユーザー モード ドライバー フレームワーク (UMDF) を説明し、UMDF バージョン 1 と 2 の違いの詳細。
ms.assetid: 2C4DAFA4-783C-4739-8D27-A417AC63B447
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1d4e7ad9728f83c6758f09b8107de3c57e49682
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384439"
---
# <a name="getting-started-with-umdf"></a>UMDF の概要


このセクションでは、ユーザー モード ドライバー フレームワーク (UMDF) を説明し、UMDF バージョン 1 と 2 の違いの詳細。 アーキテクチャの大まかな UMDF に関する情報も提供します。 このセクションを使用して、UMDF ドライバーが、ニーズに最適かどうかを決定し、使用する UMDF バージョンを判断します。

Windows Driver Frameworks (WDF) には、UMDF、ユーザー モード ドライバーを作成するためのフレームワークが含まれています。 カーネル モード ドライバー フレームワーク (KMDF) のような UMDF は、特定の機能とイベント処理のためのオプトインに、暗黙その他のプラグ アンド プレイ (PnP) や、電源管理機能の多くを処理し、ドライバーを許可することの WDM から抽象化レイヤーを提供します。

Windows 8.1 以降の場合は、2 つのメジャー バージョン UMDF、バージョン 1 と 2 があります。 UMDF version 1.11 (11 種類 1 つのドット) は UMDF version 1 の最新バージョンは、UMDF 2 の登場する前に最終バージョンです。 テーブルの完全なバージョン情報とオペレーティング システムの関連性を示す場合を参照してください。 [UMDF バージョン履歴](umdf-version-history.md)します。

UMDF のバージョン 1 では、COM プログラミング モデルを使用して、C++ コードを記述する必要がありますを使用してドライバーを記述します。 UMDF バージョン 1 は KMDF と同じ概念ドライバーのプログラミング モデルに基づいて、UMDF 1 は、さまざまなコンポーネント、デバイス ドライバー インターフェイス (Ddi) データ構造とモデルを実装します。

これに対し、UMDF バージョン 2 以降、多くの KMDF ドライバーを使用できるメソッドを呼び出し、C プログラミング言語で UMDF ドライバーを記述することができます。 すべてのバージョン 2 の UMDF および KMDF の間で共有されるインターフェイスは、同じ名前、パラメーター、および構造体の定義があります。 ドライバーは、共有機能のみを使用または 1 つのフレームワークでのみサポートされている呼び出しの周りの条件付きのマクロを使用して、UMDF または KMDF のいずれかでコンパイルすることが 1 つのドライバーを記述できます。 詳細については、次を参照してください。 [KMDF ドライバーから UMDF ドライバーを生成する方法](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)します。

2 の UMDF および KMDF の間で共通する重要なが、まだ少量のどちらか 1 つのフレームワークでのみ使用できる機能 詳しくは、次を参照してください。 [KMDF に UMDF 2 機能を比較する](comparing-umdf-2-0-functionality-to-kmdf.md)します。 すべての 2 の UMDF および KMDF のコールバックとメソッドの一覧については、適用されるどの framework(s) を参照してくださいと[WDF のコールバックの概要とメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_wdf/)します。 いくつかの場合、構造体のメンバーまたはメソッドのパラメーターがどちらか 1 つのフレームワークにのみ適用されます。 ドキュメントでは、対応するリファレンス ページにこれらの違いについて説明します。

1 つ、または一方を選択する必要があります。両方の UMDF バージョン 1 と 2 からメソッドを呼び出して UMDF ドライバーを記述することはできません。

UMDF ドライバーのバージョン 2 では、Windows 8.1 でのみ、またはそれ以降を実行します。 Windows 8.1 より前のオペレーティング システムで実行されている UMDF ドライバーを作成する必要がある場合は、1.x UMDF ドライバーを作成する必要があります。 1\.11 バージョンを使用すると、Windows Vista 以降を実行しているドライバーをビルドします。 バージョン 1 の詳細については、次を参照してください。 [UMDF 1.x 設計ガイド](user-mode-driver-framework-design-guide.md)します。 このセクションでは、UMDF バージョン 2 について説明します。



 

 
