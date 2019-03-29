---
title: WIA ドライバーの名前空間
description: WIA ドライバーの名前空間
ms.assetid: 67260a25-6233-4738-a08f-26223cc8e563
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9411744e22d6073a7f6d9a7ae18017144845b10e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571207"
---
# <a name="namespaces-for-wia-drivers"></a>WIA ドライバーの名前空間





すべてのサービスは、セッション 0 で実行します。 ただし、アプリケーションの場合は、別のセッションで実行している可能性があります。 各セッションには、独自*名前空間*します。 そのため、1 つのセッションで作成した名前付きオブジェクトは一般に表示されないコンポーネントに別のセッション。

この問題の解決策では、両方のコンポーネントが同じ名前空間を使用することを確認します。 これを行う最も簡単な方法が使用するには、*グローバル名前空間*します。 たとえば、WIA 以外のデバイスにアクセスする場合にバンドルされたコンポーネントは、使用してという名前のミュー テックス オブジェクト**MyDeviceLock** WIA ドライバーを使用したアクセスを同期します。 グローバル名前空間でミュー テックスの名前を格納するために呼び出す必要があります**Global\\MyDeviceLock**します。 名前付きミュー テックス**Global\\MyDeviceLock**は、ドライバーとセッションに関係なく実行されている、名前がグローバル名前空間に属していることを指定して両方いないため、アプリケーションの両方に表示されます。

詳細については、Microsoft Windows SDK ドキュメントでは、「カーネル オブジェクトの名前空間」を参照してください。

 

 




