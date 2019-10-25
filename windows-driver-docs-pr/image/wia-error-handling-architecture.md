---
title: WIA エラー処理アーキテクチャ
description: WIA エラー処理アーキテクチャ
ms.assetid: 2672a5ee-d860-44de-9e68-bd70377d58a8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d2a994c6e00e8b9d86ccb2f30ca14a3cb638959
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840702"
---
# <a name="wia-error-handling-architecture"></a>WIA エラー処理アーキテクチャ


WIA エラー処理アーキテクチャは、3つの部分で構成されています。 オペレーティングシステム、ドライバー、およびアプリケーション。 エラー処理メカニズムは、ストリームベースのデータ転送に依存しています。 この転送モデルは、Windows Vista 以降のオペレーティングシステムで使用できます。 この新しいエラー処理方法をサポートするために、この転送モデルを使用するには、WIA ドライバーを作成する必要があります。 同様に、ストリームベースの転送モデルをサポートするようにアプリケーションを記述して、この新しいエラー処理アーキテクチャに参加できるようにする必要もあります。

WIA エラー処理は、システムによって提供される、IHV 提供のコンポーネント、および ISV が提供するコンポーネントで構成されています。 次の図は、各コンポーネントの供給元を示しています。

![wia エラー処理コンポーネントを示す図](images/wia-error-wv.png)

考えられるエラーハンドラーには、アプリケーションエラーハンドラー、ドライバーエラーハンドラー、および既定のエラーハンドラーの3つがあります。 次の図は、これら3つのエラーハンドラーを示しています。

![3つの wia エラーハンドラーを示す図](images/wia-errorhandlers.png)

また、このイメージには、これら3つのエラーハンドラーが WIA プロキシコールバックによって試行される階層も示されています。

ほとんどの場合、これらのハンドラーは同じです。 ただし、いくつか違いがあります。 アプリケーションエラーハンドラーは**Iwiaapperrorhandler**インターフェイスを実装しますが、ドライバーエラー処理拡張機能と既定のエラーハンドラーは**IWiaErrorHandler**インターフェイスを実装します。 アプリケーションエラーハンドラーは、コールバックオブジェクトに実装する必要がある**Iwiatransfercallback**も使用します。

デバイスの状態コードは、 **IWiaErrorHandler:: reportstatus**の*hrstatus*パラメーターを使用してエラーハンドラーに渡されます。 これは、 **Iwiatransfercallback:: wiatransミニドライバー params**メソッドの*hrErrorStatus*パラメーターに設定されている値と同じです。

*Hrstatus*パラメーターが\_SUCCESS に設定されている場合、これは致命的ではない遅延を表します。 つまり、エラー処理 UI には、モードレス、情報ダイアログボックス、および転送をキャンセルする機会を提供するだけで済みます。 次にエラーハンドラーが異なる*Hrstatus*値を持つメッセージを受信したときに、UI を破棄する必要があります (エラーハンドラーでこのメッセージがサポートされているかどうか)。

**注**   [モードレスエラーハンドラー] ダイアログボックスは1つだけ表示されます。

 

エラーハンドラーは、デバイスステータスメッセージの重大度\_エラーに応答してモーダル UI を表示する必要があります。

WIA のエラー処理には、次の4つのコンポーネントが関係します。

<a href="" id="the-wia-minidriver"></a>**WIA ミニドライバー**  
ミニドライバーは、を使用して、Windows Vista の新しい、WIA\_TRANSFER\_MSG\_デバイス\_ステータスメッセージをデバイスレベルで発生したことを示すことができるようになりました。 ドライバーは、このメッセージを送信するときに、 **Iwiatransfercallback:: WiatranshrErrorStatus params**メソッドの (または、場合によっては*lpercentcomplete*率) パラメーターも設定する必要があります。 状態コードには、エラーまたは情報を指定できます。 エラー状態コードが発生した場合は、エラーを回復するためにユーザーの介入が必要です。 ドライバーは、 *hrErrorStatus*を定義済みの wia hresult 値に設定できます。たとえば、WIA\_ステータス\_ウォームアップ\_、独自のカスタム HRESULT を作成します。

<a href="" id="the-application-error-handler"></a>**アプリケーションエラーハンドラー**  
アプリケーションでエラー処理を有効にするためには、 **Iwiaapperrorhandler**インターフェイスを実装する必要があります。 このインターフェイスは、 **IWiaTransfer::D o)** メソッドおよび**IWiaTransfer:: Upload**メソッドに渡されるアプリケーションのコールバックオブジェクトによって実装されます。 このコールバックオブジェクトは、 **Iwiatransのコールバック**インターフェイスを実装するために必要です。 **Iwiaapperrorhandler**を実装することにより、アプリケーションは、データ転送中にエラーハンドラーを呼び出すことができることを示します。

<a href="" id="the-driver-s-error-handler"></a>**ドライバーのエラーハンドラー**  
ドライバーのエラーハンドラーは、 [IWiaErrorHandler インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nn-wia_lh-iwiaerrorhandler)を実装する必要があるドライバーの拡張機能です。 エラーハンドラーは、すべての状態コードの UI を処理および表示できます。これらの状態コードには、WIA で定義されている状態コードだけでなく、ドライバーに固有のステータスコードも含まれています。

<a href="" id="the-default-error-handler"></a>**既定のエラーハンドラー**  
既定のエラーハンドラーは、WIA によって実装されます。 このメソッドは、多数の一般的なデバイスステータスメッセージの UI を処理して表示します。 これらのメッセージには、情報とエラーの両方があります。たとえば、WIA\_エラー\_用紙\_詰まり、WIA\_ステータス\_ウォームアップ\_ます。

WIA プロキシでは、エラーメッセージ自体は処理されません。 代わりに、WIA プロキシによって、デバイスのステータスメッセージを処理する機会がエラーハンドラーに与えられます。

エラーハンドラーは、ユーザーがデータ転送を続行またはキャンセルできる状態にシステムを配置するための UI を提供します。

WIA\_転送\_MSG\_デバイス\_ステータスメッセージを受信すると、まず、アプリケーションエラーハンドラーの**Iwiaapperrorhandler:: ReportStatus**メソッドが呼び出されます。 アプリケーションコールバックルーチンがデバイスステータスコードを処理しない場合、WIA プロキシはドライバーエラーハンドラーの[**IWiaErrorHandler:: ReportStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiaerrorhandler-reportstatus)実装を呼び出し、最後に、wia プロキシが既定のエラーハンドラー**を呼び出します。IWiaErrorHandler:: ReportStatus**実装。 特定のハンドラーが存在しない場合 (たとえば、ドライバーがエラー処理拡張機能に付属していない場合)、またはドライバーのデバイスステータスハンドラーが WIA を返した場合\_状態\_\_処理されません。これは、ドライバーのハンドラーがサポートしていないことを示します。デバイスコードでは、チェーン内の次のハンドラーが使用されます。 デバイスのステータスメッセージが正常に処理されるか、失敗した場合、WIA プロキシコールバックはを返します。 そのため、ドライバーエラーハンドラーの**Reportstatus**メソッドがすべてのメッセージに対して s\_OK を返した場合、既定のエラーハンドラーはデバイスのステータスメッセージを処理する機会を得ることができません。

重大度\_エラー (エラーメッセージ) を含むデバイスステータスメッセージをサポートするエラーハンドラーがない場合、WIA プロキシはドライバーにステータスエラーを返します。このエラーは、転送を停止する必要があります。 ドライバーは、 [**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)からこの hresult 値を返し、アプリケーションは**IWiaTransfer::D O)** または**IWiaTransfer:: Upload**からこの hresult を受け取ります。

重大度\_成功 (情報メッセージ) を含むデバイスステータスメッセージを処理するエラーハンドラーがない場合、WIA プロキシからドライバーに\_OK が返されます。

**注**  アプリケーションのコールバックルーチン**Iwiatransfercallback:: Transfercallback**は、 *lmessage*が WIA に設定されたメッセージを受信することはありません\_転送\_MSG\_デバイス\_状態です。 代わりに、これらのメッセージがエラーハンドラーに送信されます。

 

**Iwiatransfercallback**、**iwiaapperrorhandler**、および**IWiaTransfer**インターフェイスについては、Microsoft Windows SDK のドキュメントを参照してください。

 

 




