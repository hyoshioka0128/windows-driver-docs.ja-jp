---
Description: The WpdServiceSampleDriver Sample
title: WpdServiceSampleDriver サンプル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03ade2ad76c92a80e1450c9aae73a1671e0bf5ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527785"
---
# <a name="the-wpdservicesampledriver-sample"></a>WpdServiceSampleDriver サンプル


デバイス サービスは、関数型のオブジェクトの拡張機能です。 デバイスの機能を論理的にグループ化、だけでなくは、デバイスのサービスは、プログラムによってこれらの機能を検出できるアプリケーションを提供します。

WpdServiceSampleDriver では、デバイスの連絡先サービスでシミュレートされたデバイスをサポートするように、WpdHelloWorldDriver サンプルを拡張する方法を示します。 このデバイスのサービスを使用すると、アプリケーションは、イベント、メソッド、およびデバイスに保存されている連絡先に対する操作のプロパティを検出できます。 また、アプリケーションはこれらのイベントを処理、これらのメソッドを呼び出す、またはこれらのプロパティを取得する連絡先デバイス サービスを使用することができます。 たとえば、アプリケーションでは、連絡先をコンピューターに保存されているデバイス上にある連絡先を同期する、または特定の連絡先の名前プロパティの読み取りメソッドを呼び出す可能性があります。

## <a name="span-idlimitationspanspan-idlimitationspanspan-idlimitationspanlimitation"></a><span id="Limitation"></span><span id="limitation"></span><span id="LIMITATION"></span>制限事項


このドライバーは、概念を説明する最も簡単な方法で記述されました。 そのため、サンプル ドライバーでは、操作を実行する場合がありますか、ドライバーでは運用効率性が低い方法で構造化します。 さらに、このサンプルでは、実際のハードウェアは使用しません。 代わりに、メモリ内データ構造を使用してデバイスをシミュレートします。 したがって、ドライバーは、実稼働のハードウェアの現実的な方法で実装する可能性があります。

 

 




