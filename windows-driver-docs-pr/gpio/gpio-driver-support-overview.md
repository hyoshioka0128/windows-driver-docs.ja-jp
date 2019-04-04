---
title: GPIO ドライバー サポートの概要
description: 以降では、Windows 8、GPIO フレームワークの拡張機能 (GpioClx) には、GPIO コント ローラー デバイス用のドライバーの記述のタスクが簡略化します。
ms.assetid: 450E7F80-D9AC-4F52-8062-2DA5343C8D0F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdd49c365f797b1271206f9af87ecdde0a16b686
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529456"
---
# <a name="gpio-driver-support-overview"></a>GPIO ドライバー サポートの概要


以降では、Windows 8、GPIO フレームワークの拡張機能 (GpioClx) には、GPIO コント ローラー デバイス用のドライバーの記述のタスクが簡略化します。 さらに、GpioClx では、GPIO ピンに接続するための周辺機器のドライバーのサポートを提供します。 カーネル モード ドライバー フレームワーク (KMDF) をシステム提供の拡張機能である、GpioClx GPIO デバイス クラスのメンバーに共通するタスクの処理を実行します。

この概要では、次のトピックについて説明します。

- [GPIO ドライバー サポートの概要](#gpio-driver-support-overview)
    - [GPIO コント ローラーのドライバー](#gpio-controller-drivers)
    - [GPIO ピンを使用している周辺機器のデバイスのドライバー](#drivers-for-peripheral-devices-that-use-gpio-pins)

## <a name="gpio-controller-drivers"></a>GPIO コント ローラーのドライバー


ハードウェア ベンダーは、それぞれの GPIO コント ローラーを制御するドライバーを指定します。 GPIO コント ローラーのドライバーは、GPIO コント ローラーのすべてのハードウェア固有の操作を管理する KMDF ドライバーです。 GpioClx GPIO ピンが構成されているグループの I/O 要求を処理するために使用する GPIO コント ローラーのドライバーと連携データ入力とデータの出力として。 さらに、GpioClx 割り込みの入力として構成されている GPIO ピンからの割り込み要求を処理するために使用するこのドライバーと連携します。

GPIO コント ローラー デバイスは、いくつかの GPIO ピンにします。 これらのピンは、周辺機器に物理的に接続できます。 GPIO ピンは、データ入力、出力のデータ、または割り込み要求の入力として構成できます。 通常、GPIO ピンは専用の周辺機器にし、2 つまたは複数のデバイスで共有されません。 GPIO ピンと周辺機器の間の接続は、固定、(たとえば、周辺機器のデバイスを削除して、別のデバイスに置き換えること) をユーザーが変更ことはできません。 したがって、周辺機器の GPIO ピンの割り当ては、プラットフォーム ファームウェアで記述できます。




次の図は、GPIO コント ローラーのドライバーと GpioClx を示します。

![gpio コンポーネントのブロック図](images/gpiomodules.png)

GPIO コント ローラーのドライバーと GpioClx GpioClx デバイス ドライバー インターフェイス (DDI) 経由で互いと通信します。 GPIO コント ローラーのドライバー呼び出し[ドライバー サポート メソッド](https://msdn.microsoft.com/library/windows/hardware/hh439460)GpioClx により実装されます。 GpioClx 呼び出し[イベント コールバック関数](https://msdn.microsoft.com/library/windows/hardware/hh439464)GPIO コント ローラーのドライバーにより実装されます。

GPIO コント ローラーのドライバーは、GPIO コント ローラー デバイスのハードウェア レジスタに直接アクセスします。

GpioClx は、GPIO ピンに物理的に接続するための周辺機器のドライバーからの I/O 要求を処理します。 GpioClx では、これらの I/O 要求をイベントに GPIO コント ローラーのドライバーによって実装されるコールバック関数を呼び出すことによってこれを実行するシンプルなハードウェア操作に変換します。 たとえば、データの読み取りまたは一連の GPIO ピンにデータを書き込む、GpioClx 関数を呼び出すイベント コールバックなど[*クライアント\_ReadGpioPins* ](https://msdn.microsoft.com/library/windows/hardware/hh439404)と[*クライアント\_WriteGpioPins*](https://msdn.microsoft.com/library/windows/hardware/hh439439)します。 GpioClx は GPIO コント ローラーの I/O キューを管理し、それによってこのタスクの GPIO コント ローラーのドライバーを緩和します。

さらに、GpioClx は GPIO コント ローラーのデバイスからプライマリの割り込みを処理し、これらの割り込みを周辺機器のデバイス ドライバーが処理すると、セカンダリ割り込みにマップします。 プライマリの割り込みは、ハードウェア デバイスによって生成される割り込みです。 セカンダリの割り込みは、特定のプライマリ割り込みに応答のオペレーティング システムによって生成されます。 プライマリとセカンダリの両方の割り込みは、グローバル システムの割り込み (GSIs) によって識別されます。 ACPI のファームウェア ハードウェア プラットフォームをプライマリの割り込みを GSIs を割り当てられ、実行時に、オペレーティング システムはセカンダリの割り込みを GSIs を割り当てます。

たとえば、ファームウェアがハードウェア割り込みに GPIO コント ローラーから、GSI を割り当て、オペレーティング システムは、入力、割り込みとして構成されている GPIO ピンに、GSI を割り当てます。

GpioClx は、GPIO コント ローラーのデバイスからのハードウェアによって生成された、プライマリの割り込みを処理する ISR を実装します。 周辺機器の GPIO ピンでは、割り込みをアサートし、上、この pin が有効になっているし、マスクが解除されたプロセッサに対して割り込みを GPIO コント ローラー。 応答をカーネル トラップ ハンドラーを実行する GpioClx ISR をスケジュールします。 GpioClx ISR を呼び出して、割り込みの原因となった GPIO ピンを識別するために、 [*クライアント\_QueryActiveInterrupts* ](https://msdn.microsoft.com/library/windows/hardware/hh439395) GPIO コント ローラーによって実装されているイベントのコールバック関数ドライバー。 この pin に割り当てられているし、ハードウェア アブストラクション レイヤー (HAL) にこの GSI を渡します GSI し GpioClx ISR を検索します。 HAL は、この GSI に対して登録されている ISR を呼び出すことによって、セカンダリの割り込みを生成します。 この ISR は、最初に、割り込みをアサートする周辺機器のデバイスのドライバーに属しています。

プライマリとセカンダリの割り込みの詳細については、[GPIO 割り込み](https://msdn.microsoft.com/library/windows/hardware/hh406467)を参照してください。

## <a name="drivers-for-peripheral-devices-that-use-gpio-pins"></a>GPIO ピンを使用している周辺機器のデバイスのドライバー


起動時に、プラグ アンド プレイ (PnP) manager PnP デバイスと非 PnP デバイスの両方を列挙します。 GPIO ピンへの接続が修正されました。 非 PnP デバイス、PnP マネージャーはどの GPIO ピンは、これらのデバイスのハードウェアのシステムで管理されるリソースとして割り当てられている特定のプラットフォームのファームウェアを照会します。

KMDF ドライバーの周辺機器の中に割り当てられたハードウェア リソースを受け取る、 [ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック。 これらのリソースには、データの出力、データ入力、または割り込み要求の入力として構成されている GPIO ピンを含めることができます。

GPIO I/O リソースは、Windows 8 の新しい Windows リソースの種類です。 このリソースは、1 つのセットから構成またはことができる複数の GPIO ピンは、データの入力またはデータの出力としてのどちらを使用します。 周辺機器のデバイス ドライバーは、読み取りの GPIO I/O リソースを開き、ドライバーであるすべてのピン リソースのデータ入力します。 ドライバーでは、書き込みの GPIO I/O リソースが開いたら、ドライバーであるすべてのピン リソースのデータ出力します。 周辺機器のデバイス ドライバーが I/O の GPIO ピンのセットへの論理接続を開く方法を示すコード例では、次のトピックを参照してください。

[KMDF ドライバーを GPIO I/O ピンに接続します。](https://msdn.microsoft.com/library/windows/hardware/hh406474)

割り込みの入力として構成されている GPIO ピンは、ドライバーに通常の Windows 割り込みリソースとして割り当てられます。 割り込みリソースの抽象化には、ファクトのではなく、たとえば、プログラム可能割り込みコント ローラーの GPIO ピン留めして、割り込みを実装する場合がありますが非表示にします。 そのため、ドライバーできます割り込みの GPIO ベースのリソースと同様に処理割り込みの他のリソース。

GPIO ピン GPIO I/O リソースにアクセスするに周辺機器のデバイス ドライバーは、ピンへの論理接続を開く必要があります。 KMDF ドライバーは呼び出し、 [ **WdfIoTargetOpen** ](https://msdn.microsoft.com/library/windows/hardware/ff548634)接続を開くメソッドです。 この接続を介して、ドライバーは、GPIO ピンを I/O 要求を送信できます。 ドライバーの送信[ **IOCTL\_GPIO\_読み取り\_ピン**](https://msdn.microsoft.com/library/windows/hardware/hh406483) (入力ピンの場合)、これらのピンからデータを読み取り要求または[ **IOCTL\_GPIO\_書き込み\_ピン**](https://msdn.microsoft.com/library/windows/hardware/hh406487) (出力ピンの場合) にデータの書き込み要求。

割り込みリソースの GPIO ピンから割り込みを受信するに周辺機器のデバイス ドライバーは、割り込みサービス ルーチン (ISR) には、この暗証番号 (pin) によって実装される割り込みリソースからの割り込みの受信を登録する必要があります。 KMDF ドライバーは呼び出し、 [ **WdfInterruptCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547345)割り込みに ISR を接続するメソッド。 

 

 




