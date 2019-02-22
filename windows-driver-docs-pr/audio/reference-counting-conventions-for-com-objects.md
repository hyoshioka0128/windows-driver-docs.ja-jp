---
title: COM オブジェクトの参照カウントの規則
description: COM オブジェクトの参照カウントの規則
ms.assetid: e6b19110-37e2-4d23-a528-6393c12ab650
keywords:
- COM オブジェクトの参照の WDK オーディオ
- オブジェクト参照の WDK オーディオ
- 参照の WDK オーディオのカウント
- 参照カウントの WDK オーディオ
- 入力パラメーターの参照カウントの WDK オーディオ
- 出力パラメーターの参照カウント WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d67224669169850ce0047d5a7317364d59035520
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539061"
---
# <a name="reference-counting-conventions-for-com-objects"></a>COM オブジェクトの参照カウントの規則


## <span id="reference_counting_conventions_for_com_objects"></span><span id="REFERENCE_COUNTING_CONVENTIONS_FOR_COM_OBJECTS"></span>


オーディオのインターフェイスのメソッドでは、一般的な一連の入力パラメーターとして取得または出力パラメーターとして返す COM オブジェクトの参照カウントの規則に従います。 これらの規則と、その例外は、次に示します。 COM インターフェイスの詳細については、Microsoft Windows SDK ドキュメントの [COM] セクションを参照してください。

### <a name="span-idreferencecountingoninputparametersspanspan-idreferencecountingoninputparametersspanspan-idreferencecountingoninputparametersspanreference-counting-on-input-parameters"></a><span id="Reference_Counting_on_Input_Parameters"></span><span id="reference_counting_on_input_parameters"></span><span id="REFERENCE_COUNTING_ON_INPUT_PARAMETERS"></span>入力パラメーターの参照カウント

オブジェクトへの参照がメソッドを呼び出しているいつ*X*入力パラメーターとして、呼び出し元する必要があります、独自の参照を保持オブジェクトの呼び出しの実行中です。 この動作は、メソッドのことを確認するために必要なオブジェクトへのポインター *X*は、返されるまで有効です。 場合、オブジェクト*Y*実装がこのメソッドは、オブジェクトへの参照を保持する必要がある*X*このメソッドからの戻り値を超えるメソッドを呼び出す必要があります[ **AddRef**](https://msdn.microsoft.com/library/windows/desktop/ms691379)オブジェクトで*X*を返す前にします。 オブジェクトと*Y*オブジェクトを使用して後で完了*X*を呼び出す必要が[**リリース**](https://msdn.microsoft.com/library/windows/desktop/ms682317)オブジェクトで*X*します。

たとえば、 [ **IServiceGroup::AddMember** ](https://msdn.microsoft.com/library/windows/hardware/ff536996)メソッド呼び出し[ **AddRef** ](https://msdn.microsoft.com/library/windows/desktop/ms691379)上、 [IServiceSink](https://msdn.microsoft.com/library/windows/hardware/ff537006)サービス グループに追加されるオブジェクト。 この動作を補完する、 [ **IServiceGroup::RemoveMember** ](https://msdn.microsoft.com/library/windows/hardware/ff537001)メソッド呼び出し[**リリース**](https://msdn.microsoft.com/library/windows/desktop/ms682317) IServiceSink オブジェクトをサービスのグループから削除します。

### <a name="span-idreferencecountingonoutputparametersspanspan-idreferencecountingonoutputparametersspanspan-idreferencecountingonoutputparametersspanreference-counting-on-output-parameters"></a><span id="Reference_Counting_on_Output_Parameters"></span><span id="reference_counting_on_output_parameters"></span><span id="REFERENCE_COUNTING_ON_OUTPUT_PARAMETERS"></span>出力パラメーターの参照カウント

Output パラメーターを通じて、呼び出し元へのオブジェクト参照を渡すメソッドを呼び出す必要があります[ **AddRef** ](https://msdn.microsoft.com/library/windows/desktop/ms691379)オブジェクトを返します前に (またはオブジェクトに独自の参照を解放する前に)。 この動作は、呼び出し元が、呼び出しからの戻り時に有効な参照を保持していることを確認する必要があります。 呼び出し元が通話を担当[**リリース**](https://msdn.microsoft.com/library/windows/desktop/ms682317)オブジェクトを使用してこれが完了するとします。

たとえば、 [ **IMiniportWaveCyclic::NewStream** ](https://msdn.microsoft.com/library/windows/hardware/ff536723)メソッド呼び出し[ **AddRef** ](https://msdn.microsoft.com/library/windows/desktop/ms691379)ストリーム、サービスのグループおよび DMA チャネル呼び出し元 (WaveCyclic ポート ドライバー) に出力するオブジェクト。 呼び出し元が不要になった必要になった場合は、これらの参照を解放する責任を負います。 実装については、 **IMiniportWaveCyclic::NewStream**方式でこの動作は、Sb16 サンプル アダプターで、Microsoft Windows Driver Kit (WDK) を参照してください。

### <a name="span-idexceptionstotherulesspanspan-idexceptionstotherulesspanspan-idexceptionstotherulesspanexceptions-to-the-rules"></a><span id="Exceptions_to_the_Rules"></span><span id="exceptions_to_the_rules"></span><span id="EXCEPTIONS_TO_THE_RULES"></span>ルールの例外

このメソッドを実行する一般的な参照カウントの説明については、*もできます*出力パラメーターは、「 [ **IMiniportWavePci::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536735)します。

 

 




