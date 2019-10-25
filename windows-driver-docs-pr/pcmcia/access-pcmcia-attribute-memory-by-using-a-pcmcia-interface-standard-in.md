---
title: PCMCIA_INTERFACE_STANDARD を使用したメモリへのアクセス
description: PCMCIA_INTERFACE_STANDARD インターフェイスを使用して PCMCIA 属性のメモリにアクセスする
ms.assetid: cd73a8da-1441-4e95-a955-97235ad091ce
keywords:
- PCMCIA_INTERFACE_STANDARD
- 属性メモリ WDK PCMCIA バス、PCMCIA_INTERFACE_STANDARD インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36cfcee371cbd3af25e215ba4f112a6c904b28ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837735"
---
# <a name="access-pcmcia-attribute-memory-by-using-a-pcmcia_interface_standard-interface"></a>PCMCIA\_インターフェイス\_標準インターフェイスを使用して PCMCIA 属性のメモリにアクセスする





このセクションでは、ドライバーが PCMCIA\_インターフェイス\_標準インターフェイスを使用して属性メモリにアクセスする方法について説明します。

PCMCIA インターフェイス標準は、主にメモリカードドライバーとファイルシステム用に提供されています。

ドライバーは、pcmcia\_INTERFACE\_STANDARD インターフェイスでサポートされている[**pcmcia\_MODIFY\_MEMORY\_WINDOW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpcm/nc-ntddpcm-pcmcia_modify_memory_window)インターフェイスルーチンを使用できます。 [PCMCIA\_\_メモリの変更]\_ウィンドウは、PCMCIA メモリカードの [メモリ] ウィンドウの属性を設定します。 [メモリ] ウィンドウは、PCMCIA バスドライバーによってマップされます。 このルーチンは、永続的なウィンドウを提供しないことに注意してください。既存のウィンドウの現在の設定のみが変更されます。 また、システムの電源状態が変化しても、設定は永続的ではありません。

詳細については、「 [PCMCIA\_INTERFACE\_Memory カード用の標準インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/pcmcia-interface-standard-interface-for-memory-cards)」を参照してください。

 

 





