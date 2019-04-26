---
title: METransformInputStreamStateChanged
description: METransformInputStreamStateChanged イベントは、入力ストリームの状態に、メディアの種類を変更する必要がありますを示します。
ms.assetid: 734080DD-8D96-4AF3-BB13-FDA8E0398C0B
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0384c0aae1672207c752bc42c5546cc1a8081555
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348355"
---
# <a name="metransforminputstreamstatechanged"></a>METransformInputStreamStateChanged


**METransformInputStreamStateChanged**イベントの入力ストリームの状態またはメディアの種類を変更する必要がありますのことを示します。

## <a name="span-idwhensentspanspan-idwhensentspanspan-idwhensentspanwhen-sent"></a><span id="When_sent"></span><span id="when_sent"></span><span id="WHEN_SENT"></span>送信されたときに


デバイス MFT 出力が変更されたときに、関連する入力ストリームの状態が変更する必要もあります。 この状況が発生したときにデバイス MFT を生成、 **METransformInputStreamStateChanged**イベント。

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


| パラメーター              | 説明                                                                     |
|------------------------|---------------------------------------------------------------------------------|
| **入力ストリーム インデックス** | 入力ストリームのインデックスは、IMFMediaEvent の属性ストアに設定する必要があります。 |

 

## <a name="remarks"></a>注釈


デバイス変換 manager (DTM) を呼び出すには、このイベントに応答して、 [ **GetInputStreamPreferredState** ](https://msdn.microsoft.com/library/windows/hardware/mt797670)で指定された入力ストリームのインデックスを持つデバイス MFT します。 デバイス MFT は、優先状態とメディアの種類を返します。

DTM を devproxy 出力ストリームに、要求されたメディアの種類を設定し、要求されたストリームの状態に移行します。 これが成功すると、DTM はデバイス MFT 入力ストリームで同じメディアの種類を設定し、要求された状態に移行します。 します。

このプロセス中にエラーがある場合、 **SetInputStreamStatedwStatus**パラメーターには、発生したエラーにが含まれます。 デバイス MFT は、に応じて DTM にエラーを伝達する必要があります。

指定したストリームが停止または実行中の状態の場合、このイベントを生成できます。 ストリームが停止状態である場合は、デバイス Transform Manager はそのデバイス MFT 入力ストリームの推奨される種類のクエリを実行し、Devproxy の出力に設定します。 失敗した場合、DTM はデバイス MFT の入力に同じ優先メディアの種類が設定されます。

ときにデバイス MFT は、ストリーミング、さらにサンプルの配信が停止して、入力デバイス MFT で推奨されるメディアの種類が要求されます中に、このイベントを生成します。 このメディアの種類は、Devproxy の出力に、デバイス MFT の入力に設定されます。 ストリームが Devproxy 出力ストリームに自動的に再起動され、サンプルは、デバイス MFT 入力ストリームに配信されます。 新しいサンプルが届いたら、デバイス MFT は関連する出力ストリームに、サンプルを提供します。

 

 





