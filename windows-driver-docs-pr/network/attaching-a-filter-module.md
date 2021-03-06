---
title: フィルター モジュールのアタッチ
description: フィルター モジュールのアタッチ
ms.assetid: 4441383e-cc22-4fe1-9c46-28d405736daa
keywords:
- WDK のモジュールをフィルター処理ネットワーク、アタッチ
- フィルター モジュールのアタッチ
- フィルター ドライバー WDK ネットワークは、フィルター モジュールのアタッチ
- NDIS フィルター ドライバー WDK、フィルター モジュールのアタッチ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11d79679b3c08cc1b425d9c0a09aa3d83f4b0449
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384415"
---
# <a name="attaching-a-filter-module"></a>フィルター モジュールのアタッチ





NDIS フィルター ドライバーの呼び出しのドライバー スタックにフィルター モジュールを挿入するプロセスを開始する[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)関数。 実行の開始時、 *FilterAttach*関数の場合、フィルター モジュールが入力、*アタッチ*状態。 ドライバー スタックへのフィルター モジュールのインポートに関する詳細については、次を参照してください。[開始ドライバー スタック](starting-a-driver-stack.md)します。

フィルター ドライバーで NDIS を渡すと、ハンドルを使用して、 *NdisFilterHandle*パラメーターの[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)将来のすべての**NdisXxx**このフィルター モジュールを参照する関数の呼び出し。 このような関数は、状態インジケーターを含める、要求を送信する、インジケーター、および OID 要求を受信します。

フィルター モジュールが、*アタッチ*状態では、ドライバー。

-   フィルター モジュールのコンテキストの領域を作成し、バッファー プールと他のフィルター モジュールに固有のリソースを割り当てます。 バッファー プールの詳細については、次を参照してください。[フィルター ドライバー バッファー管理](filter-driver-buffer-management.md)します。

-   呼び出し、 [ **NdisFSetAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsetattributes)関数を使用して、 *NdisFilterHandle*に渡される NDIS 値[ *FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach). *FilterModuleContext*パラメーターの**NdisFSetAttributes**このフィルター モジュールのフィルター ドライバーのコンテキストの領域を指定します。 NDIS フィルター ドライバーのこのコンテキストの領域を渡す*FilterXxx*関数。

-   必要に応じて、このフィルター モジュールの構成パラメーターをレジストリから読み取ります。 詳細については、次を参照してください。[フィルター ドライバーの構成の情報にアクセスする](accessing-configuration-information-for-a-filter-driver.md)します。

-   かどうか上述の操作を正常に完了して、フィルター モジュールが、 *Paused*状態。

-   フィルター ドライバーに割り当て、リソースを解放する必要があります、上述の操作に失敗した場合、 [ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)関数し、フィルター モジュールを返す、 *Detached*状態。

-   NDIS 返します\_状態\_成功または適切なエラー コード。 ドライバーは、エラー コードを返します、NDIS ドライバー スタックを終了します。

**注**  レジストリは、フィルター モジュールが省略可能なことを指定するフラグを含めることができます。 オプションのフィルター モジュールがアタッチされず、NDIS ドライバー スタックの残りの部分は終了しません。

 

フィルター ドライバーが要求を送信、受信したデータを示す、OID 要求を実行する、またはからの状態インジケーターを行うことはできません、*アタッチ*状態。 送信および受信操作ではサポートされて、*を実行している*と*一時停止中*状態。 OID 要求と状態インジケーターがでサポートされている、*一時停止*、*再開中*、*を実行している*、および*一時停止中*状態。

NDIS 呼び出し、 [ *FilterDetach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach)関数で NDIS が接続されているフィルター モジュールをデタッチする[ *FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)します。 詳細については、次を参照してください。[フィルター モジュールをデタッチ](detaching-a-filter-module.md)します。

 

 





