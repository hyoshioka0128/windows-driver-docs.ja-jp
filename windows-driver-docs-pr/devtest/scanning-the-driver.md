---
title: ドライバーのスキャン
description: ドライバーのスキャン
ms.assetid: c36960b4-d97e-49b7-a7ad-e71b0820db8a
keywords:
- Static Driver Verifier WDK、DriverEntry ルーチンをスキャンします。
- StaticDV WDK、DriverEntry ルーチンをスキャンします。
- SDV の WDK DriverEntry ルーチンをスキャンします。
- DriverEntry ルーチン WDK Static Driver Verifier のスキャン
- WDK Static Driver Verifier のドライバー エントリ ポイントします。
- WDK Static Driver Verifier のエントリ ポイントします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9953e67c8242108d74aeeac2afc44be80ee3518a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559573"
---
# <a name="scanning-the-driver"></a>ドライバーのスキャン


ドライバーを使用して、スキャン、 **スキャン/** コマンド オプションは省略可能です。 ドライバーを検証する前にスキャンしない場合 SDV は関数の役割の型宣言をスキャンし、ドライバーを確認するときは、Sdv map.h ファイルを作成します。

このスキャンでは、SDV は、ドライバーを確認するために必要なドライバーのエントリ ポイントを検出しようとします。 Sdv map.h、ドライバーのソース ディレクトリに作成したファイルのスキャンの結果を記録します。

ただし、スキャン手順の後に、または後に、検証、SDV の正しいエントリ ポイントが検出されたことを確認するには、このファイルを確認することが非常に重要です。 エントリ ポイントがないか間違っている場合、検証は信頼できない可能性があります。 さらに、SDV では、すべてのエントリ ポイントを検出できない場合は、ドライバーを検証できません。 

のみ、ドライバーごとに 1 回スキャンする必要があるとします。 その後、SDV は、今後の認証ドライバーの Sdv map.h ファイルを保持します。

### <a name="span-idexaminethesdvmaphfilespanspan-idexaminethesdvmaphfilespanexamine-the-sdv-maph-file"></a><span id="examine_the_sdv_map_h_file"></span><span id="EXAMINE_THE_SDV_MAP_H_FILE"></span>Sdv map.h ファイルを調べる

スキャン コマンドを実行しているかと、ドライバーの検証、Sdv map.h ファイルを開き、ファイルを確認します。 Sdv map.h は、書式設定されたテキスト ファイルです。 メモ帳などの任意のテキスト エディターを読み取ることができます。

ドライバーの宣言された関数のロールの種類と Sdv map.h ファイルの内容を比較します。 ドライバーのコールバックまたはディスパッチ ルーチンが正しく識別されていることを確認する Sdv map.h ファイルの内容を確認します。

Sdv map.h ファイルがすべてのエントリ ポイント; は、ドライバーの一覧を表示する必要はありません。のみ IRP の主要な関数のコードまたは分析で使用される関数のロールの種類のエントリ ポイント。 ファイルに任意の IRP の主要な関数のコードまたは関数のロールの種類を追加することはできません。

Sdv map.h ファイルの詳細については、次を参照してください。 [Sdv map.h](sdv-map-h.md)します。 形式については、「 [Sdv map.h ファイルの形式](format-of-the-sdv-map-h-file.md)します。 Sdv map.h ファイルに含まれるエラーについては、 [Sdv map.h ファイルを承認する](approving-the-sdv-map-h-file.md)します。

失敗から次の例は、Sdv map.h ファイルのコンテンツ\_driver1、ツールのサンプル WDM ドライバー\\sdv\\サンプル\\失敗\_ドライバー\\wdm ディレクトリ。

```
//Approved=false
//DriverAddDevice
#define fun_AddDevice DriverAddDevice
//DriverEntry
#define fun_DriverEntry DriverEntry
//DriverUnload
#define fun_DriverUnload DriverUnload
//CompletionRoutine
#define fun_IO_COMPLETION_ROUTINE_1 CompletionRoutine
//DpcForIsrRoutine
#define fun_IO_DPC_ROUTINE_1 DpcForIsrRoutine
//DispatchCreate
#define fun_IRP_MJ_CREATE DispatchCreate
//DispatchPnp
#define fun_IRP_MJ_PNP DispatchPnp
//DispatchPower
#define fun_IRP_MJ_POWER DispatchPower
//DispatchRead
#define fun_IRP_MJ_READ DispatchRead
//DispatchSystemControl
#define fun_IRP_MJ_SYSTEM_CONTROL DispatchSystemControl
//InterruptServiceRoutine
#define fun_KSERVICE_ROUTINE_1 InterruptServiceRoutine
```

### <a name="span-idcorrectthesdvmaphfilespanspan-idcorrectthesdvmaphfilespancorrect-the-sdv-maph-file"></a><span id="correct_the_sdv_map_h_file"></span><span id="CORRECT_THE_SDV_MAP_H_FILE"></span>Sdv map.h ファイルを修正します。

ドライバーを確認する前に、Sdv map.h ファイルのエラーを修正します。 SDV は、Sdv map.h ファイルが正しくないか許可されていませんが、検証の結果を信頼できない可能性がある場合でも、ドライバーを確認することができます。 たとえば、ドライバーのディスパッチまたはコールバック ルーチンが対応する関数の役割の種類を使用してに宣言しない場合ドライバーのルーチンは Sdv map.h ファイルには表示されません。 そのため、検証の一部としてこれらのルールを指定した場合でも、SDV は該当なしとロールの種類の関数を使用するルールと見なすので、コード内の欠陥を検索が欠落する可能性があります。

Sdv map.h ファイルを修正するには、関数の適切なロールの種類を使用して、ドライバーのディスパッチまたはコールバック ルーチンが宣言されていることを必ずします。 ドライバーを再スキャンし、Sdv map.h ファイルに表示されることを確認します.

### <a name="span-idapprovethesdvmaphfilespanspan-idapprovethesdvmaphfilespanapprove-the-sdv-maph-file"></a><span id="approve_the_sdv_map_h_file"></span><span id="APPROVE_THE_SDV_MAP_H_FILE"></span>Sdv map.h ファイルを承認します。

Sdv map.h ファイルが正しいことを決定した後、ファイルを承認することができます。 場合は、ファイルには変更しないようにして、承認する必要はありません。

SDV は、Sdv map.h ファイルが承認されていない場合でも、ドライバーを確認します。

ファイルの最初の行で、Sdv map.h ファイルを承認するには、次のように変更します。

```
//Approved=false
```

これを次のように変更します。

```
//Approved=true
```

のみ、ドライバーごとに 1 回 Sdv map.h ファイルを承認する必要があるとします。 その後、SDV は、今後の認証ドライバーの承認済みの Sdv map.h ファイルを保持します。 SDV 関数の役割の型宣言に対してもう一度、ソース コードをスキャンする場合は、ファイルを削除します。

次の例では、KMDF サンプル ドライバーの場合、承認済みの Sdv map.h ファイルが失敗する\_Driver1 します。 SDV は、Sdv map.h ファイルを使用して、SDV の検証に必要な関数のロールの種類と、ドライバーの宣言されたコールバック関数をマップします。

```
//Approved=true
//DriverEntry
#define fun_DriverEntry DriverEntry
//EvtDriverDeviceAdd
#define fun_WDF_DRIVER_DEVICE_ADD EvtDriverDeviceAdd
//EvtIoDeviceControl
#define fun_WDF_IO_QUEUE_IO_DEVICE_CONTROL EvtIoDeviceControl
//EvtIoInternalDeviceControl
#define fun_WDF_IO_QUEUE_IO_INTERNAL_DEVICE_CONTROL EvtIoInternalDeviceControl
//EvtIoRead
#define fun_WDF_IO_QUEUE_IO_READ EvtIoRead
//EvtRequestCancel
#define fun_WDF_REQUEST_CANCEL_1 EvtRequestCancel
```

 

 





