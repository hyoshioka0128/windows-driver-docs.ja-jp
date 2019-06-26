---
title: クライアント オブジェクトの使用
description: クライアント オブジェクトの使用
ms.assetid: 07311a2e-86a7-4985-9dfa-55a876cd7899
keywords:
- デバッガー エンジン、COM インターフェイス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdcbdbb1730228be46a8bc1595630ae4ab4c4d32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366338"
---
# <a name="using-client-objects"></a>クライアント オブジェクトの使用


デバッガー エンジンと対話するクライアント オブジェクトの役割の概要については、次を参照してください。[クライアント オブジェクト](client-objects.md)します。

一般に、クライアントのメソッドは、クライアントが作成されたスレッドからのみ呼び出すことがあります。 通常、間違ったスレッドから呼び出されるメソッドはすぐに失敗します。 このルールの主な例外は、メソッド[ **CreateClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createclient); このメソッドは、任意のスレッドから呼び出すことができ、呼び出し元のスレッドで使用できる新しいクライアントを返します。 参照セクションでは、その他の例外が記載されています。

クライアント オブジェクトを記述する文字列が、メソッドによって返される[ **GetIdentity** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-getidentity)またはエンジンの出力を書き込むストリームを使用して[ **OutputIdentity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-outputidentity).

### <a name="span-idcominterfacesspanspan-idcominterfacesspancom-interfaces"></a><span id="com_interfaces"></span><span id="COM_INTERFACES"></span>COM インターフェイス

デバッガー エンジン API には、いくつかの COM インターフェイスなどが含まれています。実装する、 **IUnknown**インターフェイス。

セクションで説明されているインターフェイス[デバッグ エンジンのインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/debugger/client-com-interfaces)(が必ずしも最新のバージョンで)、クライアントによって実装されます。 COM メソッドを使用することがあります**iunknown::queryinterface**他のいずれかからこれらの各インターフェイスを取得します。

クライアントの実装、 **IUnknown** COM インターフェイスし、参照カウントを維持するために使用するインターフェイスの選択。 ただし、クライアントは、登録済みの COM オブジェクトではありません。 メソッド**iunknown::addref** 、オブジェクトとメソッドの参照カウントをインクリメントするために使用 **:release**参照カウントをデクリメントするために使用します。 ときに**iunknown::queryinterface**を呼び出すと、参照カウントをインクリメントすると、クライアントのインターフェイス ポインターが不要になったとき、 **:release**の参照をデクリメントを呼び出す必要がありますカウントです。

参照カウントを使用して、クライアント オブジェクトが作成されたときに、1 つに初期化されます[ **DebugCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-debugcreate)または[ **DebugConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-debugconnect)します。

インクリメントとデクリメントの参照カウントのする場合の詳細については、プラットフォーム SDK を参照してください。

**Iunknown::queryinterface**、 **DebugCreate**、および**DebugConnect**それぞれの引数の 1 つとして、インターフェイス ID を受け取ります。 このインターフェイスを使用して ID を取得することができます、  **\_ \_uuidof**演算子。 次に、例を示します。

```cpp
IDebugClient * debugClient;
HRESULT Hr = DebugCreate( __uuidof(IDebugClient), (void **)&debugClient );
```

**重要な**  、IDebug\*ようなインターフェイス[ **IDebugEventCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugeventcallbacks)インターフェイス、like、COM は適切な COM Api ではありません。 これらのインターフェイスをマネージ コードから呼び出すことは、サポートされていないシナリオです。 ガベージ コレクション スレッドの所有権などの問題は、インターフェイスがマネージ コードで呼び出されたときに、システムが不安定につながります。

 

 

 





