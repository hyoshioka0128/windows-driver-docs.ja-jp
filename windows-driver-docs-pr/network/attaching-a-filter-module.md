---
title: フィルター モジュールのアタッチ
description: フィルター モジュールのアタッチ
ms.assetid: 4441383e-cc22-4fe1-9c46-28d405736daa
keywords:
- フィルターモジュール WDK ネットワーク、アタッチ
- フィルターモジュールのアタッチ
- フィルタードライバーの WDK ネットワーク, フィルターモジュールのアタッチ
- NDIS フィルタードライバー WDK、アタッチ (フィルターモジュールを)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f85bf31442549b5211cd1d270bf265743b22542
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835283"
---
# <a name="attaching-a-filter-module"></a>フィルター モジュールのアタッチ





フィルターモジュールをドライバースタックに挿入するプロセスを開始するために、NDIS はフィルタードライバーの[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数を呼び出します。 *Filterattach*関数での実行の開始時に、フィルターモジュールは*アタッチ*状態に入ります。 フィルターモジュールをドライバースタックにアタッチする方法の詳細については、「[ドライバースタックを開始](starting-a-driver-stack.md)する」を参照してください。

フィルタードライバーは、このハンドルを使用します。このハンドルは、このフィルターモジュールを参照するすべての将来の**NdisXxx**関数呼び出しで[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)の*NdisFilterHandle*パラメーターに渡されます。 このような関数には、状態の表示、送信要求、受信通知、OID 要求などがあります。

フィルターモジュールが*アタッチ*状態のとき、ドライバーは次のようになります。

-   フィルターモジュールのコンテキスト領域を作成し、バッファープールとその他のフィルターモジュール固有のリソースを割り当てます。 バッファープールの詳細については、「[フィルタードライバーのバッファー管理](filter-driver-buffer-management.md)」を参照してください。

-   NDIS が[*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)に渡された*NdisFilterHandle*値を使用して、 [**NdisFSetAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsetattributes)関数を呼び出します。 **NdisFSetAttributes**の*filtermodulecontext*パラメーターは、このフィルターモジュールのフィルタードライバーのコンテキスト領域を指定します。 NDIS は、このコンテキスト領域をフィルタードライバーの*Filterxxx*関数に渡します。

-   必要に応じて、レジストリからこのフィルターモジュールの構成パラメーターを読み取ります。 詳細については、「[フィルタードライバーの構成情報へのアクセス](accessing-configuration-information-for-a-filter-driver.md)」を参照してください。

-   上記の操作が正常に完了した場合、フィルターモジュールは*一時停止*状態になります。

-   上記の操作が失敗した場合、フィルタードライバーは、 [*Filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数で割り当てられたリソースを解放し、フィルターモジュールを*デタッチ*された状態に戻す必要があります。

-   NDIS\_STATUS\_SUCCESS または適切なエラーコードを返します。 ドライバーがエラーコードを返した場合、NDIS はドライバースタックを終了します。

レジストリにフラグを含めること  できます。これは、フィルターモジュールが省略可能で**あることを**指定します。 オプションのフィルターモジュールがアタッチされていない場合、NDIS はドライバースタックの残りの部分を終了しません。

 

フィルタードライバーは、送信要求を行ったり、受信データを指定したり、OID 要求を行ったり、状態を*添付*状態から確認したりすることはできません。 送信および受信操作は、*実行中*と*一時停止*中の状態でサポートされています。 OID 要求と状態のインジケーターは、*一時停止*、*再起動*、*実行中*、および*一時停止*状態でサポートされています。

NDIS は、 [*Filterdetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)関数を呼び出して、Ndis が[*filterdetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)にアタッチしたフィルターモジュールをデタッチします。 詳細については、「[フィルターモジュールのデタッチ](detaching-a-filter-module.md)」を参照してください。

 

 





