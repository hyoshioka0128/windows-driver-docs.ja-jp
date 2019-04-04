---
title: DLL の停止操作
description: DLL の停止操作
ms.assetid: b49e9215-3781-4e19-8287-f484553ccb2e
keywords:
- IHV 拡張 DLL WDK ネイティブ 802.11、停止操作
- IHV 拡張 DLL のアンロード
- IHV 拡張機能の DLL を停止しています
- ネイティブの 802.11 IHV 拡張 DLL の WDK、操作を停止します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c393f00942b2c4f33c755b74cb040c3cb453600a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551902"
---
# <a name="dll-stop-operations"></a>DLL の停止操作




 

オペレーティング システムが停止し、IHV 拡張 DLL をアンロードするたびにします。

-   DLL によって管理されている最後のワイヤレス LAN (WLAN) アダプターが削除または無効になっています。

-   ホスト コンピューターはリセットまたはシャット ダウンします。

オペレーティング システムでは、このシーケンスを停止すると、IHV 拡張 DLL のアンロードに従います。

1.  オペレーティング システムの最初の呼び出し、 [ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452) IHV 拡張機能の DLL によって管理されるすべての WLAN アダプターの IHV ハンドラー関数。 この操作の詳細については、[802.11 WLAN アダプター削除](802-11-wlan-adapter-removal.md)を参照してください。

    呼び出し後*Dot11ExtIhvDeinitAdapter*、IHV 拡張機能の DLL などのアダプター固有の操作に関連するすべての IHV 拡張関数を呼び出してはならない[ **Dot11ExtNicSpecificExtension**](https://msdn.microsoft.com/library/windows/hardware/ff547526).

2.  オペレーティング システムを呼び出して、 [ *Dot11ExtIhvDeinitService* ](https://msdn.microsoft.com/library/windows/hardware/ff547457) IHV ハンドラー関数。 この関数し、呼び出され、IHV 拡張機能の DLL する必要があります割り当てられているすべてのリソースを解放自体をアンロードするために準備します。

    呼び出し後*Dot11ExtIhvDeinitService*、IHV 拡張機能の DLL は任意の拡張機能の IHV 関数を呼び出す必要がありますされません。

3.  最後に、オペレーティング システムの呼び出し、 *DllMain*を IHV 拡張 DLL 内の関数、 *fdwReason* DLL にパラメーターが設定\_プロセス\_デタッチします。 詳細については*DllMain*と Dll は、Microsoft Windows SDK のドキュメント内のトピック「ダイナミック リンク ライブラリについて」を参照してください。

IHV 拡張機能の詳細については、[802.11 IHV 拡張関数をネイティブ](https://msdn.microsoft.com/library/windows/hardware/ff560609)を参照してください。

 

 





