---
title: SCSI パススルー要求を Storport に使用してクラスドライバーをバイパスする
description: SCSI パススルー要求を Storport に使用してクラスドライバーをバイパスする
ms.assetid: 1162a1e7-a4f8-446f-8106-527f9b916382
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69ef1a01a31c56466e4634e2c594ab4c2a9e7eb5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845099"
---
# <a name="bypass-a-class-driver-with-scsi-pass-through-requests-to-storport"></a>SCSI パススルー要求を Storport に使用してクラスドライバーをバイパスする

ほとんどの場合、クラスドライバーは、Storport と上位レベルのドライバーおよびアプリケーション間のすべての通信を仲介します。 ただし、一部のターゲットデバイスにはクラスドライバーがありません。 このようなデバイスのドライバーは、"パススルー" 要求と呼ばれる要求のクラスを使用して、Storport と直接通信する必要があります。 パススルー要求を使用するには、クラスドライバーに依存せずに、要求で使用される CDB を設定するために、上位レベルのコンポーネントが必要です。

クラスドライバーが存在し、デバイスが要求されている場合は、適切なデバイスハンドルを開いて、"パススルー" 要求をクラスドライバーに送る必要があります。 デバイスのクラスドライバーがなく、デバイスが要求されていない場合は、適切なデバイスハンドルを開くことによって、"パススルー" 要求がアダプターに直接送信されることがあります。

SCSI パススルー要求は、irp の種類が irp\_MJ\_デバイス\_コントロールであり、ioctl の ioctl コードを使用して[ **\_scsi\_パス\_経由**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)または ioctl\_を通過\_[ **\_DIRECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through_direct)。 要求がクラスドライバーを介して渡される場合、クラスドライバーは、IRP の**Minorfunction**コードを、デバイス\_コントロール\_の IRP\_MJ に設定することを義務としています。 Storport は、この値をチェックして、パススルー要求がクラスドライバーをバイパスしたかどうかを確認します。 ターゲットデバイスがストレージクラスドライバーによって要求されている場合、パススルー要求を直接 Storport に送信するアプリケーションエラーです。

Storport は、パススルー要求に埋め込まれている SCSI コマンドの有効性をチェックしません。

ストレージクラスドライバーから見た SCSI パススルー要求の詳細については、「 [Scsi パススルー要求の処理](handling-scsi-pass-through-requests.md)」を参照してください。

 

 




