---
title: コールアウトの種類
description: コールアウトの種類
ms.assetid: d9539403-7657-4e95-8791-309673d1207d
keywords:
- 保留中のパケット WDK Windows フィルタ リング プラットフォーム
- 吹き出しは、WDK Windows フィルタ リング プラットフォームを種類します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f1475cbd66408c86560e29ff5fb3fbfe8097668
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358376"
---
# <a name="types-of-callouts"></a>コールアウトの種類


次の種類の吹き出しは、WFP で使用できます。

<a href="" id="inline-inspection-callout-------"></a>**インラインの検査の吹き出し**   
この種類の吹き出しは常に返します**FWP\_アクション\_続行**から、 [ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)関数し、ネットワークを変更しません任意の方法でトラフィックです。 ネットワークの統計情報を収集する吹き出しは、この種類の吹き出しの例を示します。

この種類の吹き出し、フィルター アクションの種類 (で指定された、**型**のメンバー、 [ **FWPS\_ACTION0** ](https://msdn.microsoft.com/library/windows/hardware/ff551215)構造) に設定する必要があります**FWP\_アクション\_コールアウト\_検査**します。

<a href="" id="out-of-band-inspection-callout-------"></a>**帯域外の検査の吹き出し**   
この種類の吹き出しには、ネットワーク トラフィックは変更されません。 代わりに、それを遅延外部で実行する任意の検査、 *classifyFn*関数「保留中」で指定されたデータと、TCP/IP に戻す保留データを reinjecting スタックのいずれかで、[パケット インジェクション関数](packet-injection-functions.md). 保留中の最初に返すことで後に、指定されたデータを複製することにより実装されます**FWP\_アクション\_ブロック**から、 *classifyFn*関数を持つ、 **FWPS\_分類\_アウト\_フラグ\_吸収**ビットが設定されます。

<a href="" id="inline-modification-callout-------"></a>**インラインの変更の吹き出し**   
この種類の吹き出しは、指定されたデータの複製を作成するネットワーク トラフィックを変更し、スタックからのクローンを変更して、TCP/IP に変更の複製を最後に挿入する、 *classifyFn*関数。 この種類の吹き出しも返します**FWP\_アクション\_ブロック**から、 *classifyFn*関数を持つ、 **FWPS\_分類\_アウト\_フラグ\_吸収**ビットが設定されます。

この種類の吹き出しのフィルター アクションの種類を設定する必要があります**FWP\_アクション\_コールアウト\_終端**します。

<a href="" id="out-of-band-modification-callout-------"></a>**帯域外の変更の吹き出し**   
まず、この種類の吹き出しを使用して、指定されたパケットを参照、 [ **FwpsReferenceNetBufferList0** ](https://msdn.microsoft.com/library/windows/hardware/ff551206)関数を持つ、 *intentToModify*パラメーターに設定**TRUE**します。 引き出し線を返します**FWP\_アクション\_ブロック**で、 **FWPS\_分類\_アウト\_フラグ\_吸収**ビットセットから、 *classifyFn*関数。 パケットが外部で変更する準備ができて場合*classifyFn*、引き出し線のクローンを作成、参照されているパケット (が複製するとすぐに元のパケットしは逆参照できます)。 引き出し線は、クローンを変更し、TCP/IP スタックに変更されたパケットを挿入します。

この種類の吹き出しのフィルター アクションの種類を設定する必要があります**FWP\_アクション\_コールアウト\_終端**します。

<a href="" id="redirection-callout"></a>**リダイレクトの吹き出し**  
この種類の吹き出しの詳細については、次を参照してください。 [Bind を使用して、または接続のリダイレクト](using-bind-or-connect-redirection.md)します。

これにはリダイレクト コールアウトの 2 つの種類があります。

-   バインド リダイレクトの吹き出しには、ローカル アドレスと、ソケットのローカル ポートを変更するコールアウト ドライバーができます。
-   接続のリダイレクトの吹き出しには、リモート アドレスおよび接続のリモートのポートを変更するコールアウト ドライバーができます。

この種類の吹き出しのフィルター アクションの種類に設定する必要があります**FWP\_アクション\_許可**します。

詳細については**FWPS\_分類\_アウト\_フラグ\_吸収**を参照してください[ **FWPS\_分類\_OUT0**](https://msdn.microsoft.com/library/windows/hardware/ff551229). このフラグは、WFP 破棄層では無効です。 返す**FWP\_アクション\_ブロック**で、 **FWPS\_分類\_アウト\_フラグ\_吸収**フラグの設定から、*classifyFn*関数原因が発生するパケットを破棄する、レイヤーを破棄するパケットはヒットしません、WFP のいずれかの方法でもは監査イベントを生成します。

複製された net バッファーのリストを変更ことはできますが、net バッファーまたは MDLs、またはその両方を追加または削除してコールアウト取り消す必要がありますこのような変更呼び出しの前に、 [ **FwpsFreeCloneNetBufferList0** ](https://msdn.microsoft.com/library/windows/hardware/ff551170)関数。

吹き出しが「ハード」にありますパケットが保留の参照/複製-削除-再挿入メカニズムを使用する前に、パケット インスペクション、パケットの変更、または接続のリダイレクトを実行するその他の付記との共存、-、をオフにすると、元のパケットをドロップ**FWPS\_右\_アクション\_書き込み**フラグ、 **rights**のメンバー、 [ **FWPS\_分類\_OUT0**](https://msdn.microsoft.com/library/windows/hardware/ff551229)によって返される構造体、 *classifyFn*関数。 場合、 **FWPS\_右\_アクション\_書き込み**フラグが設定されて*classifyFn*が呼び出されます (これは、パケット保留可能性がありますと後でれるか、変更)、引き出し線の表示を保留する必要があり、現在のアクション タイプを変更しないでください変更される可能性が複製を挿入する重要度を高く吹き出しを待つ必要があります。

**FWPS\_右\_アクション\_書き込み**コールアウトとれたを分類するたびに、フラグを設定する必要があります。 コールアウト ドライバーをテストする必要があります、 **FWPS\_右\_アクション\_書き込み**吹き出しを返すアクションの権限をチェックするフラグ。 このフラグが設定されていないかどうか、引き出し返すことができますが、 **FWP\_アクション\_ブロック**アクションを拒否するために、 **FWP\_アクション\_許可**アクションを前の引き出しによって返されました。 示した例では[コールアウトを使用して、詳細な検査の](using-a-callout-for-deep-inspection.md)関数の終了フラグが設定されていない場合だけです。

[ **FwpsPendOperation0** ](https://msdn.microsoft.com/library/windows/hardware/ff551199)関数から発信された保留パケットを使用して、 **FWPM\_レイヤー\_ALE\_リソース\_割り当て\_**<em>XXX</em>、 **FWPM\_レイヤー\_ALE\_AUTH\_リッスン\_** <em>XXX</em>、または**FWPM\_レイヤー\_ALE\_AUTH\_CONNECT\_**<em>XXX</em>[管理レイヤーをフィルタ リング](https://msdn.microsoft.com/library/windows/hardware/ff557101)します。

[ **FwpsPendClassify0** ](https://msdn.microsoft.com/library/windows/hardware/ff551197)関数を使用して、次から発信された保留パケット[実行時のフィルター処理レイヤー](https://msdn.microsoft.com/library/windows/hardware/ff570731):

FWPS\_レイヤー\_ALE\_エンドポイント\_クロージャ\_V4 FWPS\_レイヤー\_ALE\_エンドポイント\_クロージャ\_V6 FWPS\_レイヤー\_ALE\_CONNECT\_リダイレクト\_V4 FWPS\_レイヤー\_ALE\_CONNECT\_リダイレクト\_V6 FWPS\_レイヤー\_ALE\_バインド\_リダイレクト\_V4 FWPS\_レイヤー\_ALE\_バインド\_リダイレクト\_V6
 

 





