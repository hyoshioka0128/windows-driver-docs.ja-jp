---
title: WDTF オブジェクトのログ記録
description: WDTF オブジェクトのログ記録
ms.assetid: A99E62D1-31A2-46B5-841B-F3969854E39A
keywords:
- WDK WDTF のログ記録
- WDK WDTF のトレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da9c7e1d7cfa1d9a855ef6c96bcacbf44dec20df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383752"
---
# <a name="wdtf-object-logging"></a>WDTF オブジェクトのログ記録





WDTF オブジェクト*ログ*により自動的に共通のログ ファイルにログ メッセージを記述するオブジェクトが WDTF WDTF 機能です。 オブジェクトのログ ファイルの名前は、TestTextLog.log と呼ばれます。 WDTF オブジェクトのログ記録は、2 つの主な利点です。 高レベルのメソッドの呼び出し、メソッドのパラメーターとメソッドの結果をログに WDTF オブジェクトのメソッドを使用して、テスト スクリプトの作成が簡単になります。 WDTF オブジェクトのログ記録は、共通のログ メッセージの書き込みの一貫性のあるメカニズムを提供することで、診断も向上します。

既定では、WDTF オブジェクトのログ記録が無効にします。 呼び出すことによってオブジェクトのログ記録を有効にすると、 [ **IWDTFConfig2::EnableObjectLogging** ](https://msdn.microsoft.com/library/windows/hardware/hh406389)メソッド。 ログ記録を有効にした後は一時的に無効にするか再、メソッドを呼び出して、特定のアクションまたはアクションのコレクションの有効[ **IWDTFAction2::EnableObjectLogging**](https://msdn.microsoft.com/library/windows/hardware/hh406319)、 [**IWDTFAction2::DisableObjectLogging**](https://msdn.microsoft.com/library/windows/hardware/hh406315)、 [ **IWDTFActions2::EnableObjectLogging**](https://msdn.microsoft.com/library/windows/hardware/hh406357)、および[ **IWDTFActions2::DisableObjectLogging**](https://msdn.microsoft.com/library/windows/hardware/hh406349)します。

ログ ファイルに書き込みを行う、WDTF ログ メッセージでは、一般的なパターンがあります。

```cpp
<OBJECT_NAME> : <TYPE> : - <METHOD_NAME>(<METHOD_PARAMS>) <Additional Info>
<OBJECT_NAME> : <TYPE> : Target: <DisplayName>
```

次の例への呼び出しのログ出力を示しています。 **DeviceDepot.Query("Volume::")** 例のシステムのログ記録が有効な場合。

```cpp
[ Output ]

WDTF_TARGETS    : INFO  :  - Query("Volume::")
WDTF_TARGETS    : INFO  :          Target: Generic volume
WDTF_TARGETS    : INFO  :          Target: Generic volume
WDTF_TARGETS    : INFO  :          Target: HL-DT-ST RW/DVD MU10N ATA Device
WDTF_TARGETS    : INFO  :          Target: Generic volume
WDTF_TARGETS    : INFO  :          Target: Generic volume
WDTF_TARGETS    : INFO  :          Target: Generic volume
```

オブジェクトのログ記録が有効になっている場合、オブジェクトのエラーのログ記録は既定で有効にします。 それ以外の場合、エラー ログの既定値は無効になります。 オブジェクトのログ記録のようなことができます有効/無効にするエラーのログ記録メソッドを呼び出して[ **IWDTFConfig2::EnableObjectErrorLogging**](https://msdn.microsoft.com/library/windows/hardware/hh406387)、 [ **IWDTFConfig2::DisableObjectErrorLogging**](https://msdn.microsoft.com/library/windows/hardware/hh406383)、 [ **IWDTFAction2::EnableObjectErrorLogging**](https://msdn.microsoft.com/library/windows/hardware/hh406317)、 [ **IWDTFAction2::DisableObjectErrorLogging**](https://msdn.microsoft.com/library/windows/hardware/hh406313)、 [ **IWDTFActions2::EnableObjectErrorLogging**](https://msdn.microsoft.com/library/windows/hardware/hh406353)、および[ **IWDTFActions2::DisableObjectErrorLogging**](https://msdn.microsoft.com/library/windows/hardware/hh406346)します。

エラーのログ記録は、ログ ファイルに書き込みを行う、WDTF ログ メッセージでは、次のパターンがあります。 最初のエラー ログにジャンプするには、「エラー」キーワードを探します。

``` syntax
<OBJECT_NAME> : <TYPE> : - <METHOD_NAME>(<METHOD_PARAMS>) <Additional Info>
<OBJECT_NAME> : <TYPE> : Target: <DisplayName>
<OBJECT_NAME> : ERROR : Status: <ErrorString>
```

呼び出すことによって、ログ ファイルにカスタム メッセージを書き込むオプションがある、 [ **IWDTFLog2::OutputInfo** ](https://msdn.microsoft.com/library/windows/hardware/hh451016)または[ **IWDTFLog2::OutputError** ](https://msdn.microsoft.com/library/windows/hardware/hh451014)メソッド。

使用可能なオブジェクトの一覧は、次を参照してください。 [WDTF オブジェクト名のタグ](wdtf-object-name-tags.md)します。

## <a name="related-topics"></a>関連トピック
[WDTF オブジェクト名のタグ](wdtf-object-name-tags.md)  
[有効化と WDTF トレースの表示](viewing-wdtf-traces.md)  



