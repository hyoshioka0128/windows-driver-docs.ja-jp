---
title: WMI クラスを処理するためにデザイン ミニポート コールバック ルーチン
description: データ フィールドを含む WMI クラスを処理するミニポート ドライバー コールバック ルーチンの設計
ms.assetid: 6e08f9c1-e541-4e5f-8c99-f81d5793cc21
keywords:
- WMI される Srb WDK の記憶域、コールバック ルーチンの設計
- コールバック ルーチン WDK WMI される Srb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 478d86a7bad8855bbe18e1a7be31ae08e0a8368f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368310"
---
# <a name="designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-with-data-fields"></a>データ フィールドを含む WMI クラスを処理するミニポート ドライバー コールバック ルーチンの設計


## <span id="ddk_designing_a_miniport_driver_callback_routine_that_handles_wmi_clas"></span><span id="DDK_DESIGNING_A_MINIPORT_DRIVER_CALLBACK_ROUTINE_THAT_HANDLES_WMI_CLAS"></span>


このセクションでは、コールバック ルーチンがデータ フィールドを持つ WMI クラスの入力と出力データを処理する必要がある方法について説明します.

WMI クラスにデータ フィールドが含まれている場合、WMI ツール スイートの間でデータの構造体の宣言が生成されます。 構造体の宣言では、入力データと、クラスに属している WMI メソッドのパラメーターが出力に生成される構造体とは別です。 WMI メソッドを処理するために、WMI ツール スイートを生成する構造体の詳細については、設計を処理する WMI クラスとメソッドのミニポート ドライバー コールバック ルーチンを参照してください。

たとえばには、次の WMI クラス定義をコンパイル**mofcomp**で .h ファイルを生成および**wmimofck**します。

```cpp
class HBAFCPBindingEntry
{
  [HBAType("HBA_FCPBINDINGTYPE"),
   Values{"TO_D_ID", "TO_WWN", "TO_OTHER"},
   ValueMap{"0", "1", "2"},
   WmiDataId(1)
  ]
  uint32  Type;
  [HBAType("HBA_FCID"),
   WmiDataId(2)
  ]
  HBAFCPID  FCPId;
  [HBAType("HBA_FCPSCSIENTRY"),
   WmiDataId(3)
  ]
  HBAScsiID  ScsiId;
};
```

結果として得られる .h ファイルは、次の構造体の宣言が含まれます。

```cpp
typedef struct _HBAFCPBindingEntry
{
  ULONG  Type;
  HBAFCPID  FCPId;
  HBAScsiID  ScsiId;
} HBAFCPBindingEntry, *PHBAFCPBindingEntry;
```

データ入力と出力データを管理するときに、SRB の入力と出力バッファーにこの構造体宣言をキャストすることができます。

、戻る前に、コールバック ルーチンを呼び出す必要があります[ **ScsiPortWmiPostProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmipostprocess)します。 この SCSI ポート WMI ライブラリ ルーチンでは、要求の状態と戻り値のデータのサイズなどの情報を要求コンテキストを更新します。 要求コンテキストに格納されているデータの詳細については、次を参照してください。 [ **SCSIWMI\_要求\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/ns-scsiwmi-scsiwmi_request_context)します。

 

 




