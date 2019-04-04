---
title: クライアント オブジェクトの使用
description: クライアント オブジェクトの使用
ms.assetid: 07311a2e-86a7-4985-9dfa-55a876cd7899
keywords:
- デバッガー エンジン、COM インターフェイス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2006e9f2686fcd7cb93f656242e486f990c22211
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549778"
---
# <a name="using-client-objects"></a>クライアント オブジェクトの使用


デバッガー エンジンと対話するクライアント オブジェクトの役割の概要については、[クライアント オブジェクト](client-objects.md)を参照してください。

一般に、クライアントのメソッドは、クライアントが作成されたスレッドからのみ呼び出すことがあります。 通常、間違ったスレッドから呼び出されるメソッドはすぐに失敗します。 このルールの主な例外は、メソッド[ **CreateClient**](https://msdn.microsoft.com/library/windows/hardware/ff539320); このメソッドは、任意のスレッドから呼び出すことができ、呼び出し元のスレッドで使用できる新しいクライアントを返します。 参照セクションでは、その他の例外が記載されています。

クライアント オブジェクトを記述する文字列が、メソッドによって返される[ **GetIdentity** ](https://msdn.microsoft.com/library/windows/hardware/ff546831)またはエンジンの出力を書き込むストリームを使用して[ **OutputIdentity**](https://msdn.microsoft.com/library/windows/hardware/ff553219).

### <a name="span-idcominterfacesspanspan-idcominterfacesspancom-interfaces"></a><span id="com_interfaces"></span><span id="COM_INTERFACES"></span>COM インターフェイス

デバッガー エンジン API には、いくつかの COM インターフェイスなどが含まれています。実装する、 **IUnknown**インターフェイス。

セクションで説明されているインターフェイス[デバッグ エンジンのインターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff539131)(が必ずしも最新のバージョンで)、クライアントによって実装されます。 COM メソッドを使用することがあります**iunknown::queryinterface**他のいずれかからこれらの各インターフェイスを取得します。

クライアントの実装、 **IUnknown** COM インターフェイスし、参照カウントを維持するために使用するインターフェイスの選択。 ただし、クライアントは、登録済みの COM オブジェクトではありません。 メソッド**iunknown::addref** 、オブジェクトとメソッドの参照カウントをインクリメントするために使用 **:release**参照カウントをデクリメントするために使用します。 ときに**iunknown::queryinterface**を呼び出すと、参照カウントをインクリメントすると、クライアントのインターフェイス ポインターが不要になったとき、 **:release**の参照をデクリメントを呼び出す必要がありますカウントです。

参照カウントを使用して、クライアント オブジェクトが作成されたときに、1 つに初期化されます[ **DebugCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff540469)または[ **DebugConnect**](https://msdn.microsoft.com/library/windows/hardware/ff540465)します。

インクリメントとデクリメントの参照カウントのする場合の詳細については、プラットフォーム SDK を参照してください。

**Iunknown::queryinterface**、 **DebugCreate**、および**DebugConnect**それぞれの引数の 1 つとして、インターフェイス ID を受け取ります。 このインターフェイスを使用して ID を取得することができます、  **\_ \_uuidof**演算子。 次に、例を示します。

```cpp
IDebugClient * debugClient;
HRESULT Hr = DebugCreate( __uuidof(IDebugClient), (void **)&debugClient );
```

**重要な**  、IDebug\*ようなインターフェイス[ **IDebugEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff550550)インターフェイス、like、COM は適切な COM Api ではありません。 これらのインターフェイスをマネージ コードから呼び出すことは、サポートされていないシナリオです。 ガベージ コレクション スレッドの所有権などの問題は、インターフェイスがマネージ コードで呼び出されたときに、システムが不安定につながります。

 

 

 





