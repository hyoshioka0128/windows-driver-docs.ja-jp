---
title: DLL 停止操作
description: DLL 停止操作
ms.assetid: b49e9215-3781-4e19-8287-f484553ccb2e
keywords:
- IHV 拡張 DLL WDK ネイティブ 802.11、停止操作
- IHV 拡張 DLL のアンロード
- IHV 拡張機能の DLL を停止しています
- ネイティブの 802.11 IHV 拡張 DLL の WDK、操作を停止します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8943a76f41f542724050de91b7c4268cd177f3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386556"
---
# <a name="dll-stop-operations"></a>DLL 停止操作




 

オペレーティング システムが停止し、IHV 拡張 DLL をアンロードするたびにします。

-   DLL によって管理されている最後のワイヤレス LAN (WLAN) アダプターが削除または無効になっています。

-   ホスト コンピューターはリセットまたはシャット ダウンします。

オペレーティング システムでは、このシーケンスを停止すると、IHV 拡張 DLL のアンロードに従います。

1.  オペレーティング システムの最初の呼び出し、 [ *Dot11ExtIhvDeinitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter) IHV 拡張機能の DLL によって管理されるすべての WLAN アダプターの IHV ハンドラー関数。 この操作の詳細については、次を参照してください。 [802.11 WLAN アダプター削除](802-11-wlan-adapter-removal.md)します。

    呼び出し後*Dot11ExtIhvDeinitAdapter*、IHV 拡張機能の DLL などのアダプター固有の操作に関連するすべての IHV 拡張関数を呼び出してはならない[ **Dot11ExtNicSpecificExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension).

2.  オペレーティング システムを呼び出して、 [ *Dot11ExtIhvDeinitService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_service) IHV ハンドラー関数。 この関数し、呼び出され、IHV 拡張機能の DLL する必要があります割り当てられているすべてのリソースを解放自体をアンロードするために準備します。

    呼び出し後*Dot11ExtIhvDeinitService*、IHV 拡張機能の DLL は任意の拡張機能の IHV 関数を呼び出す必要がありますされません。

3.  最後に、オペレーティング システムの呼び出し、 *DllMain*を IHV 拡張 DLL 内の関数、 *fdwReason* DLL にパラメーターが設定\_プロセス\_デタッチします。 詳細については*DllMain*と Dll は、Microsoft Windows SDK のドキュメント内のトピック「ダイナミック リンク ライブラリについて」を参照してください。

IHV 拡張機能の詳細については、次を参照してください。 [802.11 IHV 拡張関数をネイティブ](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)します。

 

 





