---
title: wdfkd.wdftagtracker
description: Wdfkd.wdftagtracker 拡張機能では、指定したタグの追跡ツール (タグの値、行、ファイル、および時間を含む) すべての使用可能なタグ情報が表示されます。
ms.assetid: d8720446-58c1-4792-9e16-0facfe8fa39f
keywords:
- デバッグ wdfkd.wdftagtracker Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdftagtracker
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 53ebbd9d25c65adf13f5bbbb0edaa801cd452a23
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323264"
---
# <a name="wdfkdwdftagtracker"></a>!wdfkd.wdftagtracker


**! Wdfkd.wdftagtracker**拡張機能では、指定したタグの追跡ツール (タグの値、行、ファイル、および時間を含む) すべての使用可能なタグ情報が表示されます。

```dbgcmd
!wdfkd.wdftagtracker TagObjectPointer [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______TagObjectPointer______"></span><span id="_______tagobjectpointer______"></span><span id="_______TAGOBJECTPOINTER______"></span> *TagObjectPointer*   
タグの追跡ツールへのポインター。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
(省略可能)。 表示する情報の種類。 *フラグ*次のビットの組み合わせにすることができます。 既定値は、「0x0」です。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
履歴を表示します。 操作を取得およびのオブジェクトの操作を解放します。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
10 進数ではなく 16 進数で、オブジェクトの行番号を表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

タグの追跡ツールへのポインターを取得する、 [ **! wdfkd.wdfobject** ](-wdfkd-wdfobject.md)内部フレームワーク オブジェクト ポインターの拡張機能。

追跡タグを使用するには、カーネル モード ドライバー フレームワーク (KMDF) 検証ツールを有効にし、レジストリの追跡を処理する必要があります。 これらの設定は、ドライバーに格納されている**パラメーター\\Wdf**のサブキー、 **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\サービス**キー。

KMDF 検証機能を有効にする、0 以外の値を設定**VerifierOn**します。

ハンドルの追跡を有効にするには、値を設定**TrackHandles** 1 つまたは複数のオブジェクトの種類の名前にアスタリスクを指定または (\*) すべてのオブジェクトの種類を追跡するためにします。 たとえば、次の例では、すべて WDFDEVICE と WDFQUEUE オブジェクトへの参照の追跡を指定します。

```text
TrackHandles: MULTI_SZ: WDFDEVICE WDFQUEUE
```

ハンドル オブジェクトの種類の追跡を有効にすると、フレームワークは、その型の任意のオブジェクトに対して実行される参照を追跡します。 この設定は、ドライバーのメモリ リークが解放されていない参照が発生することを確認するのに役立ちます。 **TrackHandles** KMDF 検証機能が有効になっている場合にのみ機能します。

 

 





