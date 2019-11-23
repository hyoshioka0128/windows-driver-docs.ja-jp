---
title: 仮想サブユニット ドライバーに関する注意事項
description: 仮想サブユニット ドライバーに関する注意事項
ms.assetid: e484f815-73a8-46f1-956e-ee16b1856bd0
keywords:
- Avc 関数ドライバー WDK、仮想サブユニットドライバー
- 仮想サブユニットドライバー WDK AV/C
- 外部デバイス WDK AV/C
- IOCTL_AVC_CLASS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca049d36082fae78fa7ef090595053b578446caf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845279"
---
# <a name="virtual-subunit-driver-notes"></a>仮想サブユニット ドライバーに関する注意事項


仮想サブシステムドライバーは、外部の AV/c デバイスからの制御、状態、および通知の AV/C 要求とコマンドに応答します。これには、 *avc* [ **\_avc\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_class)インターフェイスを使用します。

IOCTL\_AVC\_クラス subfunction コード[**avc\_関数\_GET\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-get-request)および[**avc\_関数**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-send-response)、仮想サブユニットドライバーが仮想ドライバースタックの残りの部分と対話するための主要なメカニズムです。\_\_ 仮想サブシステムドライバーは、 **avc\_関数**を送信し\_[**Irp の\_IRP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)に\_要求の irp を渡し*ます*。 irp には、\_デバイスルーチン (irp\_\_完了後に、スタック内の基になるドライバーによって\_デバイスが正常に開始されます) があります。\_ AVC\_関数の i/o 完了ルーチン **\_GET\_request** IRP は、仮想サブユニットの要求が受信されるたびに呼び出されます。 I/o 完了ルーチンは、(AV/C プロトコル規則に従って) 100 ミリ秒以内に、( **AVC\_関数\_** 非同期 IRP で\_応答を送信する) 応答を送信する必要があります。要求に含まれている[**AVC\_コマンド\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_command_irb)構造体を使用して、応答を送信できます。 その後、応答の i/o 完了ルーチンから最終的に戻る前に、\_REQUEST IRP を取得\_ために、 **AVC\_関数**を再送信する必要があります。

仮想ドライバスタック内のサブユニットドライバが、外部デバイスにコマンドを直接送信することはできません。 ピアドライバースタックは、この機能を提供します。 ただし、仮想サブシステムドライバーでは、 [**avc\_関数を使用して\_ピア\_do**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-find-peer-do)と[**avc\_関数**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-peer-do-list)を検索\_ことができます。[**これにより**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_class)、サブユニットのピアインスタンスを検出して参照し、*外部の AV* /C と対話することができます。\_\_\_\_\_

列挙された各仮想サブユニットについて、 *Avc*は対応するデバイスオブジェクトを作成します。 その結果、仮想サブユニットが追加および削除されると、 *Avc*は IEEE 1394 バスリセットをトリガーします。 このリセットにより、IEEE 1394 バス上の他のデバイスが、コンピューターで公開されている新しい機能を検出できるようになります。 仮想サブユニットドライバーは、 *Avc*インスタンスのレジストリ設定に基づいて読み込まれます。これは、実行時に IOCTL コード要求によって追加および削除できます。 *Avc*では、同じ種類の複数の仮想サブユニットを区別できないため、これらのサブユニットを追加または削除すると、対応する仮想サブシステムドライバーが最も大きいサブレベル識別子で読み込まれ、アンロードされます。

仮想サブユニットドライバーは、太いまたは細にすることができます。 唯一の要件は、WDM ドライバーとして記述されていることです。 シックドライバーは、仮想デバイスのほとんどの機能を実装します。 シンドライバは、仮想デバイスの機能へのプロキシインターフェイスを提供します。これは、別のドライバまたはユーザーモードコンポーネントにすることができます。 ユーザーモードと仮想サブユニットドライバー間のインターフェイスは実装固有であり、IOCTL コード、プライベートデバイスインターフェイス ( [**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)を参照)、または[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) (WMI) を使用して実現できます。

VEN\_ と MOD\_ の値は、*の仮想*インスタンスが読み込まれる原因となった INF ファイルで指定されているものと同じです。 TYP\_ と ID\_ の値は、 *Avc*によって仮想サブユニットが列挙されるときに指定されます。

仮想サブユニットの列挙は、 [**ioctl\_avc\_UPDATE\_仮想\_サブユニット\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_update_virtual_subunit_info)、 [**ioctl\_AVC\_\_仮想\_サブユニット\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_remove_virtual_subunit_info)、および[**ioctl\_avc\_BUS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_bus_reset)の ioctl コードをリセットすることで実現されます。

適切な IEEE 1394 Ioctl、 **IEEE1394\_api\_追加して\_仮想\_デバイス**と IEEE1394\_api を追加し\_**仮想\_デバイスを削除**して列挙プロセスを開始する必要があります。\_ 詳細については (IOCTL のサブコマンド\_IEEE1394\_API\_要求)」を参照してください。 V1394*ファイルには、この*目的のデバイス識別子 (ID) が既に含まれています。これは、カスタム inf ファイルで別の識別子が指定されている可能性がありますが、\\A02D & 10001 です。

仮想サブユニットを静的に列挙する別の方法として、INF ファイルを使用できます。

仮想デバイスの一覧のキーの下にある各値は、パックされたサブユニットアドレス (AV/C 一般仕様で説明されているように、サブユニットの種類と最大識別子の組み合わせ) です。 サブユニットアドレスに関連付けられている名前は問題ではありませんが、そのインスタンスで一意である必要があります。 プログラムによって作成された場合は、競合を避けるために、値の名前に連続した番号が付けられます。

たとえば、1つの仮想チューナーサブユニットを INF ファイルから作成するには、次の**AddReg**ディレクティブを使用します。

```INF
[Subunit_Device.NT.HW.AddReg]
HKR,%VirtualAvc.DeviceList%,Tuner,0x00000001,0x28 ;0x00000001 = Binary value, 0x28 = Registry key value
```

このディレクティブによって、0x28 の REG\_BINARY 値が追加されます (サブタイプの型0x5 が最上位5ビットにパックされ、最大識別子が0x0 で、最小の3ビットになります)。 ここでは最大で0x0 の識別子は、その種類のサブユニットが1つあることを意味します。

**注**  : サブユニットの INF ファイルの `[Strings]` セクションで `%VirtualAvc.DeviceList%` トークンを定義する必要もあります。
