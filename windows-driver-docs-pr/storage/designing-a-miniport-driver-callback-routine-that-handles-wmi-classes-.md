---
title: WMI クラスを処理するミニポートコールバックルーチンの設計
description: データ フィールドを含む WMI クラスを処理するミニポート ドライバー コールバック ルーチンの設計
ms.assetid: 6e08f9c1-e541-4e5f-8c99-f81d5793cc21
keywords:
- WMI SRBs WDK storage、コールバックルーチンの設計
- コールバックルーチン WDK WMI SRBs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d94ed37757124a85364223668781a085850e013
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845186"
---
# <a name="designing-a-miniport-driver-callback-routine-that-handles-wmi-classes-with-data-fields"></a>データ フィールドを含む WMI クラスを処理するミニポート ドライバー コールバック ルーチンの設計


## <span id="ddk_designing_a_miniport_driver_callback_routine_that_handles_wmi_clas"></span><span id="DDK_DESIGNING_A_MINIPORT_DRIVER_CALLBACK_ROUTINE_THAT_HANDLES_WMI_CLAS"></span>


ここでは、データフィールドを持つ WMI クラスの入力データと出力データをコールバックルーチンで処理する方法について説明します。「」を参照してください。

WMI クラスにデータフィールドが含まれている場合は、WMI ツールスイートによってデータの構造体宣言が生成されます。 構造体の宣言は、クラスに属する WMI メソッドの入力パラメーターと出力パラメーターを保持するために生成される構造体とは別のものです。 Wmi ツールスイートが WMI メソッドを処理するために生成する構造体の詳細については、「メソッドを使用して WMI クラスを処理するミニポートドライバーコールバックルーチンの設計」を参照してください。

たとえば、次の WMI クラス定義を**mofcomp.exe**でコンパイルし、 **wmimofck**を使用して .h ファイルを生成するとします。

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

結果の .h ファイルには、次の構造体宣言が含まれます。

```cpp
typedef struct _HBAFCPBindingEntry
{
  ULONG  Type;
  HBAFCPID  FCPId;
  HBAScsiID  ScsiId;
} HBAFCPBindingEntry, *PHBAFCPBindingEntry;
```

入力データと出力データを管理するときに、この構造体の宣言を SRB の入力バッファーと出力バッファーにキャストできます。

を返す前に、コールバックルーチンは[**ScsiPortWmiPostProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmipostprocess)を呼び出す必要があります。 この SCSI ポート WMI ライブラリルーチンは、要求の状態や返されるデータのサイズなどの情報で要求コンテキストを更新します。 要求コンテキストに格納されているデータの詳細については、「 [**SCSIWMI\_request\_context**](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-scsiwmi_request_context)」を参照してください。

 

 




