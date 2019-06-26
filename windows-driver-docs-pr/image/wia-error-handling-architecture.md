---
title: WIA エラー処理アーキテクチャ
description: WIA エラー処理アーキテクチャ
ms.assetid: 2672a5ee-d860-44de-9e68-bd70377d58a8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d5d175fe245af2b5d2832f3d0959cf5b35d6d2d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383755"
---
# <a name="wia-error-handling-architecture"></a>WIA エラー処理アーキテクチャ


WIA エラー処理アーキテクチャは、3 つの部分で構成されます。 オペレーティング システム、ドライバーおよびアプリケーション。 エラー処理機構は、ストリーム ベースのデータ転送に依存します。 この転送モデルは Windows Vista 以降のオペレーティング システムで使用できます。 させる WIA ドライバーを記述する必要がありますこの新しいエラーの処理方法論をサポートする場合は、この転送モデルを使用します。 同様に、アプリケーションは、この新しいエラー処理アーキテクチャに参加できるストリーム ベースの転送モデルをサポートするためにも作成する必要があります。

WIA エラー処理は、システムが指定した、IHV が指定した、および ISV が指定したコンポーネントで構成されます。 次の図は、各コンポーネントの提供元を示します。

![wia エラー処理コンポーネントを示す図](images/wia-error-wv.png)

次の 3 つの考えられるエラー ハンドラーがある: アプリケーションのエラー ハンドラー、ドライバー エラー ハンドラー、および既定のエラー ハンドラー。 これらの 3 つのエラー ハンドラーは、次の図に表示されます。

![次の 3 つの wia エラー ハンドラーを示す図](images/wia-errorhandlers.png)

イメージには、WIA プロキシ コールバックによって試行されるこれらの 3 つのエラー ハンドラーの階層も表示されます。

ほとんどの面では、これらのハンドラーは同じです。 ただし、いくつかある相違点。 アプリケーションのエラー ハンドラーの実装、 **IWiaAppErrorHandler**インターフェイスの拡張機能と、既定のエラー ハンドラーを渡すドライバー エラー実装は、 **IWiaErrorHandler**インターフェイス。 また、アプリケーションのエラー ハンドラーを使用**IWiaTransferCallback**、コールバック オブジェクトで実装されている必要があります。

デバイスの状態コードがエラー ハンドラーに渡される、 *hrStatus*パラメーターの**IWiaErrorHandler::ReportStatus**します。 これは、同じ値で、ミニドライバーの設定、 *hrErrorStatus*のパラメーター、 **IWiaTransferCallback::WiaTransferParams**メソッド。

場合、 *hrStatus*パラメーターが 重大度に設定されている\_成功すると、致命的でない遅延を表します。 これはモードレスで情報のダイアログ ボックスと転送をキャンセルする機会に、UI の処理エラーが単なる提供することを意味します。 次に、エラー ハンドラーが、別のメッセージを受信、UI を破棄する必要があります*hrStatus* (かどうか、エラー ハンドラーがこのメッセージをサポートする) 値。

**注**  と同時に 1 つだけのモードレスのエラー ハンドラー ダイアログ ボックスを表示できます。

 

エラー ハンドラーは、重要度のデバイスのステータス メッセージへの応答でモーダル UI を表示する\_エラー。

WIA エラーの処理には、4 つのコンポーネントがあります。

<a href="" id="the-wia-minidriver"></a>**WIA ミニドライバー**  
ミニドライバーを使用できますが、新しい Windows Vista では、WIA\_転送\_MSG\_デバイス\_状態のデバイスのステータス メッセージをデバイス レベルで何かが発生したことを示します。 設定する必要がありますも、ドライバーは、このメッセージを送信するとき、 *hrErrorStatus* (および場合によっても、 *lPercentComplete*) のパラメーター、 **IWiaTransferCallback::WiaTransferParams**メソッド。 状態コードは、エラーまたは情報のいずれかを指定できます。 エラー状態コードが発生した場合、エラーは回復を提供する、エラーから回復するユーザーの介入が必要です。 ドライバーを設定できます*hrErrorStatus* WIA など、定義済み WIA HRESULT の値に\_状態\_WARMING\_UP、または独自のカスタムの HRESULT を作成します。

<a href="" id="the-application-error-handler"></a>**アプリケーションのエラー ハンドラー**  
アプリケーション エラー処理を有効にするためには、これを実装する必要があります、 **IWiaAppErrorHandler**インターフェイス。 このインターフェイスは、アプリケーションのコールバック オブジェクトに渡されることを**IWiaTransfer::Download**と**IWiaTransfer::Upload**メソッド。 このコールバック オブジェクトが実装するために必要な**IWiaTransferCallback**インターフェイス。 実装することによって**IWiaAppErrorHandler**アプリケーションでは、データの転送時に呼び出されるエラー ハンドラーができることを示します。

<a href="" id="the-driver-s-error-handler"></a>**ドライバーのエラー ハンドラー**  
ドライバーのエラー ハンドラーは、ドライバーの拡張機能を実装する必要がある、 [IWiaErrorHandler インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwiaerrorhandler)します。 エラー ハンドラーが処理およびすべての状態コードの UI を表示これらのステータス コードには、WIA 定義のステータス コードと同様に、ドライバー固有の状態コードが含まれます。

<a href="" id="the-default-error-handler"></a>**既定のエラー ハンドラー**  
既定のエラー ハンドラーは、WIA によって実装されます。 処理し、さまざまな汎用デバイス ステータス メッセージの UI が表示されます。 これらのメッセージは、両方の情報と例については、エラー。WIA\_エラー\_用紙\_詰まり、WIA\_状態\_WARMING\_をします。

WIA プロキシ処理しませんエラー メッセージ自体。 代わりに、WIA プロキシは、エラー ハンドラーがデバイスのステータス メッセージを処理します。

エラー ハンドラーは、システム状態データ転送を続行またはキャンセルできますを挿入しようとするユーザーを許可する UI を提供します。

WIA を受信するときに\_転送\_MSG\_デバイス\_ステータス メッセージ、WIA プロキシはまず、アプリケーション エラー ハンドラーの呼び出し**IWiaAppErrorHandler::ReportStatus**メソッド。 WIA プロキシがドライバー エラー ハンドラーを呼び出すアプリケーションのコールバック ルーチンがデバイスの状態コードを処理しない場合[ **IWiaErrorHandler::ReportStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nf-wia_lh-iwiaerrorhandler-reportstatus)実装、および最後に、WIAプロキシは既定のエラー ハンドラーを呼び出します**IWiaErrorHandler::ReportStatus**実装します。 指定されたハンドラーが存在しない場合 (たとえば、ドライバー可能性がありますに付属していない、エラー処理拡張機能)、ドライバーのデバイスの状態のハンドラーは、WIA を返す場合、または\_状態\_いない\_処理済みであることを示す、ドライバーのハンドラーデバイス コードをサポートしていません、チェーン内の次のハンドラーは、機会が与えられます。 正常にまたはした場合も、デバイスのステータス メッセージが処理された後は、WIA プロキシ コールバックを返します。 したがって、ドライバー エラー ハンドラーの**ReportStatus**メソッドを返します。 S\_OK、すべてのメッセージに対して既定のエラー ハンドラーがする機会がない任意のデバイスのステータス メッセージを処理します。

エラー ハンドラーは、重大度を持つは、デバイスのステータス メッセージ サポートしないかどうか\_エラー (エラー メッセージ)、WIA プロキシ エラーが返されます、状態に、ドライバーは、さらに、転送を中止する必要があります。 ドライバーは、この結果の HRESULT 値を返す必要があります[ **IWiaMiniDrv::drvAcquireItemData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)アプリケーションからこの HRESULT を受け取ることは、 **IWiaTransfer::Download**または**IWiaTransfer::Upload**します。

エラー ハンドラーは、重大度を持つは、デバイスの状態メッセージ処理しないかどうか\_WIA プロキシが返されます成功 (情報メッセージ)、S\_ドライバーには、[ok] です。

**注**  アプリケーションのコールバック ルーチン、 **IWiaTransferCallback::TransferCallback**、メッセージを受け取ることはなくなります*lMessage* WIA に設定\_転送\_MSG\_デバイス\_状態。 代わりに、これらのメッセージは、エラー ハンドラーに送信されます。

 

**IWiaTransferCallback**、**IWiaAppErrorHandler**、および**IWiaTransfer**インターフェイスが、Microsoft Windows SDK ドキュメントに記載されています。

 

 




