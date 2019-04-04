---
title: 802.11 WLAN アダプターの取り外し
description: 802.11 WLAN アダプターの取り外し
ms.assetid: 2181d284-7987-48db-b7a4-d1296d8313ed
keywords:
- WDK 802.11 の WLAN のアダプターを削除します。
- WLAN アダプター、WDK を削除します。
- WLAN のアダプターを削除します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abfa024708dfd0713da3120bc44f88f258cb142d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580708"
---
# <a name="80211-wlan-adapter-removal"></a>802.11 WLAN アダプターの取り外し




 

ワイヤレス LAN (WLAN) アダプターが削除または無効になっている、オペレーティング システムの呼び出し[ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452)アダプターの削除の IHV 拡張機能の DLL に通知します。 オペレーティング システムも呼び出して、 *Dot11ExtIhvDeinitAdapter* IHV 拡張機能の DLL によって管理されるオペレーティング システムは、DLL をアンロードする前にすべてのアダプターの関数。

ときに[ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452)が呼び出されると、IHV 拡張機能の DLL は次のガイドラインを従う必要があります。

-   IHV 拡張機能の DLL には、WLAN アダプターに割り当てられたリソースを解放する必要があります。 呼び出しを通じて具体的には、すべてのメモリが割り当てられている[ **Dot11ExtAllocateBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff547419)呼び出しを通じて解放する必要があります[ **Dot11ExtFreeBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff547422).

-   ハンドルは、使用、オペレーティング システムによって、WLAN を参照するアダプターが無効になってとき[ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452)が呼び出されます。 オペレーティング システムでは、そのハンドルを渡しますを介して IHV 拡張 DLL を*hDot11SvcHandle*パラメーターと[ *Dot11ExtIhvInitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547469)が呼び出されます。

    呼び出し内で、 *Dot11ExtIhvDeinitAdapter*関数呼び出しから返された後、DLL する必要がありますいない値を使用して、ハンドル、IHV 拡張関数を呼び出すことを宣言する場合、 *hDot11SvcHandle*パラメーターなど[ **Dot11ExtSendPacket**](https://msdn.microsoft.com/library/windows/hardware/ff547563)します。

-   IHV 拡張機能の DLL を呼び出すことによって開始された保留中の関連付け前操作がある場合、 [ *Dot11ExtIhvPerformPreAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547499) IHV ハンドラー関数では、オペレーティング システムにおいて、操作を呼び出して取り消し対象として、 [ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452)関数。 呼び出し内で、DLL は内部的には、関連付け前の操作を取り消す必要がありますを呼び出してはならない[ **Dot11ExtPreAssociateCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff547538)関連付け前に操作を完了します。

    前の関連付け操作の詳細については、[関連付け前操作](pre-association-operations.md)を参照してください。

-   IHV 拡張機能の DLL を呼び出すことによって開始された保留中の後の関連付け操作がある場合、 [ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492) IHV ハンドラー関数をオペレーティング システムを取り消します。呼び出して、操作、 [ *Dot11ExtIhvStopPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547521)関数を呼び出す前に[ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452).

    詳細については、後の関連付け操作は、[後関連付け操作](post-association-operations.md)を参照してください。

-   オペレーティング システムの呼び出し、 [ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452) IHV 拡張機能の DLL によって管理されるオペレーティング システムは、DLL をアンロードする前にすべてのアダプターの関数。 このような状況でオペレーティング システムの呼び出し、 [ *Dot11ExtIhvDeinitService* ](https://msdn.microsoft.com/library/windows/hardware/ff547457) IHV ハンドラー関数を呼び出すことによって、最後の WLAN のアダプターが停止した後に*Dot11ExtIhvDeinitAdapter*します。

    この操作の詳細については、[DLL 停止操作](dll-stop-operations.md)を参照してください。

 

 





