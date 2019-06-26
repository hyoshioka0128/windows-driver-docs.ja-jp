---
title: COM オブジェクト用の参照カウントの規則
description: COM オブジェクト用の参照カウントの規則
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
ms.openlocfilehash: d75ff9b24b96ea6acd2179fe843ff931f9369be1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362528"
---
# <a name="reference-counting-conventions-for-com-objects"></a>COM オブジェクト用の参照カウントの規則


## <span id="reference_counting_conventions_for_com_objects"></span><span id="REFERENCE_COUNTING_CONVENTIONS_FOR_COM_OBJECTS"></span>


オーディオのインターフェイスのメソッドでは、一般的な一連の入力パラメーターとして取得または出力パラメーターとして返す COM オブジェクトの参照カウントの規則に従います。 これらの規則と、その例外は、次に示します。 COM インターフェイスの詳細については、Microsoft Windows SDK ドキュメントの [COM] セクションを参照してください。

### <a name="span-idreferencecountingoninputparametersspanspan-idreferencecountingoninputparametersspanspan-idreferencecountingoninputparametersspanreference-counting-on-input-parameters"></a><span id="Reference_Counting_on_Input_Parameters"></span><span id="reference_counting_on_input_parameters"></span><span id="REFERENCE_COUNTING_ON_INPUT_PARAMETERS"></span>入力パラメーターの参照カウント

オブジェクトへの参照がメソッドを呼び出しているいつ*X*入力パラメーターとして、呼び出し元する必要があります、独自の参照を保持オブジェクトの呼び出しの実行中です。 この動作は、メソッドのことを確認するために必要なオブジェクトへのポインター *X*は、返されるまで有効です。 場合、オブジェクト*Y*実装がこのメソッドは、オブジェクトへの参照を保持する必要がある*X*このメソッドからの戻り値を超えるメソッドを呼び出す必要があります[ **AddRef**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)オブジェクトで*X*を返す前にします。 オブジェクトと*Y*オブジェクトを使用して後で完了*X*を呼び出す必要が[**リリース**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)オブジェクトで*X*します。

たとえば、 [ **IServiceGroup::AddMember** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicegroup-addmember)メソッド呼び出し[ **AddRef** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)上、 [IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)サービス グループに追加されるオブジェクト。 この動作を補完する、 [ **IServiceGroup::RemoveMember** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicegroup-removemember)メソッド呼び出し[**リリース**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-release) IServiceSink オブジェクトをサービスのグループから削除します。

### <a name="span-idreferencecountingonoutputparametersspanspan-idreferencecountingonoutputparametersspanspan-idreferencecountingonoutputparametersspanreference-counting-on-output-parameters"></a><span id="Reference_Counting_on_Output_Parameters"></span><span id="reference_counting_on_output_parameters"></span><span id="REFERENCE_COUNTING_ON_OUTPUT_PARAMETERS"></span>出力パラメーターの参照カウント

Output パラメーターを通じて、呼び出し元へのオブジェクト参照を渡すメソッドを呼び出す必要があります[ **AddRef** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)オブジェクトを返します前に (またはオブジェクトに独自の参照を解放する前に)。 この動作は、呼び出し元が、呼び出しからの戻り時に有効な参照を保持していることを確認する必要があります。 呼び出し元が通話を担当[**リリース**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)オブジェクトを使用してこれが完了するとします。

たとえば、 [ **IMiniportWaveCyclic::NewStream** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclic-newstream)メソッド呼び出し[ **AddRef** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)ストリーム、サービスのグループおよび DMA チャネル呼び出し元 (WaveCyclic ポート ドライバー) に出力するオブジェクト。 呼び出し元が不要になった必要になった場合は、これらの参照を解放する責任を負います。 実装については、 **IMiniportWaveCyclic::NewStream**方式でこの動作は、Sb16 サンプル アダプターで、Microsoft Windows Driver Kit (WDK) を参照してください。

### <a name="span-idexceptionstotherulesspanspan-idexceptionstotherulesspanspan-idexceptionstotherulesspanexceptions-to-the-rules"></a><span id="Exceptions_to_the_Rules"></span><span id="exceptions_to_the_rules"></span><span id="EXCEPTIONS_TO_THE_RULES"></span>ルールの例外

このメソッドを実行する一般的な参照カウントの説明については、*もできます*出力パラメーターは、「 [ **IMiniportWavePci::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-newstream)します。

 

 




