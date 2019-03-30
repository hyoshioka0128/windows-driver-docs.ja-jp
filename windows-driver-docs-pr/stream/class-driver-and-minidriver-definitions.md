---
title: クラスのドライバーとミニドライバーの定義
description: クラスのドライバーとミニドライバーの定義
ms.assetid: eb428e8b-0c47-4843-8770-c22088ba5c6c
keywords:
- Stream.sys クラス ドライバー WDK Windows 2000 のカーネルがドライバー/ミニドライバーの関係をクラスします。
- ミニドライバー WDK Windows 2000 のカーネル クラス ドライバー/ミニドライバーのリレーションシップのストリーミング
- ミニドライバー WDK Windows 2000 カーネル ストリーミング、クラス ドライバー/ミニドライバーのリレーションシップ
- クラス ドライバー/ミニドライバー リレーションシップ WDK ストリーミング ミニドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53064efc1c1e1fa27df7b0b96bbc72ed07fbff4c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573277"
---
# <a name="class-driver-and-minidriver-definitions"></a>クラスのドライバーとミニドライバーの定義





Microsoft 提供のクラス ドライバーは、仕入先に書き込まれたミニドライバーとオペレーティング システムの間の単純なインターフェイスを提供する中間ドライバーです。 ミニドライバーは、関数の呼び出しによってほとんどの操作を実行する Microsoft 提供のクラス ドライバーを使用し、のみ、デバイス固有のコントロールを提供します。 ハードウェア固有 DLL です。

WDM、下、ミニドライバーは、クラスのドライバーとその関連付けられたハードウェア アダプターを登録およびクラス ドライバーを登録した各アダプタを表すオブジェクトを作成します。 ミニドライバーは、システムの呼び出しを行うクラス ドライバーのデバイス オブジェクトを使用します。 クラス ドライバーは、WDM ストリーミングによってユーザー モードのクライアントによってアクセスされます。

クラスのドライバーとミニドライバーの間の相互作用は次のとおりです。

-   ミニドライバーは、デバイス オブジェクトは作成されませんが、必要に応じて、クラス ドライバーのデバイス オブジェクトを共有します。 これは、システム リソースを保存します。

-   1 つだけのデバイス オブジェクトは、アダプターごとに作成されます。 複数のサブデバイス (と呼ばれる*ストリーム*) アダプターでサポートされている WDM ストリーミング ピンによって表されます。

 

 



