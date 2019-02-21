---
title: OID_CO_AF_CLOSE
description: このトピックでは、OID_CO_AF_CLOSE オブジェクト識別子 (OID) について説明します。
ms.assetid: 451ab9d5-e118-41c9-8d16-02d75a25a1d4
keywords:
- OID_CO_AF_CLOSE
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84abaf17253ba96ef7f43a410674a371520b0cd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551097"
---
# <a name="oidcoafclose"></a>OID_CO_AF_CLOSE

OID_CO_AF_CLOSE OID は、基になるミニポート ドライバーからの自体をバインド解除する必要がありますをコール マネージャーによって送信されます。 自体をバインド解除、ミニポート ドライバーから、前に、コール マネージャーは、この OID をコール マネージャーで開き、アドレス ファミリを持つ各クライアントに送信します。 応答、クライアントは、以下を実行します。

1. クライアントに multipoint のアクティブな接続がある場合は、呼び出す[NdisClDropParty](https://msdn.microsoft.com/library/windows/hardware/ff561629)として 1 つのパーティのみが、各 multipoint VC のアクティブなままになるまでに必要な回数

2. 呼び出す[NdisClCloseCall](https://msdn.microsoft.com/library/windows/hardware/ff561627)を閉じる必要な回数呼び出しはすべてまだ開いての呼び出しでマネージャー

3. 呼び出す[NdisClDeregisterSap](https://msdn.microsoft.com/library/windows/hardware/ff561628)コール マネージャーで、クライアントが登録されているすべての Sap の登録を解除するために必要なだけ多くの回数

4. 呼び出す[NdisClCloseAddressFamily](https://msdn.microsoft.com/library/windows/hardware/ff561626) OID_CO_AF_CLOSE に含まれている要求で NdisAfHandle によって参照されるアドレス ファミリを閉じる

## <a name="requirements"></a>要件

| | |
| --- | --- |
| バージョン | Windows Vista 以降 |
| Header | Ntddndis.h (include Ndis.h) |

