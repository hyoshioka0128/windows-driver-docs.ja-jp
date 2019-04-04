---
title: USB 3.0 データ構造体
description: このトピックでは、USB 3.0 ホスト コント ローラーのドライバーによって使用されるデータ構造について説明します。
ms.assetid: 39BD7413-48A5-4199-BA8E-D2A77E4D23F1
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e51c35d47e1bd4590fb18515f183bf40ff530755
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538013"
---
# <a name="usb-30-data-structures"></a>USB 3.0 データ構造体


このトピックでは、USB 3.0 ホスト コント ローラーのドライバーによって使用されるデータ構造について説明します。 これらのデータ構造を理解する際に役立つを使用して、 [USB 3.0](usb-3-extensions.md)と[RCDRKD](rcdrkd-extensions.md)デバッガー拡張機能のコマンドを効果的にします。 ここでは、データ構造と一致する名前がある、 [USB 3.0 仕様](https://go.microsoft.com/fwlink/p?LinkID=224892)します。 仕様により、さらに、USB 3.0 に関する知識は、拡張機能のコマンドを使用して、USB 3.0 ドライバーをデバッグする機能を強化します。

USB 3.0 ホスト コント ローラーのドライバーには、コアの USB 3.0 ドライバー スタックの一部です。 詳細については、[USB ドライバー スタック アーキテクチャ](https://go.microsoft.com/fwlink/p?LinkID=251983)を参照してください。

各 USB 3.0 ホスト コント ローラーは最大 255 のデバイスを持つことができ、デバイスごとに最大 31 個のエンドポイントを持つことができます。 次の図は、1 つのホスト コント ローラーと接続されたデバイスを表すデータ構造体の一部を示します。

![1 つのホスト コント ローラーと接続されたデバイスをデバイス コンテキストを持つをさらに持つスロットと終了点のコンテキストを表す usb 3.0 データ構造体](images/usb3structures01.png)

## <a name="span-iddevicecontextbasearrayspanspan-iddevicecontextbasearrayspanspan-iddevicecontextbasearrayspandevice-context-base-array"></a><span id="Device_Context_Base_Array"></span><span id="device_context_base_array"></span><span id="DEVICE_CONTEXT_BASE_ARRAY"></span>デバイス コンテキストの基本の配列


デバイス コンテキスト ベースの配列は、デバイス コンテキストの構造体へのポインターの配列です。 ホスト コント ローラーに接続されている各デバイスの 1 つのデバイス コンテキスト構造があります。 要素が 1 255 までからは、デバイス コンテキストの構造体をポイントします。 要素 0 ホスト コント ローラーのコンテキスト構造体をポイントします。

## <a name="span-iddevicecontextandslotcontextspanspan-iddevicecontextandslotcontextspanspan-iddevicecontextandslotcontextspandevice-context-and-slot-context"></a><span id="Device_Context_and_Slot_Context"></span><span id="device_context_and_slot_context"></span><span id="DEVICE_CONTEXT_AND_SLOT_CONTEXT"></span>デバイス コンテキストとスロットのコンテキスト


デバイス コンテキストの構造は、エンドポイント コンテキストを構造体へのポインターの配列を保持します。 デバイス上の各エンドポイントの 1 つのエンドポイント コンテキスト構造があります。 要素が 1 31 までからは、エンドポイントの Context 構造体をポイントします。 スロットの Context 構造体は、デバイスのコンテキスト情報を保持するポイントが 0 の要素。

## <a name="span-idcommandringspanspan-idcommandringspanspan-idcommandringspancommand-ring"></a><span id="Command_Ring"></span><span id="command_ring"></span><span id="COMMAND_RING"></span>コマンドのリング


コマンドのリングは、ホスト コント ローラーにコマンドを渡すソフトウェアによって使用されます。 これらのコマンドの一部は、ホスト コント ローラーに転送し、いくつかは、ホスト コント ローラーに接続されている特定のデバイスに転送します。

## <a name="span-ideventringspanspan-ideventringspanspan-ideventringspanevent-ring"></a><span id="Event_Ring"></span><span id="event_ring"></span><span id="EVENT_RING"></span>イベントのリング


イベントのリングは、ソフトウェアにイベントを渡すホスト コント ローラーによって使用されます。 これはイベント リングでは、ホスト コント ローラーは、ドライバー操作が完了したことを通知するために使用する構造があります。

## <a name="span-iddoorbellregisterarrayspanspan-iddoorbellregisterarrayspanspan-iddoorbellregisterarrayspandoorbell-register-array"></a><span id="Doorbell_Register_Array"></span><span id="doorbell_register_array"></span><span id="DOORBELL_REGISTER_ARRAY"></span>ドアベル レジスタ配列


登録ドアベル配列は、ドアベル レジスタは、ホスト コント ローラーに接続されている各デバイスに 1 つの配列です。 1 ~ 255 の要素は、ドアベルのレジスタです。 要素の 0 は、コマンドのリング内の保留中のコマンドがあるかどうかを示します。

デバイスの登録ドアベルにコンテキスト情報を記述することで実行するデバイスに関連する、またはエンドポイントに関連する作業があるホスト コント ローラーのソフトウェアに通知します。

次の図は、前の図の右側が続行されます。 1 つのエンドポイントを表す追加のデータ構造が表示されます。

![usb 3.0 構造が表示されたエンドポイントを持つデータ コンテキストを持つデータと tds 複数 trbs](images/usb3structures02.png)

## <a name="span-idtransferringspanspan-idtransferringspanspan-idtransferringspantransfer-ring"></a><span id="Transfer_Ring"></span><span id="transfer_ring"></span><span id="TRANSFER_RING"></span>リングを転送します。


各エンドポイントには 1 つまたは複数の転送の呼び出し回数。 転送のリングは、転送要求のブロック (TRBs) の配列です。 連続したデータのブロックを指す各 TRB (最大 64 KB) をハードウェアと 1 つの単位としてメモリの間で転送されます。

USB 3.0 core スタックは、USB クライアント ドライバーからの転送要求を受信したときに、転送用エンドポイント コンテキストを識別して、転送要求を 1 つまたは複数の転送記述子 (TDs) に分割します。 各 TD には、1 つまたは複数の TRBs が含まれています。

## <a name="span-idendpointcontextspanspan-idendpointcontextspanspan-idendpointcontextspanendpoint-context"></a><span id="Endpoint_Context"></span><span id="endpoint_context"></span><span id="ENDPOINT_CONTEXT"></span>エンドポイント コンテキスト


エンドポイント コンテキストを構造体では、1 つのエンドポイントのコンテキスト情報を保持します。 **デキュー**と**エンキュー**メンバーで、ソフトウェアによって TRBs が追加されて、TRBs はハードウェアによって使用されている場所の追跡に使用します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[USB の Windows 8 における革新的技術をデバッグします。](https://go.microsoft.com/fwlink/p/?LinkID=249153)

 

 






