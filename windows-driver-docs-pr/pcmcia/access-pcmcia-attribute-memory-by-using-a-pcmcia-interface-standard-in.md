---
title: PCMCIA_INTERFACE_STANDARD を使用してアクセスのメモリ
description: PCMCIA_INTERFACE_STANDARD インターフェイスを使用してアクセス PCMCIA 属性メモリ
ms.assetid: cd73a8da-1441-4e95-a955-97235ad091ce
keywords:
- PCMCIA_INTERFACE_STANDARD
- 属性のメモリ バス WDK PCMCIA PCMCIA_INTERFACE_STANDARD インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d73cdc5d353ad04f4930ec3b70660ec6f9b4e42
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531434"
---
# <a name="access-pcmcia-attribute-memory-by-using-a-pcmciainterfacestandard-interface"></a>PCMCIA 属性のメモリを PCMCIA を使用してアクセス\_インターフェイス\_標準インターフェイス





このセクションでは、ドライバーが、PCMCIA を使用する方法について説明します\_インターフェイス\_メモリにアクセスする属性の標準的なインターフェイスです。

標準の PCMCIA インターフェイスは、主にメモリ カードのドライバーとファイル システムに提供されます。

ドライバーを使用できる、 [ **PCMCIA\_変更\_メモリ\_ウィンドウ**](https://msdn.microsoft.com/library/windows/hardware/ff537610) PCMCIA でサポートされているルーチンをインターフェイス\_インターフェイス\_標準的なインターフェイスです。 PCMCIA\_変更\_メモリ\_ウィンドウ PCMCIA のメモリ カードのメモリ ウィンドウの属性を設定します。 [メモリ] ウィンドウは、PCMCIA バス ドライバーによってマップされます。 このルーチンは永続的なウィンドウを提供していないのみ既存のウィンドウの現在の設定を変更しことに注意してください。 さらに、設定が永続的なシステム電源の状態では、変化です。

詳細については、次を参照してください。 [PCMCIA\_インターフェイス\_メモリ カードの標準的なインターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff537606)します。

 

 





