---
title: METransformNeedInput
description: METransformNeedInput イベントは、デバイス変換が入力を必要があることを示します。
ms.assetid: AACD80F6-90A1-4338-AE5B-4A9248747949
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d40168ae5fd48a8e5da49aa04aefbdabfd3cb24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579418"
---
# <a name="metransformneedinput"></a>METransformNeedInput


**METransformNeedInput**イベントは、デバイス変換が入力を必要があることを示します。

## <a name="span-idwhensentspanspan-idwhensentspanspan-idwhensentspanwhen-sent"></a><span id="When_sent"></span><span id="when_sent"></span><span id="WHEN_SENT"></span>送信されたときに


デバイス変換には、出力を生成する入力が必要がある場合は、このイベントが送信されます。 通常、非同期の仕様は、処理と、出力のサンプルを生成するための入力のサンプルを取得するのにこのメッセージを使用します。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


| パラメーター              | 説明                                                                                                   |
|------------------------|---------------------------------------------------------------------------------------------------------------|
| **入力ストリーム インデックス** | 入力ストリーム インデックスとして IMFMediaEvent 属性ストアに送信される**MF\_イベント\_MFT\_入力\_ストリーム\_ID**します。 |

 

## <a name="remarks"></a>コメント


このイベントは、次の理由でデバイス変換 manager (DTM) によって処理されません。

-   Devproxy には、入力ピンはありません。
-   デバイス MFT 入力ピンがある場合でも自動的に渡されるサンプル Devproxy の出力で使用できる場合。 そのため、デバイス MFT サンプルを要求する必要はありません。 DTM では、この要求は無視されます。

 

 





