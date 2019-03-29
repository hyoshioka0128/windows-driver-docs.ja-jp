---
title: Windows Vista でのデータ転送のキャンセル
description: Windows Vista でのデータ転送のキャンセル
ms.assetid: 0cdc02bf-23fe-4122-8d5f-f42c3c07da8b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7a456ee86ca7245cb4d2823abbd24c588150588
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577771"
---
# <a name="cancellation-of-data-transfers-in-windows-vista"></a>Windows Vista でのデータ転送のキャンセル


Windows Vista では、新しいインターフェイスで**IWiaTransfer** (これは、「Windows SDK のドキュメント) ストリーム ベースのデータ転送を実行するアプリケーションで使用されます。 新しい転送方法だけでなく、このインターフェイスが含まれています、**キャンセル**など、データ転送をキャンセルするアプリケーションが使用できるメソッド[複数項目転送](multipage-istream-transfers.md)します。 この方法では、非同期的にデータ転送をキャンセルできます。 この手順を使用して、データ転送をキャンセルすることをお勧めします。 ただし、Windows Vista アプリケーションを返すことも S\_転送をキャンセルするには、そのコールバック ルーチンから false を指定します。

したがって、Windows Vista の WIA アプリケーション転送をキャンセルする 2 つの方法があります。

-   戻り値の S\_コールバック ルーチンから false を指定します。

-   呼び出す**IWiaTransfer::Cancel**します。

アプリケーションが、転送をキャンセルする 2 つの異なる方法で、Windows Vista ドライバーが通知されることができます。

-   ドライバーへの呼び出しを受信するその[ **IWiaMiniDrv::drvNotifyPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff544998) WIA を\_イベント\_キャンセル\_IO イベント。 すべてのカーネル モードの読み取りまたは書き込み操作を使用して、重複 I/O のことをお勧めします。 この手順でのみを保証できる*即時*キャンセルします。

-   S\_2 つのコールバック関数から FALSE が返されます。**IWiaMiniDrvTransferCallback::GetNextStream**と[ **IWiaMiniDrvTransferCallback::SendMessage**](https://msdn.microsoft.com/library/windows/hardware/jj151552)します。

アプリケーションを呼び出すと**IWiaTransfer::Cancel**、 **IWiaMiniDrv::drvNotifyPnPEvent** WIA をドライバーにメソッドを呼び出す必要があります\_イベント\_キャンセル\_IO。 さらに、 [ **IWiaMiniDrvTransferCallback::GetNextStream** ](https://msdn.microsoft.com/library/windows/hardware/jj151551)と**IWiaMiniDrvTransferCallback::SendMessage**コールバック関数は常に返す必要があります S\_転送をキャンセルした後は FALSE です。

場合**IWiaTransferCallback::GetNextStream** WIA を返します\_状態\_スキップ\_項目の中に、[複数項目転送](multipage-istream-transfers.md)アプリケーションがスキップしています (は、されません転送する)、現在の項目。 戻り値の S\_FALSE 静止全体の転送を取り消す必要があることを意味します。

**IWiaTransfer**と**IWiaTransferCallback**インターフェイスが、Microsoft Windows SDK ドキュメントに記載されています。

## <a name="related-topics"></a>関連トピック
[**IWiaMiniDrvTransferCallback**](https://msdn.microsoft.com/library/windows/hardware/jj151550)  



