---
title: モーション補正予測
description: モーション補正予測
ms.assetid: 02706369-2d99-4ac9-8dad-9e431acff42f
keywords:
- MCP WDK DirectX VA
- 動き補正 WDK DirectX VA
- DirectX のビデオ アクセラレータ WDK Windows 2000 の表示、ビデオのデコード
- ビデオ アクセラレータの WDK DirectX のビデオのデコード
- VA WDK DirectX、ビデオのデコード
- ビデオの WDK DirectX va なので、動き補正予測のデコード
- ビデオのデコード WDK DirectX va なので、動き補正の予測
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e21f0a8336ceab731cbc881f5866487a58c0251
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354259"
---
# <a name="motion-compensated-prediction"></a>モーション補正予測


## <span id="ddk_motion_compensated_prediction_gg"></span><span id="DDK_MOTION_COMPENSATED_PREDICTION_GG"></span>


ブロックの動き補償予測 (MCP) は、DirectX 問い合わせください。 によって実装される予測の種類 この予測の種類は、コーデックの MPEG および H.26x ファミリの利点は、純粋な静止コーディングなどのメソッド、JPEG を与えるもの。 ブロック ベースの予測以外の予測の動き補正の種類は、DirectX 問い合わせください。 で実装されていません。

動き補償の予測では、以前に送信され、デコードされたデータは、現在のデータの予測として使用できます。 予測と実際の現在のデータ値の違いは、予測誤差です。 コード化された予測のエラーは、入力データの最終的な表現を取得する予測に追加されます。 MCP に、コード化された予測誤差が追加されると、最終的なデコードされた画像は、後続のコード化された画像を生成する、MCP で使用されます。

この再帰ループは場合によっては、さまざまな種類の予測される要素に固有のリセットで区切られています。 デコードの処理のセマンティクスで、リセットのとおりです。 (たとえば、動きベクトルと係数の予測はリセットされますスライスの境界でテンポラル全体のフレームの予測チェーン内の更新、フレームがリセット中にします。)

次の図は、予測の動き補正のシグナル フローを示します。

![予測の動き補正のシグナルのフローを示す図](images/sigflow.png)

予測の動き補償が画像のコーディングに必要な手順は次のとおりです。

1.  参照ブロックは、以前にデコードされたフレームから抽出し、エンコード モードの選択と動きベクトルの各イメージのブロックの予測を作成するには、その他の予測コマンドで指定された変更はします。

2.  現在の入力データ ブロックと、予測の変換後の違いは、エンコーダーで使用可能なビット レートとできるだけ近似し、結果は、コード化された予測誤差として送信します。

3.  予測および予測の逆変換エラーは、画像を再構築されたブロックを形成する合計されます。

4.  画像を再構築されたブロックは、後続の図の予測に使用する参照フレーム バッファーに格納されます。

5.  このプロセスは、手順 1 でもう一度続行されます。

動きベクトル、DCT 係数、および直接、MCP の一部ではないその他のデータを処理する、データの送信されたフォームをよりコンパクトな採用の予測も。 予測のこれらのインスタンス上で実行される、*ホスト CPU*パーサーと変数の長さ-デコード ユニットのプロセッサまたはビット ストリーム。

 

 





