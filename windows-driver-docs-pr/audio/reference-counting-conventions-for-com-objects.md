---
title: COM オブジェクト用の参照カウントの規則
description: COM オブジェクト用の参照カウントの規則
ms.assetid: e6b19110-37e2-4d23-a528-6393c12ab650
keywords:
- COM オブジェクトが WDK オーディオを参照する
- オブジェクトが WDK オーディオを参照する
- カウント参照の WDK オーディオ
- 参照カウント WDK オーディオ
- 入力パラメーター参照による WDK オーディオのカウント
- WDK オーディオをカウントする出力パラメーターの参照
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3e431a2cecc8f9f77c49d96682c1ade172b2d9c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832441"
---
# <a name="reference-counting-conventions-for-com-objects"></a>COM オブジェクト用の参照カウントの規則


## <span id="reference_counting_conventions_for_com_objects"></span><span id="REFERENCE_COUNTING_CONVENTIONS_FOR_COM_OBJECTS"></span>


オーディオインターフェイスのメソッドは、入力パラメーターとして、または出力パラメーターとして返す COM オブジェクトの参照をカウントするための一般的な一連の規則に従います。 これらのルールとその例外を以下にまとめます。 COM インターフェイスの詳細については、Microsoft Windows SDK のドキュメントの「COM」セクションを参照してください。

### <a name="span-idreference_counting_on_input_parametersspanspan-idreference_counting_on_input_parametersspanspan-idreference_counting_on_input_parametersspanreference-counting-on-input-parameters"></a><span id="Reference_Counting_on_Input_Parameters"></span><span id="reference_counting_on_input_parameters"></span><span id="REFERENCE_COUNTING_ON_INPUT_PARAMETERS"></span>入力パラメーターの参照カウント

オブジェクト*X*への参照を入力パラメーターとして受け取るメソッドを呼び出す場合、呼び出し元は、呼び出しの間、オブジェクトに対する独自の参照を保持する必要があります。 この動作は、オブジェクト*X*へのメソッドのポインターがを返すまで有効なままになるようにするために必要です。 このメソッドを実装するオブジェクト*Y*が、このメソッドからの戻り値を超えるオブジェクト*x*への参照を保持する必要がある場合、メソッドはを返す前に、オブジェクト*x*に対して[**AddRef**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)を呼び出す必要があります。 後でオブジェクト*x*を使用してオブジェクト*Y*を終了する場合は、object *x*で[**Release**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)を呼び出す必要があります。

たとえば、 [**Iservicegroup:: AddMember**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicegroup-addmember)メソッドは、サービスグループに追加する[iservices Ink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)オブジェクトで[**AddRef**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)を呼び出します。 この動作を補完するために、 [**Iservicegroup:: RemoveMember**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicegroup-removemember)メソッドは、サービスグループから削除する Iservices ink オブジェクトで[**Release**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)を呼び出します。

### <a name="span-idreference_counting_on_output_parametersspanspan-idreference_counting_on_output_parametersspanspan-idreference_counting_on_output_parametersspanreference-counting-on-output-parameters"></a><span id="Reference_Counting_on_Output_Parameters"></span><span id="reference_counting_on_output_parameters"></span><span id="REFERENCE_COUNTING_ON_OUTPUT_PARAMETERS"></span>出力パラメーターの参照カウント

出力パラメーターを使用して呼び出し元にオブジェクト参照を渡すメソッドは、を返す前 (またはオブジェクトへの独自の参照を解放する前) に、そのオブジェクトに対して[**AddRef**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)を呼び出す必要があります。 この動作は、呼び出し元が呼び出しから戻った時点で有効な参照を保持するようにするために必要です。 呼び出し元は、オブジェクトの使用が終了したときに、そのオブジェクトに対して[**Release**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)を呼び出す必要があります。

たとえば、 [**IMiniportWaveCyclic:: newstream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-newstream)メソッドは、呼び出し元 (WaveCyclic port driver) に出力するストリーム、サービスグループ、および DMA チャネルオブジェクトで[**AddRef**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-addref)を呼び出します。 呼び出し元は、不要になったときに、これらの参照を解放する必要があります。 この動作を示す**IMiniportWaveCyclic:: NewStream**メソッドの実装については、Microsoft Windows Driver KIT (WDK) の Sb16 サンプルアダプターを参照してください。

### <a name="span-idexceptions_to_the_rulesspanspan-idexceptions_to_the_rulesspanspan-idexceptions_to_the_rulesspanexceptions-to-the-rules"></a><span id="Exceptions_to_the_Rules"></span><span id="exceptions_to_the_rules"></span><span id="EXCEPTIONS_TO_THE_RULES"></span>ルールの例外

このメソッドが*DmaChannel*出力パラメーターに対して実行する、従来の参照カウントの詳細については、「 [**IMiniportWavePci:: newstream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)」を参照してください。

 

 




