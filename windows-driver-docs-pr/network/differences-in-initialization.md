---
title: 初期化の相違点
description: 初期化の相違点
ms.assetid: 1b19e30d-3c10-4b97-9bb4-3233f7f2a195
keywords:
- 接続指向プロトコルの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4e52663f3f90e3f7c6da25ae1a1d99f0d72f413
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529891"
---
# <a name="differences-in-initialization"></a>初期化の相違点





コール マネージャーは、NDIS プロトコルです。そのため、初期化シーケンス接続指向プロトコルしますが、1 つ追加の手順に従います。 その[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)ハンドラー、接続指向プロトコルでは、初期化の手順を完了した直後にコール マネージャー登録する必要があります、アドレス ファミリを呼び出すことによって[**NdisCmRegisterAddressFamilyEx**](https://msdn.microsoft.com/library/windows/hardware/ff561685)します。 呼び出し**NdisCmRegisterAddressFamilyEx**、コール マネージャーが登録マネージャーの関数を呼び出し、コール マネージャーとして、プロトコルを識別します。 コール マネージャーは、バインド自体に各 NIC のアドレス ファミリを登録する必要があります。

MCM ドライバーは、ミニポート ドライバー。次の手順を追加すると接続指向のミニポート ドライバーの初期化シーケンスを次にそのため、: MCM ドライバーが呼び出すことによって、アドレス ファミリを登録する必要があります[ **NdisMCmRegisterAddressFamilyEx**](https://msdn.microsoft.com/library/windows/hardware/ff563554)でその[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)ミニポート ドライバーの初期化シーケンスを完了した直後に、関数。 呼び出し**NdisMCmRegisterAddressFamilyEx**MCM にドライバーが登録マネージャーの関数を呼び出し、通常の接続指向のミニポート ドライバーと MCM のドライバーを区別します。 ただし、MCM ドライバーの初期化中に呼び出すことによって、ミニポート ドライバー ハンドラーを 1 回だけを登録する[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)、呼び出す必要があります**NdisMCmRegisterAddressFamilyEx**それによって制御される各 NIC に 1 回です。

 

 





