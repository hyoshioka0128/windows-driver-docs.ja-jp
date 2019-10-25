---
title: WDTF オブジェクトのログ記録
description: WDTF オブジェクトのログ記録
ms.assetid: A99E62D1-31A2-46B5-841B-F3969854E39A
keywords:
- WDK WDTF のログ記録
- WDK WDTF のトレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adb9620eb10f19ee5716571fefdc6829324eb6f6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844817"
---
# <a name="wdtf-object-logging"></a>WDTF オブジェクトのログ記録





WDTF オブジェクト*ログ*機能は、wdtf オブジェクトがログメッセージを共通ログファイルに自動的に書き込むことができるようにする wdtf の機能です。 オブジェクトのログファイルの名前は TestTextLog .log と呼ばれます。 WDTF オブジェクトのログ記録には、2つの重要な利点があります。 これにより、WDTF object メソッドを使用して、高度なメソッド呼び出し、メソッドのパラメーター、およびメソッドの結果を記録することで、テストスクリプトの作成が簡単になります。 WDTF オブジェクトのログ記録では、共通ログメッセージを書き込むための一貫したメカニズムが提供されるため、diagnosability も向上します。

既定では、WDTF オブジェクトのログ記録は無効になっています。 オブジェクトのログ記録を有効にするには、 [**IWDTFConfig2:: EnableObjectLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfconfig2-enableobjectlogging)メソッドを呼び出します。 ログ記録を有効にした後、 [**IWDTFAction2:: EnableObjectLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfaction2-enableobjectlogging)、 [**IWDTFAction2::D isableobjectlogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfaction2-disableobjectlogging)、 [**IWDTFActions2:: メソッドを呼び出すことによって、特定のアクションまたはアクションのコレクションに対して一時的に無効にしたり、再度有効にしたりすることができます。EnableObjectLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)および[**IWDTFActions2::D isableObjectLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

WDTF によってログファイルに書き込まれるログメッセージには、一般的なパターンがあります。

```cpp
<OBJECT_NAME> : <TYPE> : - <METHOD_NAME>(<METHOD_PARAMS>) <Additional Info>
<OBJECT_NAME> : <TYPE> : Target: <DisplayName>
```

次の例では、システム例でログ記録が有効になっている場合に、Devicedepot の呼び出しのログ出力を示し**ます。**

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

オブジェクトのログ記録が有効になっている場合、オブジェクトエラーのログ記録は既定で有効になっています。 それ以外の場合、エラーログの既定値は無効になります。 オブジェクトのログと同様に、 [**IWDTFConfig2:: EnableObjectErrorLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfconfig2-enableobjecterrorlogging)、 [**IWDTFConfig2::D isableobjecterrorlogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfconfig2-disableobjecterrorlogging)、 [**IWDTFAction2:: EnableObjectErrorLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfaction2-enableobjecterrorlogging)[**の各メソッドを呼び出すことによって、エラーのログ記録を有効または無効にすることができます。IWDTFAction2::D isableObjectErrorLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtfaction2-disableobjecterrorlogging)、 [**IWDTFActions2:: EnableObjectErrorLogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)、 [**IWDTFActions2::D isableobjecterrorlogging**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

WDTF によってエラーログのログファイルに書き込まれるログメッセージは、次のパターンになります。 ログの最初のエラーに移動するには、キーワード "ERROR" を探します。

``` syntax
<OBJECT_NAME> : <TYPE> : - <METHOD_NAME>(<METHOD_PARAMS>) <Additional Info>
<OBJECT_NAME> : <TYPE> : Target: <DisplayName>
<OBJECT_NAME> : ERROR : Status: <ErrorString>
```

[**IWDTFLog2:: OutputInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtflog2-outputinfo)または[**IWDTFLog2:: OutputError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdtf/nf-wdtf-iwdtflog2-outputerror)メソッドを呼び出して、ログファイルにカスタムメッセージを書き込むこともできます。

使用可能なオブジェクトの一覧については、「 [Wdtf オブジェクト名タグ](wdtf-object-name-tags.md)」を参照してください。

## <a name="related-topics"></a>関連トピック
[WDTF オブジェクト名タグ](wdtf-object-name-tags.md)  
[WDTF トレースの有効化と表示](viewing-wdtf-traces.md)  



