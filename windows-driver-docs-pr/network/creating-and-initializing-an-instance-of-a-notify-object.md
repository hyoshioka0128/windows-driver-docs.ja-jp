---
title: 通知オブジェクトのインスタンスの作成と初期化
description: 通知オブジェクトのインスタンスの作成と初期化
ms.assetid: 933d24cc-d1a0-4768-9bba-4c78150a84da
keywords:
- オブジェクトの WDK ネットワー キングのインスタンスへの通知します。
- ネットワークは、WDK、オブジェクトのインスタンスに通知します。
- 通知オブジェクトの WDK ネットワー キングのインスタンス
- オブジェクトのインスタンスへの通知の初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98ca7f07175d777f389a48d682698d6b7aeb1a5e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374920"
---
# <a name="creating-and-initializing-an-instance-of-a-notify-object"></a>通知オブジェクトのインスタンスの作成と初期化





ネットワーク構成のサブシステムが通知オブジェクトのインスタンスを作成し、サブシステムは、ネットワーク構成、所有するコンポーネントのカスタム プロパティ ページの表示と変更について通知オブジェクトを通知できます前にオブジェクトを初期化する必要があります、オブジェクト。

サブシステムでは、DLL のクラス ファクトリから通知オブジェクトのインスタンスを作成します。 クラス ファクトリは、通知クラスのコンス トラクターを呼び出します。

クラスのコンス トラクターは、初期値をクラスのデータ メンバーに割り当てる最初必要があります。 コンス トラクターが最初に割り当てる必要があります値を以下に示します。

-   コンス トラクターは、ネットワーク コンポーネントのインスタンスにインターフェイス ポインターを設定する必要があります[ **INetCfgComponent**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547715(v=vs.85))を**NULL**値。

-   コンス トラクターは、ネットワーク構成オブジェクトのインスタンスにインターフェイス ポインターを設定する必要があります[ **INetCfg**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547694(v=vs.85))を**NULL**値。

-   コンス トラクターには、通知オブジェクトは以前、不明なアクションを識別する定数を実行するアクションを指定する変数を設定する必要があります。 この変数の詳細については、次を参照してください。[通知のクラスを定義する](defining-a-notify-class.md)します。

オブジェクトを呼び出して、サブシステム、ネットワーク構成のサブシステムには、通知オブジェクトのインスタンスが作成されたら、 [ **INetCfgComponentControl::Initialize** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547729(v=vs.85))オブジェクトを初期化するメソッドインスタンス。 この呼び出しでは、サブシステムを渡します、 **INetCfgComponent**インターフェイス ポインター。 これは、 **INetCfgComponent**にアクセスして、コンポーネントを制御するオブジェクトで使用できるオブジェクトのコンポーネントのインスタンスに通知オブジェクトを提供します。 サブシステム、この呼び出しで渡すことも、 **INetCfg**通知オブジェクトを使用してネットワークの構成のすべての側面にアクセスするネットワーク構成オブジェクトのインスタンスを持つ通知オブジェクトを提供するインターフェイス ポインター。

**初期化**メソッドが割り当てる必要があります、 **INetCfgComponent**と**INetCfg**インターフェイス ポインターのデータ メンバーに、ネットワーク構成のサブシステムによって提供される、クラスに通知します。 **初期化**し、呼び出す必要があります。

-   **INetCfg::AddRef**ネットワーク構成オブジェクトの参照カウントをインクリメントする方法

-   **INetCfgComponent::AddRef**通知オブジェクトを所有するコンポーネントの参照カウントをインクリメントする方法

まで他の通知オブジェクトのインターフェイス メソッドは呼び出されません**初期化**を返します。

 

 





