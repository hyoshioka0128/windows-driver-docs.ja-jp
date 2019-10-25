---
title: コールアウトの種類
description: コールアウトの種類
ms.assetid: d9539403-7657-4e95-8791-309673d1207d
keywords:
- 保留中のパケット WDK Windows フィルタリングプラットフォーム
- コールアウトの種類 WDK Windows フィルタリングプラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca6f4829515cd5852b740c0f0118b7e2f043426a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841773"
---
# <a name="types-of-callouts"></a>コールアウトの種類


次の種類のコールアウトを WFP と共に使用できます。

<a href="" id="inline-inspection-callout-------"></a>**インライン検査の吹き出し**   
この種類のコールアウトは、常に、[*分類関数から*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)**続行\_\_アクション**を返します。また、ネットワークトラフィックは一切変更されません。 ネットワーク統計情報を収集するコールアウトは、この種類のコールアウトの一例です。

この種類のコールアウトの場合は、 [**Fwps\_ACTION0**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_action0_)構造体の**型**メンバーで指定されたフィルターアクションの種類を、[**コールアウト\_検査]\_[.fwp\_アクション**] に設定する必要があります。

<a href="" id="out-of-band-inspection-callout-------"></a>**帯域外検査の吹き出し**   
この種類のコールアウトでは、ネットワークトラフィックは変更されません。 代わりに、指定されたデータを "保留" することによって、 *classid*の年関数の外部で行われる検査を延期し、[パケット挿入関数](packet-injection-functions.md)のいずれかを使用して、保留中のデータを tcp/ip スタックに reinjecting します。 Pending は、最初に指定されたデータを複製し、次に、 **Fwps\_分類\_OUT\_フラグ**を持つ*classid*によって **\_アクション\_ブロック**を返すことによって実装されます。ビットセット。

<a href="" id="inline-modification-callout-------"></a>**インライン変更コールアウト**   
この種類のコールアウトでは、最初に指定されたデータの複製を作成し、次に複製を変更してから、最後に変更された複製を*classid*の年関数から tcp/ip スタックに挿入することで、ネットワークトラフィックを変更します。 また、この種類のコールアウトは、 **Fwps\_分類\_OUT\_フラグ**を持つ*classid*関数から **\_ブロックの\_アクション**を返します。

この種類のコールアウトのフィルターアクションの種類は、**吹き出し\_終了\_吹き出し\_アクション**に設定する必要があります。

<a href="" id="out-of-band-modification-callout-------"></a>**帯域外変更コールアウト**   
この種類のコールアウトでは、最初に、 *intentToModify*パラメーターが**TRUE**に設定されている[**FwpsReferenceNetBufferList0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsreferencenetbufferlist0)関数を使用して、指定されたパケットを参照します。 次に、コールアウトは、 **\_アクション\_ブロック**を**FWPS\_分類\_OUT\_フラグ**を使用して返します。このフラグは、 *classid*の関数からビットセットを吸収します。 パケットが*classid*によって変更される準備ができたら、コールアウトは参照されたパケットを複製します (複製されるとすぐに、元のパケットを逆参照できます)。 その後、コールアウトが複製を変更し、変更されたパケットを TCP/IP スタックに挿入します。

この種類のコールアウトのフィルターアクションの種類は、**吹き出し\_終了\_吹き出し\_アクション**に設定する必要があります。

<a href="" id="redirection-callout"></a>**リダイレクト吹き出し**  
この種類のコールアウトの詳細について[は、「Using Bind Or Connect リダイレクション](using-bind-or-connect-redirection.md)」を参照してください。

リダイレクトコールアウトには、次の2種類があります。

-   バインドリダイレクトの吹き出しを使用すると、コールアウトドライバーはソケットのローカルアドレスとローカルポートを変更できます。
-   接続リダイレクトの吹き出しを使用すると、コールアウトドライバーは接続のリモートアドレスとリモートポートを変更できます。

この種類のコールアウトのフィルターアクションの種類は、 **\_アクション\_許可**に設定する必要があります。

**Fwps\_分類\_OUT\_フラグ\_** の詳細については、「 [**fwps\_分類\_OUT0**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_classify_out0_)」を参照してください。 このフラグは、どの WFP 破棄レイヤーでも有効ではありません。 **\_アクション\_BLOCK**を**FWPS\_分類\_OUT\_フラグ**と共に返す\_、分類*関数から設定された*"吸収フラグ" を使用すると、パケットが警告なしに破棄されます。この方法では、パケットは、どの WFP 破棄レイヤーにもヒットしません。また、監査イベントが生成されません。

複製されたネットワークバッファーの一覧は変更できますが、たとえば、net buffer や MDLs を追加したり削除したりすることや、コールアウトでは、 [**FwpsFreeCloneNetBufferList0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsfreeclonenetbufferlist0)関数を呼び出す前に変更を元に戻す必要があります。

パケット検査、パケット変更、または接続リダイレクトを実行する他のコールアウトと共存させるには、パケットを参照/複製 reinject メカニズムで保留する前に、コールアウトによって、Fwps をクリアすることによって元のパケットを "ハード" にする必要があります。 **\_RIGHT\_ACTION\_** [**Fwps wps**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_classify_out0_)の**RIGHTS**メンバーでの書き込みフラグを作成します。これは、 *CLASSID*によって返される OUT0 構造体を\_分類します。 再挿入 **\_の権限を\_アクション\_書き込み**フラグが設定されている場合、 *classid*が呼び出されると (つまり、パケットが保留され、後でまたは変更される可能性があります)、コールアウトが表示を保留しないようにする必要があります。現在のアクションの種類。また、変更される可能性がある複製を挿入するために、より高重量のコールアウトを待機する必要があります。

コールアウトが分類を pends たびに**Fwps\_RIGHT\_ACTION\_WRITE**フラグを設定する必要があります。 コールアウトドライバーは、 **Fwps\_RIGHT\_action\_WRITE**フラグをテストして、コールアウトがアクションを返す権限を確認する必要があります。 このフラグが設定されていない場合でも、コールアウトは、前のコールアウトによって返された**許可操作\_許可**アクションを\_拒否するために、 **\_アクション\_ブロック**アクションを返すことができます。 [詳細検査にコールアウトを使用して](using-a-callout-for-deep-inspection.md)いる例では、フラグが設定されていない場合にのみ、関数が終了します。

[**FwpsPendOperation0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendoperation0)関数は、 **FWPM\_レイヤー\_ALE\_リソース**から送信されたパケットを保留するために使用され\_割り当て\_<em>XXX</em>、 **FWPM\_レイヤー\_ALE\_AUTH\_LISTEN\_** <em>XXX</em>、または**FWPM\_LAYER\_ALE\_AUTH\_CONNECT\_** <em>XXX</em> [管理のフィルターレイヤー](https://docs.microsoft.com/windows-hardware/drivers/network/management-filtering-layer-identifiers)に接続します。

[**FwpsPendClassify0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendclassify0)関数は、次の[実行時フィルタリングレイヤー](https://docs.microsoft.com/windows-hardware/drivers/network/run-time-filtering-layer-identifiers)から送信されるパケットを保留するために使用されます。

FWPS\_レイヤー\_ALE\_エンドポイント\_クロージャ\_V4 FWPS\_レイヤー\_ALE\_エンドポイント\_\_V6 FWPS\_レイヤー\_ALE\_接続\_リダイレクト\_V4 FWPS\_レイヤー\_ALE\_接続\_リダイレクト\_V6 FWPS\_レイヤー\_ALE\_バインド\_V4 FWPS\_レイヤー\_ALE\_バインド\_リダイレクト\_V6
 

 





