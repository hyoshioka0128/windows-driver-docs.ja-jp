---
title: METransformHaveOutput
description: METransformHaveOutput イベントでは、デバイス変換が、出力ストリームのいずれかにサンプルの準備ができてを持つことを示します。
ms.assetid: 1CD11A3C-8181-4AF2-9AB3-10B04668CF1C
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb4e197292db24f0c882d80b8e5834a49b23ec2c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532330"
---
# <a name="metransformhaveoutput"></a>METransformHaveOutput


**METransformHaveOutput**イベントは、デバイス変換では、その出力ストリームのいずれかの準備ができてサンプルが用意を示します。

## <a name="span-idwhensentspanspan-idwhensentspanspan-idwhensentspanwhen-sent"></a><span id="When_sent"></span><span id="when_sent"></span><span id="WHEN_SENT"></span>送信されたときに


Devproxy またはデバイス MFT は、デバイス変換 manager (DTM) で取り上げられることに、出力ストリームの準備完了のサンプルがある場合、このイベントを発生させます。

Devproxy METransformHaveOutput が発生したときに、DTM は Devproxy で ProcessOutput を呼び出します。 結果として得られるサンプルは、デバイス MFT の対応する入力に渡すとします。

デバイス MFT を生成するとき**METransformHaveOutput**、DTM デバイス ソースにイベントを中継します。 デバイス ソースは、デバイス MFT にルーティングはデバイス Transform Manager でプロセスの出力を呼び出します。 したがってサンプルでは、デバイス ソースによって取得されるとし、メディア パイプライン入力します。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


なし。

## <a name="remarks"></a>注釈


デバイス MFT は、の合計の出力ストリームの数を受け取る**MFT\_出力\_データ\_バッファー**配列内の構造体。 構造体のメンバーを適切な値を入力すると想定されます。 応答のサンプルを取得するデバイス MFT に DTM 呼び出される前に、 **METransformHaveOutput**メッセージ、別のサンプルが、別のストリーム可能になる場合デバイス MFT はさあ、これで、サンプルを送信ProcessOutput 呼び出し。 DTM は ProcessOutput をもう一度、呼び出しが、その時点でデバイス MFT でしたのみを返す、呼び出しでは、サンプルはありませんが利用できない場合。

詳細については、次を参照してください。 [ **IMFDeviceTransform::ProcessOutput**](https://msdn.microsoft.com/library/windows/hardware/mt797682)します。

 

 





