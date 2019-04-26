---
title: METransformFlushInputStream イベント
description: METransformFlushInputStream イベントは、デバイス MFT の入力に接続されている devproxy の出力ストリームをフラッシュするデバイス Transform Manager を通知します。
ms.assetid: 400FB4BE-90F2-4FF2-A709-7E213D99DCC8
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bb03fc58935a0788ec818b85311c6e215f455ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353690"
---
# <a name="metransformflushinputstream-event"></a>METransformFlushInputStream イベント


**METransformFlushInputStream**イベント デバイス MFT の入力に接続されている devproxy の出力ストリームをフラッシュするデバイス Transform Manager に通知します。

これは、デバイス MFT の特定の出力を取得フラッシュされたときに必要です、デバイス MFT の対応する入力と接続されている devproxy ストリームをフラッシュする必要があります。

## <a name="span-idwhensentspanspan-idwhensentspanspan-idwhensentspanwhen-sent"></a><span id="When_sent"></span><span id="when_sent"></span><span id="WHEN_SENT"></span>送信されたときに


デバイス MFT の出力が変更またはフラッシュ、関連する入力ストリームは、フラッシュ必要があります。 この条件が発生した場合、デバイス MFT は、このイベントを生成します。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


| パラメーター              | 説明                                                                     |
|------------------------|---------------------------------------------------------------------------------|
| **入力ストリーム インデックス** | 入力ストリームのインデックスは、IMFMediaEvent の属性ストアに設定する必要があります。 |

 

## <a name="remarks"></a>注釈


デバイス MFT の入力ストリームの接続されているストリームをフラッシュする必要があるとき、に、このイベントを生成します。 このイベントに応答して、DTM を呼び出して、 [ **FlushOutputStream** ](https://msdn.microsoft.com/library/windows/hardware/mt797665) 、Devproxy との接続されているストリームに呼び出す[ **FlushInputStream** ](https://msdn.microsoft.com/library/windows/hardware/mt797664) MFT デバイス。 デバイス MFT は、入力ストリームをフラッシュし、フラッシュ操作は完了と見なされます。

一般に、ストリーム自体が状態または停止するを実行している際にこのイベントは呼び出されます。

 

 





