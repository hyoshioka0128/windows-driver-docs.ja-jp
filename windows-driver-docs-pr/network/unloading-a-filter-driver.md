---
title: フィルター ドライバーのアンロード
description: フィルター ドライバーのアンロード
ms.assetid: e7ef209f-ab61-4644-a641-2fef09023a24
keywords:
- フィルター ドライバー WDK ネットワーク、アンロード
- NDIS フィルター ドライバー WDK、アンロード
- フィルター ドライバーをアンロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5281f141ccdf5711b5df6a95812abb3b2e110480
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382095"
---
# <a name="unloading-a-filter-driver"></a>フィルター ドライバーのアンロード





NDIS フィルター ドライバーに関連付けられているドライバー オブジェクトを指定します、 [*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)というルーチン*FilterDriverUnload*します。 システムを呼び出すことができます、 *FilterDriverUnload*ルーチンとフィルター ドライバーのサービスが削除されているすべてのミニポート アダプター。

[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)ドライバー固有のリソースを解放する必要があります。 フィルター ドライバーを作成したすべてのデバイス オブジェクトを破棄する必要があります。 システムは、後にドライバー アンロード操作を完了できる*FilterDriverUnload*を返します。

アンロード関数の機能は、ドライバー固有です。 一般的な規則として[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)ドライバーの初期化中に実行された操作を元に戻す必要があります。 ドライバーの初期化の詳細については、次を参照してください。[フィルター ドライバーの初期化](initializing-a-filter-driver.md)します。

フィルター ドライバーを呼び出す必要があります、 [ **NdisFDeregisterFilterDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfderegisterfilterdriver)関数[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)します。 **NdisFDeregisterFilterDriver**呼び出し[ *FilterDetach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach)このフィルター ドライバーに関連付けられているすべてのフィルターが現在アタッチされているモジュールをデタッチします。

アンロードのフィルター ドライバーの詳細については、次を参照してください。[ドライバー スタックを停止する](stopping-a-driver-stack.md)します。
