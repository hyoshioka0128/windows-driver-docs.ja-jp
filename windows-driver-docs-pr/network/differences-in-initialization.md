---
title: 初期化の相違点
description: 初期化の相違点
ms.assetid: 1b19e30d-3c10-4b97-9bb4-3233f7f2a195
keywords:
- 接続指向プロトコルの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc4aa36a3bd1eedafa415fee6b20b27a47395b60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838139"
---
# <a name="differences-in-initialization"></a>初期化の相違点





呼び出しマネージャーは、NDIS プロトコルです。そのため、接続指向プロトコルの初期化シーケンスに従いますが、1つ追加の手順があります。 [*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)ハンドラーでは、接続指向プロトコルの初期化手順を完了した直後に、呼び出しマネージャーが[**NdisCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregisteraddressfamilyex)を呼び出してアドレスファミリを登録する必要があります。 呼び出しマネージャーが呼び出しマネージャーの関数を登録する**NdisCmRegisterAddressFamilyEx**を呼び出すと、プロトコルが呼び出しマネージャーとして識別されます。 呼び出しマネージャーは、それ自体をバインドする各 NIC のアドレスファミリを登録する必要があります。

MCM ドライバーはミニポートドライバーです。したがって、次の手順を追加することで、接続指向ミニポートドライバーの初期化シーケンスに従います。 MCM ドライバーは、 [**NdisMCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmregisteraddressfamilyex)を[*呼び出して、アドレスファミリを登録する必要があります。MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数。ミニポートドライバーの初期化シーケンスの完了直後です。 MCM ドライバーが呼び出しマネージャー関数を登録する**NdisMCmRegisterAddressFamilyEx**を呼び出すと、mcm ドライバーが通常の接続指向のミニポートドライバーと区別されます。 MCM ドライバーは、 [**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)を呼び出して初期化中にミニポートドライバーハンドラーを1回だけ登録しますが、制御する NIC ごとに**NdisMCmRegisterAddressFamilyEx**を1回呼び出す必要があります。

 

 





