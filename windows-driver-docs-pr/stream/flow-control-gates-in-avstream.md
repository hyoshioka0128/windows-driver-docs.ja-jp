---
title: AVStream のフロー制御ゲート
description: AVStream のフロー制御ゲート
ms.assetid: c5592f92-a432-44e3-afe0-60fcf917a443
keywords:
- AVStream ロジックゲート WDK
- ロジックゲート WDK AVStream
- ゲート WDK AVStream
- およびゲート WDK AVStream
- KSGATE
- フロー制御ゲート WDK AVStream
- コントロールゲートの処理 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55b860bf26eb7c88b31cd6302f4fcabcc849379c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842598"
---
# <a name="flow-control-gates-in-avstream"></a>AVStream のフロー制御ゲート





AVStream では、制御フロー機構としてロジックゲートが使用されます。 各ロジックゲートは、 [**Ksk ゲート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksgate)構造体によって表されます。

AVStream は、1つのおよびゲートで各フィルターまたはピンを初期化します。 ミニドライバーは、このメカニズムを使用して、特定のオブジェクトがいつデータを処理できるかを判断できます。 ピンの処理制御ゲートを取得するために、ミニドライバーは[**Kspingetandgate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetandgate)を呼び出します。 フィルターの処理制御ゲートを取得するには、 [**Ksk Filtergetandgate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksfiltergetandgate)を呼び出します。

新しいロジックゲートを作成するために、ミニドライバーは[**KsGateInitializeAnd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksgateinitializeand)または[**KsGateInitializeOr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksgateinitializeor)を呼び出します。 1つのゲートの出力を別のゲートへの入力として使用し、その結果、状態遷移を転送できます。 これを行うには、これらの呼び出しに*Nextorgate*パラメーターまたは*nextorgate*パラメーターを指定します。

ロジックゲートへの既存の入力を閉じるには、 [**KsGateTurnInputOff**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksgateturninputoff)を呼び出すことができます。 ミニドライバーは、アクティブな pin を停止および終了したり、無期限に処理を中断したりするために、この呼び出しを行う場合があります。

同様に、 [**KsGateTurnInputOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksgateturninputon)を呼び出して、特定のゲートへの既存の入力を開きます。

スレッドは、処理の準備が整うと、処理オブジェクトの処理を制御するおよびゲートの入力*時に*をキャプチャしようとします。 これを行うために、ミニドライバーは[**KsGateCaptureThreshold**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksgatecapturethreshold)を呼び出します。

およびゲートが開いている場合、AVStream はゲートへの入力をオフにし、処理を開始します。 処理中にゲートが閉じられるようになったため、他のスレッドがゲートの入力*時に*をキャプチャすることはできません。 一度に1つのスレッドのみがデータを処理できます。

変更せずにゲートの状態を確認するために、ミニドライバーは[**KsGateGetStateUnsafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksgategetstateunsafe)を呼び出すことができます。 ただし、この関数は同期を処理しないことに注意してください。

ロジックゲートを削除するには、 [**KsGateTerminateAnd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksgateterminateand)または[**KsGateTerminateOr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksgateterminateor)を呼び出します。 削除するゲートは、ゲートチェーンの先頭にある必要があります。

Pin をロジックゲートに入力としてアタッチした後、同じロジックゲートをフィルターの AND ゲートへの入力として接続するには、 [**KsPinAttachAndGate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinattachandgate)または[**KsPinAttachOrGate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinattachorgate)を呼び出します。

### <a name="determining-gate-status"></a>ゲートの状態の確認

およびゲートの場合、KSGATE 構造体の**Count**メンバーの値は、 *off*入力の数から1を引いた値になります。

Count = 1- *(入力数*が不足しています)

この値が0以下の場合、ゲートは閉じられます。 この値が0より大きい場合は、ゲートが開かれています。

またはゲートの場合、KSGATE の**Count**メンバーの値はゲートへ*の入力の数になり*ます。

Count = (入力*時*の数)

この値が0に等しい場合、ゲートは閉じられます。 **Count**が0より大きい場合は、ゲートが開かれています。

およびゲートの有効な**数**の範囲は1以下です。またはゲートの有効な**数**の範囲が0以上です。 **Count**を無効な値に設定しないでください。*Avstream では、ミニドライバーによってゲートが有効な状態に設定されているかどうかは検証されません。*

 

 




