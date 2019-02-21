---
title: 処理がコールアウトを非同期的に分類します。
description: 処理がコールアウトを非同期的に分類します。
ms.assetid: 1026f917-7b21-4b01-8cfd-4d14e92106fe
keywords:
- WFP の非同期処理コールアウト WDK Windows フィルタ リング プラットフォームの分類します。
- Windows フィルタ リング プラットフォーム コールアウト ドライバー WDK、非同期処理のコールアウトを分類します。
- 保留中の WFP コールアウト WDK Windows フィルタ リング プラットフォームを分類します。
- コールアウト WDK Windows フィルタ リング プラットフォームを分類する非同期処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17932ca1577d5817bc23c46c5f7359424751429b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536334"
---
# <a name="processing-classify-callouts-asynchronously"></a>処理がコールアウトを非同期的に分類します。


WFP コールアウト ドライバーを承認または拒否のネットワーク操作または認めざるを得ませんまたはアクションの種類を返すことによって、ネットワーク パケットを破棄**FWP\_アクション\_許可**、 **FWP\_アクション\_続行**、または**FWP\_アクション\_ブロック**から、 [ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)コールアウト関数。 頻繁にコールアウト ドライバーが検査決定を返すことはできません、 *classifyFn*別に処理関数まで分類可能なフィールド、メタデータ、またはパケットをなど、指定された情報を転送できますユーザー モード アプリケーションなどのコンポーネント。 このような場合、意思決定が後で非同期に実行する必要があります。

### <a name="general-rules-for-asynchronous-processing"></a>非同期処理のための一般的な規則

WFP の非同期処理をサポートしている、 *classifyFn*コールアウト関数。 ただし、これを行うためのメカニズムは、さまざまな層によって異なります。

<a href="" id="asynchronous-ale-classify-------"></a>**非同期 ALE を分類します。**   
コールアウト ドライバーを呼び出す必要があります、 [ **FwpsPendOperation0** ](https://msdn.microsoft.com/library/windows/hardware/ff551199)関数*classifyFn*します。 呼び出して、非同期操作を完了する必要があります、 [ **FwpsCompleteOperation0** ](https://msdn.microsoft.com/library/windows/hardware/ff551152)関数。

<a href="" id="asynchronous-packet-classify-------"></a>**非同期のパケットを分類します。**   
コールアウト ドライバーを返す必要があります**FWP\_アクション\_ブロック**から、 *classifyFn*関数で、 **FWPS\_分類\_OUT\_フラグ\_吸収**フラグを設定します。 ネットワーク パケットは、複製または参照する必要があります。 複製または変更されたパケットを reinjecting いずれかまたはサイレント モードで、パケット破棄することによって、非同期操作が完了します。

<a href="" id="asynchronous-ale-classify-that-includes-packets-------"></a>**非同期 ALE を分類するパケットが含まれます**   
前の 2 つの手順の組み合わせを使用: 分類操作が保留の状態で、パケットが参照されている場合、または複製、およびいくつかの時間を後で呼び出し*classifyFn*が完了し、複製されたパケットがれるか、破棄されます。

### <a name="special-cases-and-considerations"></a>特殊なケースと考慮事項

<a href="" id="ale-connect-vs--receive-accept-layers-------"></a>**ALE Connect vs します。レイヤーの表示と同意します。**   
ときに**FwpsCompleteOperation0** 、保留を完了するために呼び出される、ALE での操作の分類層の接続 (**FWPS\_レイヤー\_ALE\_AUTH\_の接続\_V4**または**FWPS\_レイヤー\_ALE\_AUTH\_CONNECT\_V6**)、ALE の再認証操作の分類にトリガーされる、それぞれの ALE では、レイヤーを接続します。 コールアウト ドライバーは、検査を返す必要がありますこの再認証から意思決定は、操作を分類します。 エールを検出する再認証を確認して操作を分類するかどうか、 **FWP\_条件\_フラグ\_IS\_再認証**フラグを設定します。

コールアウト ドライバーは、各保留 ALE の一意の状態を維持する必要があります\_AUTH\_接続などの操作の分類の各を決定する検査が操作を分類方法を中に検索することができます、 **FwpsCompleteOperation0**-再認証をトリガーします。 パケットが参照されているまたは保留 ALE 中にクローンかどうか\_AUTH\_接続 (たとえば、非 TCP 接続の場合)、操作の分類、再認証が行われた後、れることができます。

ときに**FwpsCompleteOperation0** ALE が表示される同意の層での分類操作中に呼び出されます (**FWPS\_レイヤー\_ALE\_AUTH\_RECV\_ACCEPT\_V4**または**FWPS\_レイヤー\_ALE\_AUTH\_RECV\_ACCEPT\_V6**)、 **FwpsCompleteOperation0** ALE の再認証をトリガーしません。 代わりに新しい呼び出し*classifyFn*が再びに複製されたパケットのれるときに、変更が、フィルターをバイパスするほど重要でない場合は、受信します。 ALE から挿入された自己のクローンを許可\_RECV\_ACCEPT レイヤーが効果的に着信接続を承認します。 呼び出された後に、着信パケットを破棄して、着信接続を許可しないように場合は、 **FwpsCompleteOperation0**します。

<a href="" id="ale-reauthorization-------"></a>**ALE 再認証**   
エールのコールアウト ドライバーを再分類できます接続またはポリシーの変更 (追加または層でのフィルターを削除するなど) などのイベントが表示される同意レイヤーは、到着の新しいインターフェイスを検出し、IPsec を使用して接続を再入力します。 このような再認証は、呼び出すことによって保留をすることはできません**FwpsCompleteOperation0**、し、これを行う必要はありません。 コールアウト ドライバーでは、前述の再認証中に示されたプロセス パケットに規則を使用する必要があります。

ALE でその受信と送信パケットを再承認することができますに注意してください\_AUTH\_接続または ALE\_RECV\_ACCEPT レイヤー。 着信パケットを与えず、ALE でするなど、\_AUTH\_CONNECT レイヤー。 コールアウト ドライバーは、パケットの方向が、接続の方向と同じになると想定する必要があります。

<a href="" id="ale-flow-established-layers-------"></a>**ALE\_フロー\_確立したレイヤー**   
非同期処理は、これらの層でサポートされていません (**FWPS\_レイヤー\_ALE\_フロー\_確立した\_V4**または**FWPS\_レイヤーの\_ALE\_フロー\_確立した\_V6**)。

<a href="" id="inbound-transport-layers-------"></a>**受信\_トランスポート レイヤー**   
コールアウト ドライバーでは、ALE 分類で、受信処理を必要とするパケットの非同期処理は実行する必要があります (受信) のトランスポート層 (**FWPS\_レイヤー\_受信\_トランスポート\_V4**または**FWPS\_レイヤー\_受信\_トランスポート\_V6**)。 これを行うと干渉フローを作成できます。 WFP を呼び出すと、 *classifyFn*コールアウト関数に設定する受信トランスポート層で、 **FWPS\_メタデータ\_フィールド\_ALE\_分類\_必要な**ALE を必要とするこれらのパケット処理の分類のフラグを設定します。 コールアウト ドライバーは、受信からこのようなパケットを許可する必要があります\_トランスポート層とエールに到達するまで処理を延期する必要があります\_RECV\_ACCEPT レイヤー。

<a href="" id="stream-layers-------"></a>**ストリーム レイヤー**   
ストリーム レイヤーで (**FWPS\_レイヤー\_ストリーム\_V4**または**FWPS\_レイヤー\_ストリーム\_V6**)、TCP データ セグメントIP アドレスまたは TCP ヘッダーの代わりに示されます。 ストリーム レイヤーは 1 回の呼び出しで net バッファー リストのチェーンを示すことができますも、 *classifyFn*コールアウト関数。 WFP は、使用可能な特殊化された複製および挿入関数、 [ **FwpsCloneStreamData0** ](https://msdn.microsoft.com/library/windows/hardware/ff551149)と[ **FwpsStreamInjectAsync0**](https://msdn.microsoft.com/library/windows/hardware/ff551213)の使用するレイヤーの吹き出しをストリームします。

ストリーム レイヤーのデータの順次配送性質上、コールアウト ドライバー引き続きクローンを作成し、時間の長い、ストリーム データは引き続きデータを吸収する必要が保留中です。 指定したストリームのフローの操作を非同期と同期を混在させると、未定義の動作が発生することができます。

 

 





