---
title: 画像処理フィルターの概要
description: 画像処理フィルターの概要
ms.assetid: 59fc1bc1-c783-43df-9778-ea4306f6dd50
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22cc0c7372512dbf7339029b162a070a6e4a486f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581860"
---
# <a name="introduction-to-image-processing-filters"></a>画像処理フィルターの概要





イメージのフィルター処理は、WIA 拡張です。 イメージ処理のフィルターには、2 つの主な目的があります。

-   イメージの処理コード、ドライバーから分離することができるようにします。 たとえば、明るさとコントラストのイメージを変更して、デスキューと回転を実行する、イメージ処理フィルターを使用できます。 イメージ処理のフィルターがユーザー モード ドライバー DLL から独立した独自の DLL です。 イメージ処理フィルターにはフィルター処理を実行するドライバーから画像データをフィルター処理されていないを受信します。

-   正確なライブ プレビューを有効にします。 正確なライブ プレビューを提供する Windows Vista WIA プレビュー コンポーネント (Microsoft Windows SDK のドキュメントで説明) の新しいイメージの処理のフィルターが使用されます。 このコンテキストで「ライブ」には、アプリケーションが、このセクションでは、後ほどいくつかのプロパティ設定を変更したら、スキャナーからのイメージを再取得する必要はありませんを意味します。 プレビューは、完全に独立したイメージには単なるランダムなフィルターではなく、実際のプレビュー イメージの仕入先コンポーネントでは実際に実行されて、フィルター処理から正確です。

正確なプレビューを提供するためにフィルターを実装する必要があります[**明るさ**](https://msdn.microsoft.com/library/windows/hardware/ff552567)と[**コントラスト**](https://msdn.microsoft.com/library/windows/hardware/ff552573)には、少なくともプロパティ。 これは、明るさとコントラストのコントロールをユーザーに提供する共通の UI は正確なプレビューを表示できるようにします。

イメージがスキャンされたときに、イメージ処理フィルターが常に実行されます。 したがって、アプリケーション、画像を最初に適用されるフィルターの処理をしなくても、スキャナーからのイメージを取得する方法はありません。 アプリケーションは、フィルターを意識する必要はありません。

Microsoft では、WIA プレビュー コンポーネント スキャナーから取得した、元のフィルター処理されていないプレビュー イメージのキャッシュを提供します。 プレビューのコンポーネントでは、スキャナーからのイメージを再度取得することがなく、イメージにフィルターを複数回を適用できます。 WIA プレビュー コンポーネントは通常、使用プレビュー イメージの場合、アプリケーションで、ユーザーは、明るさ、コントラストなどの設定を変更します。 ユーザーが、設定を変更中に、アプリケーション継続的にイメージを表示できます、結果として得られるプレビュー ウィンドウにイメージを再スキャンする必要はありません。

イメージ処理のフィルターは、インプロセス COM コンポーネントとして実行されている、WIA 拡張です。 セグメント化フィルターとは異なり、通常作成されていないイメージ処理フィルター自体のインスタンスを呼び出して**IWiaItem2::GetExtension** (Windows SDK のドキュメントで説明)。 代わりに、アプリケーションが実際のイメージを使用してフィルター処理をさらに読み込む WIA プレビュー コンポーネントのインスタンスを作成、 **IWiaItem2::GetExtension**メソッド。 アプリケーションを呼び出すと、イメージ処理のフィルターは自動的に呼び出されますも**IWiaTransfer::Download**します。

イメージ処理フィルターがドライバーに関連付けられているし、通常は、ドライバーと共に配布します。 WIA プレビュー コンポーネントは、のみで使用可能なオペレーティング システムが付属しています。

次の図は、WIA コンポーネントによって、アプリケーションのプロセスに読み込まれるフィルター処理、イメージを示します。 1 つ以上のインスタンスに読み込まれるアプリケーションのプロセスと同時に、フィルターの書き込みは、これについて注意が必要である必要がありますので、イメージ処理のフィルターの可能性があるに注意してください。 たとえば、グローバル (静的) の変数を使用する場合に備えてフィルター ライターに適切な同期する必要がありますを確認します。

![wia コンポーネントによって、アプリケーションのプロセスに読み込まれるイメージ処理フィルターを示す図](images/wia-components-app-process.png)

 

 



