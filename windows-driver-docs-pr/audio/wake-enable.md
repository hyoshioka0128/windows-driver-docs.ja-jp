---
title: スリープ状態の解除
description: スリープ状態の解除
ms.assetid: f4a2d4b1-d3a0-449a-ac65-a448d2bcab5c
keywords:
- HD オーディオ、ウェイク有効化
- High Definition Audio (HD audio)、wake enable
- wake enable WDK audio
- 状態-変更イベントの WDK オーディオ
- 電源管理 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0b53df99b1ba7ef34893339156e848f8a279c81
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925621"
---
# <a name="wake-enable"></a>スリープ状態の解除


コーデックの電源を切る前に、コーデック関数ドライバーは通常、コーデックが電源ダウン状態のときに状態変更イベントが発生した場合に、コーデックがシステムをウェイクアップできるようにします。 オーディオコーデックの場合、ユーザーが入力ジャックにプラグを挿入するか、ジャックからプラグを削除すると、このようなイベントが発生する可能性があります。 モデムコーデックの場合、着信呼び出しを示すために電話が発信するときに、状態変更イベントが発生することがあります。 状態変更イベントの詳細については、intel [HD audio](https://www.intel.com/content/www/us/en/standards/intel-standards-and-initiatives.html) web サイトの「 *Intel High Definition audio Specification* 」を参照してください。

電源を切る準備をするために、関数ドライバーは、状態変更イベントが発生したときに HD オーディオバスコントローラーに通知するようにコーデックを最初に構成します。 次に、関数ドライバーは、 [**irp\_\_\_**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)がいっぱいになったことを知らせるスリープ状態の電源管理 irp を HD オーディオバスドライバーに送信し、コーデックからのウェイクアップシグナルを有効にするように指示します。 その後、ウェイクアップシグナルが有効になり、コーデックによってコーデックの SDI ラインを介してステータス変更イベントが送信されると、コントローラーはシステムにウェイクアップ信号を生成し、バスドライバーは IRP\_の完了\_待機\_ウェイク IRP を完了して関数ドライバーに通知します。

Wake イベントの後、バスドライバーは、ウェイクアップシグナルを生成したコーデックを特定し、そのコーデック\_で\_保留\_中の IRP の待機状態のウェイク irp を完了します。 ただし、コーデックにオーディオとモデムの両方の機能グループが含まれている場合、バスドライバーでは、どの関数グループがウェイクアップシグナルのソースであるかを判断する方法がありません。 この場合、関数ドライバーは独自のクエリをコーデックに送信して、ウェイクアップシグナルのソースを確認する必要があります。

 

 




