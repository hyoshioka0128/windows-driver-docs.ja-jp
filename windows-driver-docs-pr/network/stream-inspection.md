---
title: Stream の検査
description: Stream の検査
ms.assetid: 77e152bf-cb6b-4845-9a5e-9c37281f23f1
keywords:
- ストリームの検査 WDK Windows フィルタ リング プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 417c41cd9c9c736c166c369d61d5579cc0677b64
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552062"
---
# <a name="stream-inspection"></a>Stream の検査


## <a name="inline-stream-inspection"></a>インライン Stream の検査


インライン ストリーム修飾子を許可またはブロックしている指定されたデータの一部の値を設定がストリームのデータを編集できる、 **countBytesEnforced**のメンバー、 [ **FWPS\_ストリーム\_コールアウト\_IO\_PACKET0** ](https://msdn.microsoft.com/library/windows/hardware/ff552417)構造を返す**FWP\_アクション\_許可**または**FWP\_アクション\_ブロック**から、 [ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)コールアウト関数。 呼び出すことができます、 [ **FwpsStreamInjectAsync0** ](https://msdn.microsoft.com/library/windows/hardware/ff551213)ストリームに新しいコンテンツを追加する関数。 このコンテンツは新しいまたはブロックされているデータを置き換えることができます。

指定されたセグメントの途中で見つかったパターンを置き換える (たとえば、 *n*バイト数が続くパターンの*p*バイト数が続く*m*バイト)、吹き出しは次の次の手順:

1.  吹き出しの*classifyFn*を使用して関数を呼び出す*n* + *p* + *m*バイト。

2.  引き出し線を返します**FWP\_アクション\_許可**で、 **countBytesEnforced**メンバーに設定*n*します。

3.  吹き出しの*classifyFn*関数の呼び出しでもう一度*p* + *m*バイト。 WFP は呼び出す*classifyFn*もう一度場合**countBytesEnforced**が指定された量よりも少ない。

4.  *ClassifyFn*関数では、引き出し線の呼び出し、 *FwpsStreamInjectAsync0*関数を挿入、置換パターン*p'* します。 引き出し線を返します**FWP\_アクション\_ブロック**で**countBytesEnforced**に設定*p*します。

5.  吹き出しの*classifyFn*関数の呼び出しでもう一度*m*バイト。

6.  引き出し線を返します**FWP\_アクション\_ブロック**で**countBytesEnforced**に設定*m*します。

指定されたデータがコールアウトの検査を決定するのに十分ではない場合は設定できます、 **streamAction**のメンバー、 [ **FWPS\_ストリーム\_コールアウト\_IO\_PACKET0** ](https://msdn.microsoft.com/library/windows/hardware/ff552417)構造体を**FWPS\_ストリーム\_アクション\_必要\_詳細\_データ**設定と、 **countBytesRequired**最小限 WFP へのメンバーは、データが再度示される前に蓄積する必要があります。 ときに**streamAction**が設定された場合、引き出し線を返す必要があります**FWP\_アクション\_NONE**から、 *classifyFn*関数。

WFP は最大 8 MB のデータのストリームを累積できるときに**FWPS\_ストリーム\_アクション\_必要があります\_詳細\_データ**設定されています。 WFP は設定、 **FWPS\_分類\_アウト\_フラグ\_バッファー\_制限\_に達しました**フラグの吹き出しを呼び出すときに*classifyFn*関数とバッファー領域が不足します。 後者のフラグが設定されている場合、引き出し線は、完全に指定されたデータを受け入れる必要があります。 吹き出しが返す必要がありますいない**FWPS\_ストリーム\_アクション\_必要\_詳細\_データ**ときに、 **FWPS\_分類\_OUT\_フラグ\_いいえ\_詳細\_データ**フラグを設定します。

フラット バッファーからストリームのパターンをスキャンできる使いやすいように、WFP が提供、 [ **FwpsCopyStreamDataToBuffer0** ](https://msdn.microsoft.com/library/windows/hardware/ff551157)ユーティリティ関数をコピーできますに連続したストリーム データを表示します。バッファー。

## <a name="out-of-band-stream-inspection"></a>帯域外の Stream 検査


ストリーム コールアウト帯域外の検査または変更は、パケット検査コールアウトとしてのようなパターンに従うと: 遅延の処理のすべてのストリームが指定されたセグメントを最初に複製する場合し、これらのセグメントはブロックされます。 検査または変更されたデータは後で、データ ストリームに挿入されます。 データの帯域外を挿入するときに、引き出しを返す必要があります**FWP\_アクション\_ブロック**すべてでセグメント結果のストリームの整合性を保証するために示されます。 帯域外の検査モジュールが、送信のデータ ストリームに (を送信者からデータを示す) FIN を任意に挿入していない必要があります。 場合は、モジュールは、接続を削除する必要があります、 *classifyFn*コールアウト関数を設定する必要があります、 **streamAction**のメンバー、 [ **FWPS\_ストリーム\_吹き出し\_IO\_PACKET0** ](https://msdn.microsoft.com/library/windows/hardware/ff552417)構造体を**FWPS\_ストリーム\_アクション\_ドロップ\_接続**.

ストリーム データは、として指定することができますので、 [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)チェーン、FWP の提供、 [ **FwpsCloneStreamData0**](https://msdn.microsoft.com/library/windows/hardware/ff551149)と[ **FwpsDiscardClonedStreamData0** ](https://msdn.microsoft.com/library/windows/hardware/ff551161) net バッファーを操作するユーティリティ関数チェーンを一覧表示します。

WFP は、ストリーム データが入力方向の調整もサポートします。 それを返すことができるかどうか、コールアウトは、受信データ速度追い付かことはできません、 **FWPS\_ストリーム\_アクション\_DEFER**ストリームを「一時停止」にします。 ストリームから「再開できる」を呼び出して、 [ **FwpsStreamContinue0** ](https://msdn.microsoft.com/library/windows/hardware/ff551210)関数。 受信データの確認処理を停止する TCP/IP スタックは、この関数でストリームを延期します。 これにより、TCP のスライディング ウィンドウを 0 方向に減らします。

帯域外のストリーム検査のコールアウトの[ **FwpsStreamContinue0** ](https://msdn.microsoft.com/library/windows/hardware/ff551210)呼び出さないでください中に、 **FwpsStreamInjectAsync0**関数が呼び出されます。

挿入されたストリーム データを吹き出しに再指定にすることはできませんが、利用可能になりますストリームの吹き出しに下位重みサブレイヤーから。

[Windows フィルタ リング プラットフォーム Stream サンプルの編集](https://go.microsoft.com/fwlink/p/?LinkId=617933)で、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリには、インライン コード スニペットとストリーム レイヤーでの帯域外の編集を実行する方法を示します。

**注**  Windows Server 2008 以降は、次のプロセス中にストリームのフィルターの削除をサポートしていません。
-   引き出し線では、帯域外のパケットの挿入を実行します。

-   引き出し線が設定してより多くのデータを要求する、 **streamAction**のメンバー、 [ **FWPS\_ストリーム\_コールアウト\_IO\_PACKET0**](https://msdn.microsoft.com/library/windows/hardware/ff552417)構造体を**FWPS\_ストリーム\_アクション\_必要\_詳細\_データ**します。

-   引き出し線を延期するストリームと設定して、 **streamAction**のメンバー、 [ **FWPS\_ストリーム\_コールアウト\_IO\_PACKET0**](https://msdn.microsoft.com/library/windows/hardware/ff552417)構造体を**FWPS\_ストリーム\_アクション\_DEFER**します。

 

## <a name="dynamic-stream-inspection"></a>動的な Stream 検査


Windows 7 およびそれ以降のサポート動的ストリーム検査します。 ストリームが動的な検査は、既存のストリームを作成して、新しいリソースの破棄ではなく、データ フローです。 動的なストリームの検査を実行できるコールアウト ドライバーを設定する必要があります、 **FWP\_コールアウト\_フラグ\_許可\_MID\_ストリーム\_検査**フラグ、**フラグ**のメンバー、 [ **FWPS\_CALLOUT1** ](https://msdn.microsoft.com/library/windows/hardware/ff551226)または[ **FWPS\_CALLOUT2** ](https://msdn.microsoft.com/library/windows/hardware/hh439700)構造体。

## <a name="avoiding-unnecessary-inspections"></a>不要な検査を回避します。


ストリームの検査をドライバーに関心が接続でのみ実行する吹き出しを設定できます、 **FWP\_コールアウト\_フラグ\_条件付き\_ON\_フロー**フラグ、**フラグ**のメンバー、 [ **FWPS\_CALLOUT0** ](https://msdn.microsoft.com/library/windows/hardware/ff551224)構造体。 その他のすべての接続でこの吹き出しは無視されます。 パフォーマンスが向上して、ドライバーが不要な状態データを保持する必要はありません。

## <a name="stream-layer-waterfall-model"></a>Stream レイヤー ウォーター フォール モデル

WFP のストリーム レイヤーは、厳密なウォーター フォール モデルに依存します。このレイヤーに引き出しを許可する場合のみストリームのセグメントを検査するは、明示的に許可している場合前の吹き出し (ある場合)。 コールアウトは、指定されたセグメントをブロックする場合は、そのセグメントは、ストリームから外されます完全にされ、検査コールアウトは許可されません。

さらに：

1. すべて非検査コールアウト ストリーム レイヤーする必要があります明示的に値を割り当てる、 **actionType**のメンバー、 *classifyOut*にかかわらず、どのような値が以前に設定されているパラメーターパラメーター。
2. **FWPS\_右\_アクション\_書き込み**フラグ、 **rights**のメンバー、 *classifyOut*パラメーターには意味がありませんWFP ストリーム レイヤー。 このフラグが存在するこのレイヤーでのコールアウトがチェックする必要があります。 吹き出しを指定された処理*データ*パラメーターの値に関係なく*classifyOut*->**rights**します。

 

 





