---
title: UMDF ドライバーでのバッファー アクセス方法の管理
description: UMDF ドライバーを記述する場合は、フレームワークが読み取りおよび書き込み要求に使用するバッファーアクセスメソッドの設定と、デバイスの i/o 制御要求に対して設定を指定できます。
ms.assetid: BDB78BCD-1964-431B-BE99-CABA6DF44D7A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac48e52baff48165c5a02741ce034308f25ca774
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843154"
---
# <a name="managing-buffer-access-methods-in-umdf-drivers"></a>UMDF ドライバーでのバッファー アクセス方法の管理


UMDF ドライバーを記述する場合は、フレームワークが読み取りおよび書き込み要求に使用する[バッファーアクセスメソッド](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)の設定と、デバイスの i/o 制御要求に対して*設定*を指定できます。 UMDF ドライバーが提供する値は、基本設定のみであり、フレームワークによって使用されるとは限りません。

-   [適切なバッファーアクセス方法の指定](#specifying-preferred-buffer-access-method)
-   [I/o 要求のアクセスメソッドを取得する](#retrieving-access-method)
-   [バッファリングされる i/o と直接 i/o の両方からの変換](#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)

## <a href="" id="specifying-preferred-buffer-access-method"></a>適切なバッファーアクセス方法の指定


Umdf バージョン2.0 以降では、UMDF ドライバーは[**Wdfdeviceinitsetiotypeex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)を呼び出して、読み取り/書き込み要求およびデバイス i/o 制御要求に対して優先アクセスメソッドを登録します。

ドライバーが[**Wdfdeviceinitsetiotypeex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)を呼び出さない場合、UMDF は、このデバイスへの i/o 要求に対してバッファーされたメソッドを使用します。

フレームワークでは、次の規則を使用して、使用するアクセス方法を決定します。

-   ドライバースタック内のすべての UMDF ドライバーは、デバイスのバッファーにアクセスするために同じ方法を使用する必要があります。また、フレームワークはバッファーされた i/o を優先します。

    UMDF によって、一部のドライバーでバッファー i/o またはデバイスのダイレクト i/o が使用されていると判断されたが、他のドライバーがそのデバイスに対してバッファリングされた i/o のみを優先する場合、UMDF はすべてのドライバーにバッファー i/o を使用します。 1つまたは複数のスタックのドライバーがバッファー内 i/o のみを優先し、他のドライバーが直接 i/o を優先する場合、UMDF はシステムイベントログにイベントを記録し、ドライバースタックを開始しません。

    ドライバーは[**WdfDeviceGetDeviceStackIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdevicestackiotype)を呼び出して、UMDF がデバイスの読み取り/書き込み要求と i/o 制御要求に割り当てたバッファーアクセスメソッドを特定できます。

-   場合によっては、UMDF によってデバイスに直接 i/o が割り当てられますが、最適なパフォーマンスを得るには、1つまたは複数のデバイスの要求に対してバッファー内 i/o を使用します。 たとえば、UMDF では、直接アクセス用のバッファーをマップするよりも高速にデータをドライバーのバッファーにコピーできる場合は、小さなバッファーにバッファー i/o を使用します。

    必要に応じて、ドライバーは[**Wdfdeviceinitsetiotypeex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)を呼び出すときに**directtransferthreshold**値を提供できます。 フレームワークは、この値を使用して、フレームワークが直接 i/o を使用する最小バッファーサイズを決定します。 通常は、最適なパフォーマンスを提供する設定がフレームワークによって使用されるため、この値を指定する必要はありません。

-   UMDF は、メモリページの境界で開始および終了するバッファー領域に対してのみ、direct i/o を使用します。 バッファーの先頭または末尾がページの境界上にない場合、UMDF はバッファーのその部分に対してバッファーされた i/o を使用します。 言い換えると、複数の i/o 要求で構成される大規模なデータ転送の場合、UMDF はバッファー i/o とダイレクト i/o の両方を使用することがあります。

-   デバイスの i/o 制御要求の場合、UMDF は直接 i/o を使用します。これは、i/o 制御コード (IOCTL) が直接 i/o を指定し、そのデバイスのすべての UMDF ドライバーが[**Wdfdeviceinitsetiotypeex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)を呼び出して直接アクセス方法を指定している場合のみです。

## <a href="" id="retrieving-access-method"></a>I/o 要求のアクセスメソッドを取得する


ドライバーは、バッファーアクセス方法に関係なく、同じセットの要求オブジェクトメソッドを使用してデータバッファーにアクセスします。 そのため、ほとんどのドライバーでは、通常、UMDF がバッファー i/o を使用しているかどうか、または i/o 要求に直接 i/o を使用しているかどうかを知る必要はありません。

場合によっては、i/o 要求のアクセス方法がわかっていれば、ドライバーのパフォーマンスを向上させることができます。 たとえば、通常は直接 i/o を使用する高スループットデバイスを考えてみます。 ドライバーは、i/o 要求を受信すると、共有バッファー領域から検証用のローカルドライバーメモリにデータをコピーします。

ただし、ドライバーは、バッファーに格納された i/o を使用するバッファーを受け取ることがあります。 I/o マネージャーはこのデータを中間バッファーに既にコピーしているので、ドライバーはパラメーターをローカルにコピーする必要はありません。 コピー操作を回避することで、ドライバーによってパフォーマンスが向上します。

UMDF ドライバーは、 [**WdfRequestGetEffectiveIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgeteffectiveiotype)を呼び出して、i/o 要求のバッファーアクセスメソッドを取得します。 前述のように、特定の要求の i/o の種類は、デバイスのフレームワークによって割り当てられた i/o の種類の設定とは異なる場合があります。

## <a href="" id="using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers"></a>バッファリングされる i/o と直接 i/o の両方からの変換


UMDF ドライバーでは、"どちらの" メソッドも使用できません。

ただし、一部のデバイス i/o 制御コード (Ioctl) の[定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)では、要求で "指定なし" メソッドが使用されるように指定されています。 必要に応じて、UMDF ドライバーは、このようなデバイス i/o 制御要求のバッファーアクセスメソッドをバッファー i/o または直接 i/o に変換できます。 次の手順を使用します。

1.  ドライバーの INF ファイルの[**Inf DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)に[Umdfmethodneitheraction](specifying-wdf-directives-in-inf-files.md)ディレクティブを含めます。 ディレクティブの値を設定して、UMDF が "どちらの" アクセス方法を使用するデバイス i/o 制御要求をドライバーに渡す必要があることを示すことができます。 (それ以外の場合、UMDF は、エラー状態の値を使用してこれらの i/o 要求を完了します)。

2.  UMDF が[バッファー i/o](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers#buffered)または[直接](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers#direct)i/o に提供するオブジェクトメソッドを使用して、i/o 要求のバッファーにアクセスします。

"なし" メソッドを使用する IOCTL 要求のサポートを有効にする必要があります。これは、UMDF がアクセスメソッドをバッファー i/o またはダイレクト i/o に変換できることが確実である場合に限ります。 たとえば、IOCTL が、 [I/o 制御コードのバッファーの説明](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)に記述されているバッファー指定規則に従っていない、カスタマイズされた要求を指定した場合、UMDF はバッファーを変換できません。

 

 





