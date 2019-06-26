---
title: 初期化の違い
description: 初期化の違い
ms.assetid: 1b19e30d-3c10-4b97-9bb4-3233f7f2a195
keywords:
- 接続指向プロトコルの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae23a663156a747a6878d1c80568f9afcbf6d9af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381372"
---
# <a name="differences-in-initialization"></a>初期化の違い





コール マネージャーは、NDIS プロトコルです。そのため、初期化シーケンス接続指向プロトコルしますが、1 つ追加の手順に従います。 その[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)ハンドラー、接続指向プロトコルでは、初期化の手順を完了した直後にコール マネージャー登録する必要があります、アドレス ファミリを呼び出すことによって[**NdisCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmregisteraddressfamilyex)します。 呼び出し**NdisCmRegisterAddressFamilyEx**、コール マネージャーが登録マネージャーの関数を呼び出し、コール マネージャーとして、プロトコルを識別します。 コール マネージャーは、バインド自体に各 NIC のアドレス ファミリを登録する必要があります。

MCM ドライバーは、ミニポート ドライバー。次の手順を追加すると接続指向のミニポート ドライバーの初期化シーケンスを次にそのため、: MCM ドライバーが呼び出すことによって、アドレス ファミリを登録する必要があります[ **NdisMCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcmregisteraddressfamilyex)でその[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)ミニポート ドライバーの初期化シーケンスを完了した直後に、関数。 呼び出し**NdisMCmRegisterAddressFamilyEx**MCM にドライバーが登録マネージャーの関数を呼び出し、通常の接続指向のミニポート ドライバーと MCM のドライバーを区別します。 ただし、MCM ドライバーの初期化中に呼び出すことによって、ミニポート ドライバー ハンドラーを 1 回だけを登録する[ **NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)、呼び出す必要があります**NdisMCmRegisterAddressFamilyEx**それによって制御される各 NIC に 1 回です。

 

 





