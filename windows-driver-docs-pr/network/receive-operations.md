---
title: 受信操作
description: 受信操作
ms.assetid: 9ec2ba38-36dd-42d2-b0a8-0abe4d1bb847
keywords:
- 受信操作 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 368bf4c50ba01f01a503d9b0f5c24876cb4e2247
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529307"
---
# <a name="receive-operations"></a>受信操作




 

呼び出すことによって開始された後の関連付け操作を実行するときに[ *Dot11ExtIhvPerformPostAssociate*](https://msdn.microsoft.com/library/windows/hardware/ff547492)、オペレーティング システムの呼び出し、 [ *Dot11ExtIhvReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff547513) HV 拡張機能の DLL にパケットを転送する関数は、ワイヤレス LAN (WLAN) アダプターを介して受信します。 詳細については、後の関連付け操作は、[後関連付け操作](post-association-operations.md)を参照してください。

パケットを受信するには、IHV 拡張機能の DLL を呼び出す必要があります[ **Dot11ExtSetEtherTypeHandling** ](https://msdn.microsoft.com/library/windows/hardware/ff547587)を 1 つまたは複数の IEEE EtherTypes の一覧を登録します。 このリスト内のエントリに一致する、EtherType でパケットが受信されると、オペレーティング システムの呼び出し、 [ *Dot11ExtIhvReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff547513)関数し、関数のを通じてパケット バッファーを渡します*pvInBuffer*パラメーター。

**注**  IHV 拡張 DLL を呼び出す必要があります[ **Dot11ExtSetEtherTypeHandling** ](https://msdn.microsoft.com/library/windows/hardware/ff547587) DLL は、関連付け前の操作を完了する前にします。 この操作の詳細については、[関連付け前操作](pre-association-operations.md)を参照してください。

 

ときに[ *Dot11ExtIhvReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff547513)が呼び出される、 *pvInBuffer*パラメーターが、802.11 パケット全体を含むオペレーティング システムによって割り当てられるバッファーを指すなどのメディアは、コントロール (MAC) のヘッダー、LLC (必要に応じて) カプセル化、およびペイロード データにアクセスします。

IHV 拡張機能の DLL への呼び出し内から受信したパケットへの応答を送信できます[ *Dot11ExtIhvReceivePacket*](https://msdn.microsoft.com/library/windows/hardware/ff547513)します。 DLL では、このような状況で説明されているガイドラインに従う必要があります[送信操作](send-operations.md)します。

 

 





