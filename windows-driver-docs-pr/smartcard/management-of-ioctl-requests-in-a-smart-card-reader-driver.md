---
title: スマート カード リーダー ドライバーでの IOCTL 要求の管理
description: スマート カード リーダー ドライバーでの IOCTL 要求の管理
ms.assetid: 610476fc-59e7-4981-9afa-20ed7cc697c1
keywords:
- スマート カードのドライバー WDK、IOCTL 要求の管理
- Ioctl WDK のスマート カード
- ベンダーから提供されたドライバー WDK スマート カード、IOCTL 要求の管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d55b7ee31e7b4c8fcc81e179288cb79b565eab18
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356698"
---
# <a name="management-of-ioctl-requests-in-a-smart-card-reader-driver"></a>スマート カード リーダー ドライバーでの IOCTL 要求の管理


## <span id="_ntovr_management_of_ioctl_requests_in_a_smart_card_reader_driver"></span><span id="_NTOVR_MANAGEMENT_OF_IOCTL_REQUESTS_IN_A_SMART_CARD_READER_DRIVER"></span>


IOCTL 要求の管理は、スマート カードのドライバー ライブラリの中央に配置します。 ほとんどの場合、スマート カード リーダーのドライバー渡すだけで済みます IOCTL 要求を[ **SmartcardDeviceControl (WDM)** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))ライブラリ ルーチン。

ただし、スマート カードのドライバー ライブラリによって処理された IOCTL 要求の標準セットは、常に、リーダー デバイスの機能を完全にサポートには不十分な。 そのため、ベンダーは、独自の IOCTL 要求を作成する必要があります。 さらに、一部の標準の IOCTL 要求後ドライバー ライブラリによって処理されている追加の処理を必要があります。 ドライバーではどちらのこれらの理由から、スマート カード リーダーのベンダーから提供されたリーダーのドライバーのアーキテクチャが一連のコールバック ルーチンを実装することができます。 これらのコールバック ルーチンでは、必要なときに、Ioctl のさらなる処理を提供します。

次のセクションでは、リーダーのドライバーが IOCTL 要求を管理する方法、コールバックの日常的なメカニズムのしくみ、およびリーダーのドライバーがそのコールバック ルーチンを初期化するために行う必要がありますを説明します。

具体的には、次のトピックが含まれます。

[スマート カードのドライバー ライブラリとの対話](interaction-with-the-smart-card-driver-library.md)

[スマート カード ドライバー ライブラリ コールバック ルーチン](smart-card-driver-library-callback-routines.md)

[スマート カードのコールバック パラメーター](smart-card-callback-parameters.md)

 

 





