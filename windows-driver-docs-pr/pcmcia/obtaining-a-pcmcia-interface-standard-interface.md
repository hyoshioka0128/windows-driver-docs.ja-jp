---
title: PCMCIA_INTERFACE_STANDARD インターフェイスを取得します。
description: PCMCIA_INTERFACE_STANDARD インターフェイスを取得します。
ms.assetid: 475bf66a-5b6e-4a06-95f7-b7280dd7276d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1aec3560f8a4ec9f13ffc59f1cbe4989013a981
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551571"
---
# <a name="obtaining-a-pcmciainterfacestandard-interface"></a>取得、PCMCIA\_インターフェイス\_標準インターフェイス





このセクションでは、ドライバーが、PCMCIA を取得する方法について説明します\_インターフェイス\_PCMCIA バス ドライバーから PCMCIA メモリ カードの標準的なインターフェイスです。

ドライバーの取得、PCMCIA\_インターフェイス\_IRP の送信を作成して標準的なインターフェイス\_MJ\_PNP の要求を指定する、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff551687)関数コードを補助します。 ドライバーは、次の操作を実行します。

-   割り当てと 0 塗り、 [PCMCIA\_インターフェイス\_標準インターフェイスのメモリ カードのルーチン](https://msdn.microsoft.com/library/windows/hardware/ff537607)ページ メモリ プール内の構造体。

-   インターフェイスのクエリ要求の IRP を作成し、新しい IRP の次のスタックの場所を取得します。

-   新しいスタックの場所で、次のメンバーを設定します。
    -   **Parameters.QueryInterface.Interface**メンバーがドライバーに割り当てられた PCMCIA を指す\_インターフェイス\_ドライバーによって割り当てられた標準の構造体。
    -   **Parameters.QueryInterface.InterfaceType**メンバーは、GUID 値 GUID によって標準 PCMCIA インターフェイスを指定\_PCMCIA\_インターフェイス\_標準。
-   完了ルーチンを設定し、ドライバー スタック ダウン要求を送信します。

PCMCIA バス ドライバーを PCMCIA 入力要求が成功した場合、\_インターフェイス\_が標準的な構造が指す**Parameters.QueryInterface.Interface**します。

IRQL でドライバーを実行する必要があります&lt;ディスパッチ\_ダウン ドライバー スタックは、この要求を送信するレベル。

 

 





